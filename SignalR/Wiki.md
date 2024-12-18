![image](https://github.com/user-attachments/assets/d7ac6b13-f6c4-4619-9597-af10a70e3b0b)# SignalR 实时双向通信功能

> SignalR是一个.Net开源库，用于构建需要实时进行用户交互和数据更新的Web应用，如在线聊天，游戏，天气或者股票信息更新等实时应用程序。
> 
> SignalR 提供了多种客户端库，如 JavaScript、.NET、Java、Python 等，可以方便地与各种客户端集成
> 
> 参考文献：[SignalR介绍简单示例教程入门版-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1160085)

### Web消息交互技术

![image](https://github.com/user-attachments/assets/f71f7188-9cd4-4938-a755-35670c05fb93)

### Comet技术

传统模式的 Web 系统以客户端发出请求、服务器端响应的方式工作。这种方式并不能满足很多现实应用的需求，譬如：

- **监控系统**：后台硬件热插拔、LED、温度、电压发生变化；
- **即时通信系统**：其它用户登录、发送信息；
- **即时报价系统**：后台数据库内容发生变化。

这些应用都需要服务器能实时地将更新的信息传送到客户端，而无须客户端发出请求。

Comet技术是解决上述问题的一种Web编程技术，用于实现Web应用程序中的实时消息传递。这种技术可以让Web应用程序在有新消息时，立即将消息推送给用户，而不需要用户刷新页面或手动获取消息。Comet技术可以通过在服务器和客户端之间保持长连接或轮询客户端的方式来实现。这种技术在实现在线聊天、实时数据更新等应用程序中非常有用，但也有一些缺点，例如可能会占用服务器资源和增加网络带宽消耗。

### SignalR 默认传输方式

![image](https://github.com/user-attachments/assets/32f4ff49-e3c3-49de-bfe8-379b14b25d41)

### SignalR 指定传输方式

如果开发人员想要让客户端按照特定的方式和顺序进行数据传输，可以通过使用
:::highlight blue 💡
$.connection.start({transport:['webSockets','foeverFrame',……]})
:::
当客户端和服务器端并不支持指定方式时，程序将按照默认规则匹配传输方式。  
用于指定传输方式的字符串常量定义如下：
- webSockets
- foeverFrame
- serverSentEvents
- longPolling

### SignalR 通信模式

- **Persistent Connections**：Persistent Connections表示一个发送单个，编组，广播信息的简单终结点。开发人员通过使用持久性连接Api，直接访问SignalR公开的底层通信协议。
  
- **Hubs**：Hubs是基于连接Api的更高级别的通信管道，它允许客户端和服务器上彼此直接调用方法，SignalR能够很神奇地处理跨机器的调度，使得客户端和服务器端能够轻松调用在对方端上的方法。使用Hub还允许开发人员将强类型的参数传递给方法并且绑定模型
  

### SignalR 优点

- **实时性**：SignalR 可以让应用程序实现实时通信功能，使应用程序更加响应式和互动式。
  
- **跨平台和跨语言**：SignalR 可以在多种平台和语言之间进行通信，例如，可以使用 JavaScript 客户端与 .NET Core 服务器进行通信。
  
- **简单易用**：SignalR 提供了简单易用的 API，使开发人员可以轻松地实现实时通信功能。
  

### SignalR 具体开发步骤
1. 创建一个 .NET 6 Web 应用程序项目：使用你喜欢的 IDE（例如 Visual Studio 2022、Visual Studio Code 等）创建一个新的 .NET 6 Web 应用程序项目。
2. 添加 SignalR 支持：确保你的项目引用了 Microsoft.AspNetCore.SignalR NuGet 包。你可以在项目文件（例如 .csproj 文件）或通过包管理器控制台运行以下命令来添加引用：

```csharp
dotnet add package Microsoft.AspNetCore.SignalR
```
3. 创建 SignalR Hub 类：创建一个继承自 Hub 类的 SignalR Hub 类。这个类将负责处理客户端和服务器之间的实时通信。

```csharp
using Microsoft.AspNetCore.SignalR;

public class ChatHub : Hub
{
   public async Task SendMessage(string user, string message)
   {
       await Clients.All.SendAsync("ReceiveMessage", user, message);
   }
}
```
5. 配置 SignalR 终结点：在 Startup.cs 文件的 ConfigureServices 方法中，添加 SignalR 服务的配置。

```csharp
services.AddSignalR();
```
7. 配置 SignalR 终结点和路由：在 Startup.cs 文件的 Configure 方法中，使用 UseEndpoints 方法配置 SignalR 终结点和路由。

```csharp
app.UseEndpoints(endpoints =>
{
   endpoints.MapHub<ChatHub>("/chathub");
   endpoints.MapControllers();
   // 其他终结点配置
});
```
9. 在前端代码中使用 SignalR：在你的前端代码中，使用 SignalR JavaScript 客户端库来与 SignalR Hub 进行通信。

```js
<script>
var connection = new signalR.HubConnectionBuilder()
    .withUrl("/chathub")
    .withAutomaticReconnect()
    .configureLogging(signalR.LogLevel.Information)
    .build();

connection.on("ReceiveMessage", function (message) {
    var li = document.createElement("li");
    document.getElementById("messagesRes").appendChild(li);
    li.textContent = `${message}`;
});

connection.onreconnecting((error) => {
    console.log("SignalR reconnecting...", error);
});

connection.onreconnected((connectionId) => {
    console.log("SignalR reconnected with connectionId:", connectionId);
});

function start() {
    connection.start().then(function () {
        console.log("SignalR链接成功");
        document.getElementById("userInput").value = connection.connectionId;
    }).catch((err) => {
        console.error(err.toString());
    });
}

start();

// 发送消息
connection.invoke("SendMessage", user, message)
   .catch(err => {
       // 处理发送消息错误
   });
</script>
```
### 源码地址
> https://github.com/Tim-DCS/SignalR-Demo.git
