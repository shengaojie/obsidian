
# 项目


👍😍
https://github.com/networknt/light-4j


👍😍
https://github.com/search?q=repo%3Aneo4j%2Fneo4j+invokeall&type=code&p=2

👍😍
https://github.com/dusenberrymw/systemml

👍😍
https://github.com/search?q=repo%3Ahsaputra%2Fsystemml%20invokeall&type=code


👍😍
https://github.com/ThoughtFlow/ModernJava




https://github.com/search?q=repo%3Atrackmate-sc%2FTrackMate%20invokeall&type=code

实验结果：

> [!NOTE] sysmtemml

![[CleanShot 2023-12-06 at 10.24.47@2x.png]]
SpoofRowwise   2                                    同一个方法中有多个invokeall
FrameReaderTextCSVParallel   1            同一个方法中有多个invokeall
MatrixReader  1                                        pool是方法传入的，可能是自定义线程池
LibMatrixMult     2                                    没有get方法
LibMatrixDNN  1                                       没有task任务                                          解决
LibMatrixReorg   1                                    同一个方法中有多个invokeall
LibMatrixAgg 2                                         没有get方法
48 
38

> [!NOTE] astor

![[CleanShot 2023-12-06 at 10.28.11@2x.png]]
10   6

> [!NOTE] metaOmGraph

![[CleanShot 2023-12-06 at 10.30.34@2x.png]]
10   7
三个invokeAll在同一个方法中

> [!NOTE] light-4j

![[CleanShot 2023-12-06 at 10.32.02@2x.png]]
![[CleanShot 2023-12-06 at 10.32.59@2x.png]]
10
10




不能重构的场景
https://github.com/urmi-21/MetaOmGraph/blob/2a3503d764d8361bed1266b88f38961bc1d2353d/src/edu/iastate/metnet/metaomgraph/ComputeRunsSimilarity.java#L62

不能重构的原因：
1. 使用的自定义的线程池
2. 构建线程池带有了ThreadFactory参数
3. 静态分析的原因
4. 使用了ExecutorService中除了shutdown，shutdownNow之外的方法


20个任务
![[CleanShot 2023-12-28 at 15.11.04@2x.png]]

50个任务
![[CleanShot 2023-12-28 at 15.13.05@2x.png]]

100个任务
![[CleanShot 2023-12-28 at 15.14.35@2x.png]]

200个任务
![[CleanShot 2023-12-28 at 15.18.34@2x.png|575]]

400个任务
![[CleanShot 2023-12-28 at 15.20.29@2x.png|625]]

1000个任务
![[CleanShot 2023-12-28 at 15.22.47@2x.png]]


![[CleanShot 2023-12-28 at 16.33.23@2x.png]]

![[CleanShot 2024-01-15 at 15.49.56@2x.png]]


项目：trackmate
![[CleanShot 2024-01-15 at 16.38.53@2x.png]]

项目：light-4j
![[CleanShot 2024-01-15 at 21.08.15@2x.png]]


codejam
![[CleanShot 2024-03-05 at 10.01.44@2x.png]]
![[CleanShot 2024-03-05 at 10.14.47@2x.png]]

mylocalTon
![[CleanShot 2024-03-05 at 10.34.06@2x.png]]

![[CleanShot 2024-01-16 at 09.26.20@2x 1.png]]
* 可以看出对于计算型任务，其实三者之间的差距不是很大，但是结构化并发还是有所提升的
	* 但是对于io型任务，结构化并发的提升效果较为明显