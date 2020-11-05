# 深度学习部署概述

## CPU篇

针对CPU平台的深度学习部署优化方法大致可分为三个层级：

- 算法级
- 应用级
- 系统级

每个层级有其对应的性能分析工具，如下表所示：

| 优化层级 | 具体手段     | Profiling Tools                                              |
| -------- | ------------ | ------------------------------------------------------------ |
| 系统级   | 编译器选项   | perf/sar/numactl/iostat/vmstat/blktrace/[VTune](https://software.intel.com/content/www/us/en/develop/tools/vtune-profiler.html) |
| 应用级   | 并发处理     | [VTune](https://software.intel.com/content/www/us/en/develop/tools/vtune-profiler.html)/dtrace/strace/plockstat/lockstat |
| 应用级   | 异步处理     |                                                              |
| 算法级   | 设置超参数   | [TensorBoard](https://www.tensorflow.org/tensorboard?hl=zh-cn)/[Visual DL](https://www.bookstack.cn/read/PaddlePaddle-1.3-fluid/43.md) |
| 算法级   | 网络结构优化 |                                                              |
| 算法级   | 低精度推理   |                                                              |

系统级的优化方法通常与硬软件平台有关，方法包括使用SIMD指令、基于并行计算数学库、硬件厂商提供的深度学习SDK等。

应用级的优化方法主要包括改进应用服务的流水和并发性能。深度学习应用通常既包括推理，也包括前后数据处理以及网络请求响应模块。良好的并发设计可以显著改进服务端端到端的性能。

算法层面则聚焦于深度学习模型本身，通过类似设置超参数、裁剪网络结构、量化等手段减小模型占用空间和计算量，从而加速推理。

# 分类

在对深度学习应用优化之前，我们首先必须确定该应用的类型和性能评价指标以便决定应用优化目标。

从系统资源的角度看，深度学习应用可以分为计算密集型和I/O密集型。例如，基于CNN的图像/视频算法通常具备较大的计算量，所以可以归类为计算密集型。而依赖于大数据的搜索和推荐算法的特征维度比较大并且处理大量数据，所以通常归类为I/O密集型。

从性能的角度看，深度学习应用则可分为强调低时延类型和强调高吞吐量类型。例如，在线应用通常要求极低响应时延，而通常进行批量数据处理的离线应用则要求高吞吐量。

### 参考

https://software.intel.com/content/www/us/en/develop/articles/optimization-practice-of-deep-learning-inference-deployment-on-intel-processors.html