💡本章教程主要针对JMeter在windows 环境下进行api服务的压力测试
## 1. Summary Report（摘要报告）
- 概述: Summary Report 是一种简洁的报告形式，提供测试的总体性能数据。
- 主要指标:
  - **Label**: 请求的名称或类别。
  - **Samples**: 请求的总次数（样本数量）。
  - **Average**: 每个请求的平均响应时间。
  - **Min**: 最小响应时间。
  - **Max**: 最大响应时间。
  - **Error %**: 错误率，即请求失败的百分比。
  - **Throughput**: 吞吐量，表示每秒处理的请求数量（Requests per second）。
  - **KB/sec**: 每秒传输的千字节数。
- 适用场景: 当你需要快速查看测试的概要信息时，Summary Report 是个不错的选择。

## 2. Aggregate Report（汇总报告）
- 概述: Aggregate Report 提供了更详细的汇总数据，并对所有请求进行分组和汇总，类似于 Summary Report 但数据维度更多。
- 主要指标:
  - **Label**: 请求的名称。
  - **Samples**: 样本数量。
  - **Average**: 平均响应时间。
  - **Min**: 最小响应时间。
  - **Max**: 最大响应时间。
  - **90% Line**: 90% 分位线，即 90% 请求的响应时间低于该值。
  - **Median**: 中位数。
  - **Error %**: 错误率。
  - **Throughput**: 吞吐量（Requests per second）。
  - **Received KB/sec**: 每秒接收的千字节数。
  - **Sent KB/sec**: 每秒发送的千字节数。
- 适用场景: Aggregate Report 适合在需要更全面、细化的性能分析时使用，尤其是关注分位线（如 90% Line）和吞吐量等高级指标。

## 3. View Results in Table（表格形式查看结果）
- 概述: 这个监听器以表格的形式展示每个请求的详细信息，通常用于调试和分析具体请求的响应。
- 主要指标:
  - **Sample #**: 每个请求的编号。
  - **Start Time**: 请求开始的时间。
  - **hread Name**: 执行请求的线程组名称。
  - **Label**: 请求的标签或名称。
  - **Sample Time (ms)**: 请求的响应时间（以毫秒为单位）。
  - **Status**: 请求的状态，显示是否成功（Success）或失败（Fail）。
  - **Bytes**: 响应中传输的数据字节数。
  - **Latency**: 等待时间（从发出请求到接收到第一个字节的时间）。
  - **Connect Time**: 建立连接的时间。
  - **Error Message**: 如果请求失败，显示对应的错误信息。
- 适用场景：可以详细查看每个请求的响应时间、状态和错误信息，便于调试和定位问题。适合在测试过程中监控和记录某些特定请求的执行情况，帮助发现响应较慢或失败的请求。

## 4. 报告添加方式
- 针对每个线程组查看结果报告，可在每个线程组右击选择 Add -> Listener -> Summary Report / Aggregate Report / View Results in Table 。
- 同时也可以添加全局报告，查看所有线程组的结果报告，在JMeter 测试计划右击选择 Add -> Listener -> Summary Report / Aggregate Report / View Results in Table 。

![image](https://github.com/user-attachments/assets/4b172037-265d-4074-9a5c-82c6db18b6c8)

## 5. 生成HTML 测试结果报告
- 按照4 步骤在测试计划中添加 View Results in Table。
- 在 View Results in Table 界面设置将结果写入csv文件 (直接写好文件路径，如果csv文件不存在，运行JMeter会自动生成csv文件)。
- 在JMeter 界面中找到Tools，点击后选择 Generate HTML report 。
- Generate HTML report 弹出框中 (1)选中生成的csv文件、 (2) 选择JMeter安装文件夹bin中的jmeter.properties、 (3) 选择一个空文件夹，然后点击Generate report。
- 最后可以在设置的空文件夹中看到生成的报告文件，直接打开 html文件即可查看html报告。

![image](https://github.com/user-attachments/assets/23dddc75-b31b-477d-af39-5ae87ff8ff08)

![image](https://github.com/user-attachments/assets/3ee40b18-631c-4482-8b08-c34ed8457391)

![image](https://github.com/user-attachments/assets/987d7c23-bd34-4575-8c4e-b7648b97a372)




