💡**本章教程主要针对JMeter在windows 环境下进行api服务的压力测试**
### 使用CSV文件模拟请求参数
在上一篇文章中提到了模拟多用户请求时需要用到多个用户信息参数，在用户数量不会很多的情况下使用 User Parameters 确实方便我们的测试
。 但如果遇到需要几十上百个不同参数时，使用 User Parameters 则会让我们配置参数的效率低下，这时候我们就需要用到通过读取文件的方式进行请求参数的设置。
#### 创建 CSV 文件
首先我们需要创建一个文件编码为utf-8的csv文件，然后在csv文件中设置好我们需要的参数。其中每一列对应一个字段，每一行则代表一份参数信息。

📌**注意：第一行可以这是表头也可以不设置表头，因为每一列字段的参数是在JMeter中定义的。**

![image](https://github.com/user-attachments/assets/b37929a0-1025-4b2b-b96c-e474832e2aa5)

#### 添加 CSV Data Set Config
选择对应的Request 右击选择 Add —> Config Element —> csv data set config

使用了csv data set config设置参数，可以将 User Parameters 删除掉(避免参数干扰)

![image](https://github.com/user-attachments/assets/a4b981b6-ecab-4ad8-b007-02269690fb54)

![image](https://github.com/user-attachments/assets/48a3687e-cd5e-44fd-b4ef-8cb1d13f734a)



