💡本章教程主要针对JMeter在windows 环境下进行api服务的压力测试
### 使用正则表达式提取器
- 首先将Login 线程组设置好登录信息（账号,密码）。
- 在JMeter Login Request 中加入 View Results Tree 用于查看响应结果信息。
- 在JMeter Login Request 中加入 Regular Expression Extractor 用于通过正则表达式匹配登录后的标识（Token / SessionId）。
- 在JMeter Login Request 中加入 BeanShell PostProcessor 用于将正则表达式匹配到的信息保存到全局属性中。
- 在后面需要使用到SessionId的地方使用 BeanShell PostProcessor 中设置的属性名。 例： ${sessionid}

![image](https://github.com/user-attachments/assets/a6c9e697-bbed-44a9-97e0-04db93b83ab0)

![image](https://github.com/user-attachments/assets/ef351195-2051-4eff-9703-7a58169972a5)

![image](https://github.com/user-attachments/assets/90c488b5-0075-4e4d-899d-21eddcaa0c1a)

![image](https://github.com/user-attachments/assets/22295c9a-b862-46b7-afca-d3f3d0893840)

### 使用Json 提取器
- 首先将Login 线程组设置好登录信息（账号,密码）。
- 在JMeter Login Request 中加入 View Results Tree 用于查看响应结果信息。
- 在JMeter Login Request 中加入 Json Extractor 用于通过正则表达式匹配登录后的标识（Token / SessionId）。
- 在JMeter Login Request 中加入 BeanShell PostProcessor 用于将正则表达式匹配到的信息保存到全局属性中。
- 在后面需要使用到 Token 的地方使用 BeanShell PostProcessor 中设置的属性名。 例： ${token}

![image](https://github.com/user-attachments/assets/ca9f4a3a-bf19-4f7f-9678-2f9a16ed979a)

![image](https://github.com/user-attachments/assets/394b6fc8-83cd-4db6-9241-6f527f9fbf92)

![image](https://github.com/user-attachments/assets/3dfb4670-d255-4db8-b66d-619bcf9f5776)

![image](https://github.com/user-attachments/assets/02efd1f7-e48f-42e6-892d-1f672557e600)

### 使用Debug Sampler 查看全局属性信息
- 在线程组中加入 Debug Sampler 工具。
- 设置Debug Sampler 可以展示的属性、变量或系统属性。
- 在Debug Sampler 中加入 View Results Tree 用于查看响应结果信息。

![image](https://github.com/user-attachments/assets/cc252f8c-5eec-4095-805e-6e92d22e1c9e)

![image](https://github.com/user-attachments/assets/92412c16-e9ee-49af-8423-9958dde97eb9)

![image](https://github.com/user-attachments/assets/63f09887-d0ea-4328-8e56-ec5bd8c8d842)
