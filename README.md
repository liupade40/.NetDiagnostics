# .NetDocument

记录.Net的学习笔记

## .Net相关源码
.Net 运行时源码：https://source.dot.net 、 https://github.com/dotnet/runtime

asp.netcore 源码：https://github.com/dotnet/aspnetcore

.NET compiler 源码:https://github.com/dotnet/roslyn

## .Net 官方诊断程序相关文章

操作流程： https://learn.microsoft.com/zh-cn/dotnet/core/diagnostics/debug-memory-leak
示例包含了：

内存泄漏：针对内存泄漏我自己碰到的情况要么非托管资源未释放，没有使用Dispose，常见的数据库连接，Redis连接这些，其实这些连接，服务可以查看到客户端连接数，如果连接数一直在增加那就说明连接没有释放；要么就是定义的全局静态字段，比如是一个字典或者列表可以不断增加，随着使用时间的增加，占用内存越来越多。

高CPU：

死锁：

堆栈溢出：

对应的源码： https://github.com/dotnet/samples/tree/6c5ab81742af4729c5bc2c8d9c91d4eed781e58f/core/diagnostics/DiagnosticScenarios

## .Net 和 容器 简介
https://learn.microsoft.com/zh-cn/dotnet/core/docker/introduction

## .Net和AI
模型生成器是通过VS界面操作训练数据，生成模型生成预测的代码

ML.NET API是通过代码训练数据、生成模型、预测

模型生成器介绍：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/automate-training-with-model-builder

ML.NET API介绍：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/how-does-mldotnet-work

模型生成器案例：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/tutorials/predict-prices-with-model-builder

ML.NET API案例：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/tutorials/sentiment-analysis

Open Neural Network Exchange（ONNX，开放神经网络交换）是AI模型的开放源代码格式，ONNX 支持框架之间的互操作性

介绍ML.NET如何使用ONNX模型：https://learn.microsoft.com/zh-cn/azure/machine-learning/how-to-use-automl-onnx-model-dotnet?view=azureml-api-2

介绍ML.NET如何使用YOLOv2的ONNX模型：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/tutorials/object-detection-onnx

ML.NET如何导出ONNX模型：https://learn.microsoft.com/zh-cn/dotnet/machine-learning/how-to-guides/save-load-machine-learning-models-ml-net#load-a-model-stored-locally

![image](https://github.com/liupade40/.NetDocument/assets/32723645/d0750477-5748-4ba2-a48d-7c683f13a8ec)
上图是通过机器学习框架训练AI模型，训练完以后导出ONNX模型，ML.NET可以使用ONNX模型

## .Net使用GRPC
https://learn.microsoft.com/zh-cn/aspnet/core/grpc

## Asp.net core
Web服务器Kestrel、HTTP.sys、IIS：https://learn.microsoft.com/zh-cn/aspnet/core/fundamentals/servers

部署在linux服务器+nginx反向代理+systemd服务管理：https://learn.microsoft.com/zh-cn/aspnet/core/host-and-deploy/linux-nginx

## C#/C++
C#调用C++： https://www.cnblogs.com/skyfreedom/p/11773597.html

