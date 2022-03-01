### RTSP协议通信及信息获取插件实践
#### 功能实现
插件主要实现RTSP协议的初步通信。确定协议开放后，尝试爆破目标设备的RTSP流媒体传输链接。
#### 代码分析
-   RTSP协议是构建于TCP协议上层的应用层协议，因此，需要使用TCP发包与之通信。代码如下：

```
ip = cli.String("ip")
conn, err := tcp.Connect(ip, 554)
data2 = "OPTIONS rtsp://"+ ip + "/stream1 RTSP/1.0\r\nCSeq: 2\r\n\r\n"
conn.Send(data2)
```
-   通过cli.String()方法获取参数"IP"后，使用tcp.Connect()方法建立链接。data2为构造的RTSP通信数据包。
    -   这里需要注意的是，数据包需要使用双引号括起来。如果发送的数据为HEX码，则需要将 HEX进行解码，具体操作如下：

    ```
    hex_code = "54657374"
    raw, err := codec.DecodeHex(hex_code)
    conn.Send(raw)
    ```
-   接收响应数据包的方法有好几种，这里选择官方文档中的接收方法 conn.RecvStringTimeout() 接收一个字符串,若超时则直接返回,参数为超时时间,单位s.

```
resp = conn.RecvStringTimeout(5)
```
-   conn.RecvStringTimeout()的返回值 ，数据类型为list，其中包含两个元素list[0]为响应的字符串，list[1]为响应错误信息。
-   确定可以通信后，插件会尝试爆破RTSP流媒体传输地址，当获取传输地址后，如果该目标RTSP协议未进行权限限制，则可以直接观看直播画面。
-   这里用到一个RTSP协议的一个特点便是，如果该地址存在，若权限允许则会返回200状态码，若权限不允许则会返回401状态码，若该地址不存在，则会返回404状态码。因此，我们可以通过判断状态码来确定该地址是否存在。代码如下：
```
stream_address = [
        "/Streaming/Channels/1",
        "/ch1/main/av_stream",
        "/cam/realmonitor?channel=1&subtype=0",
        "/1/D1",
        "/1/h264major",
        "/1/h264minor",
        "/media/video1/multicast",
        "/h264",
        "/mpeg4",
        "/video1",
    ]
for i,n = range stream_address {
    data  = "OPTIONS rtsp://"+ ip + n + " RTSP/1.0\r\nCSeq: 2\r\n\r\n"
    conn.Send(data)
    resp_1 = conn.RecvStringTimeout(5)
    println(resp_1[0])
    if re.Match(`RTSP/1.0 (200|401)`, resp_1[0]){
        stream = "rtsp://"+ ip + n
        flag = 1
        result["stream_address"] = stream
        break  
        } 
}
```
-   其他注意事项：
    -   插件输出建议使用yakit的方法输出，而不是使用 println() 直接打印
    -   使用yakit方法输出时，需在代码头部调用 yakit.AutoInitYakit() 方法
    
    ```
    1 yakit.AutoInitYakit()
    2 yakit.EnableTable("Output", ["ip", "port","stream_address"])
    3 loglevel("info")
    ```


