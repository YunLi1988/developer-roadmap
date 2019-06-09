# 系统底层知识

- [Linux系统、内存和网络](#linux系统内存和网络)
  - [Linux 系统相关](#linux-系统相关)
  - [内存相关](#内存相关)
  - [计算机网络](#计算机网络)
    - [网络学习](#网络学习)
    - [网络调优](#网络调优)
    - [网络协议](#网络协议)
- [异步I/O模型和Lock-Free编程](#异步io模型和lock-free编程)
  - [异步 I/O 模型](#异步-io-模型)
  - [Lock-Free 编程相关](#lock-free-编程相关)
- [Java 底层知识](#java-底层知识)
  - [Java 字节码相关](#java-字节码相关)
  - [JVM 相关](#jvm-相关)

## Linux系统、内存和网络

### Linux 系统相关

- [Red Hat Enterprise Linux 文档](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/?version=7) 。Red Hat Enterprise Linux（RHEL）是老牌 Linux 厂商 Red Hat 出品的面向商业的 Linux 发行版。
- [Linux Insides](https://github.com/0xAX/linux-insides) ，GitHub 上的一个开源电子书，其中讲述了 Linux 内核是怎样启动、初始化以及进行管理的。
- [LWN’s kernel page](http://lwn.net/Kernel/Index/) ，上面有很多非常不错的文章来解释 Linux 内核的一些东西。
- [Learn Linux Kernel from Android Perspective](http://learnlinuxconcepts.blogspot.com/2014/10/this-blog-is-to-help-those-students-and.html) ，从 Android 的角度来学习 Linux 内核，这个站点上的 Blog 相对于前面的比较简单易读一些。
- [Linux Kernel Doc](https://www.kernel.org/doc/)， Linux 的内核文档也可以浏览一下。
- [Kernel Planet](http://planet.kernel.org/) ，Linux 内核开发者的 Blog，有很多很不错的文章和想法。
- [Linux Performance and Tuning Guidelines](https://lenovopress.com/redp4285.pdf) ，这是 IBM 出的红皮书，虽然有点老了，但还是非常值得一读的。
- [TLK: The Linux Kernel](http://tldp.org/LDP/tlk/tlk.html) ，这是一本相对比较老的书了，Linux 内核版本为 2.0.33，但了解一下前人的思路，也是很有帮助的。
- [Linux Performance](http://www.brendangregg.com/linuxperf.html) ，这个网站上提供了和 Linux 系统性能相关的各种工具和文章收集，非常不错。
- [Optimizing web servers for high throughput and low latency](https://blogs.dropbox.com/tech/2017/09/optimizing-web-servers-for-high-throughput-and-low-latency/) ，这是一篇非常底层的系统调优的文章，来自 DropBox，从中你可以学到很多底层的性能调优的经验和知识。

### 内存相关

- [What every programmer should know about memory](http://futuretech.blinkenlights.nl/misc/cpumemory.pdf)。
  - [Part 1: Introduction](https://lwn.net/Articles/250967/) ，中译版为 “[每个程序员都应该了解的内存知识【第一部分】](https://www.oschina.net/translate/what-every-programmer-should-know-about-memory-part1)”
  - [Part 2: CPU caches](https://lwn.net/Articles/252125/)
  - [Part 3 (Virtual memory)](http://lwn.net/Articles/253361/)
  - [Part 4 (NUMA systems)](http://lwn.net/Articles/254445/)
  - [Part 5 (What programmers can do - cache optimization)](http://lwn.net/Articles/255364/)
  - [Part 6 (What programmers can do - multi-threaded optimizations)](http://lwn.net/Articles/256433/)
  - [Part 7 (Memory performance tools)](http://lwn.net/Articles/257209/)
  - [Part 8 (Future technologies)](https://lwn.net/Articles/258154/)
  - [Part 9 (Appendices and bibliography)](https://lwn.net/Articles/258188/)
- 和内存相关的论文。
  - [Memory Barriers: a Hardware View for Software Hackers](http://irl.cs.ucla.edu/~yingdi/web/paperreading/whymb.2010.06.07c.pdf)。
  - [A Tutorial Introduction to the ARM and POWER Relaxed Memory Models](http://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf)。
  - [x86-TSO: A Rigorous and Usable Programmer’s Model for x86 Multiprocessors](http://www.cl.cam.ac.uk/~pes20/weakmemory/cacm.pdf)。
- 内存管理的 lib 库。
  - [ptmalloc](http://www.malloc.de/en/) 是 glibc 的内存分配管理。
  - [tcmalloc](https://github.com/gperftools/gperftools) 是 Google 的内存分配管理模块，全称是 Thread-Caching malloc，基本上来说比 glibc 的 ptmalloc 快两倍以上。
  - [jemalloc](http://jemalloc.net/) 是 BSD 提供的内存分配管理。其论文为 [A Scalable Concurrent malloc(3) Implementation for FreeBSD](https://people.freebsd.org/~jasone/jemalloc/bsdcan2006/jemalloc.pdf)，这是一个可以并行处理的内存分配管理器。
  - [C Dynamic Memory Allocation](https://en.wikipedia.org/wiki/C_dynamic_memory_allocation#Thread-caching_malloc_(tcmalloc))。
  - [ptmalloc，tcmalloc 和 jemalloc 内存分配策略研究](https://owent.net/2013/867.html)
  - [内存优化总结：ptmalloc、tcmalloc 和 jemalloc](http://www.cnhalo.net/2016/06/13/memory-optimize/)
  - [Scalable memory allocation using jemalloc](https://www.facebook.com/notes/facebook-engineering/scalable-memory-allocation-using-jemalloc/480222803919)
  - [Decreasing RAM Usage by 40% Using jemalloc with Python & Celery](https://zapier.com/engineering/celery-python-jemalloc/)

### 计算机网络

#### 网络学习

- 《[计算机网络（第五版）](https://book.douban.com/subject/10510747/)》，这本“计算机网络”和前面推荐的那本计算机网络不一样，前面那本偏扫盲，这本中有很多细节。这本书是国内外使用最广泛、最权威的计算机网络经典教材。全书按照网络协议模型自下而上（物理层、数据链路层、介质访问控制层、网络层、传输层和应用层）有系统地介绍了计算机网络的基本原理，并结合 Internet 给出了大量的协议实例。

#### 网络调优

- [Linux Advanced Routing & Traffic Control HOWTO](http://lartc.org/)，这是一个非常容易上手的关于 iproute2、流量整形和一点 netfilter 的指南。
- [Red Hat Enterprise Linux Network Performance Tuning Guide](https://access.redhat.com/sites/default/files/attachments/20150325_network_performance_tuning.pdf)。
- [Awesome Pcap Tools](https://github.com/caesar0301/awesome-pcaptools) ，其中罗列了各种网络工具，能够让你更从容地调试网络相关的程序。
- [Making Linux TCP Fast](https://netdevconf.org/1.2/papers/bbr-netdev-1.2.new.new.pdf) ，一篇非常不错的 TCP 调优的论文。

#### 网络协议

- 对于第 2 层链路层，你可能需要了解一下 ARP：
  - [RFC 826 - An Ethernet Address Resolution Protocol](https://tools.ietf.org/html/rfc826)

- Tunnel 相关的协议
  - [RFC 1853 - IP in IP Tunneling](https://tools.ietf.org/html/rfc1853)
  - [RFC 2784 - Generic Routing Encapsulation (GRE)](https://tools.ietf.org/html/rfc2784)
  - [RFC 2661 - Layer Two Tunneling Protocol “L2TP”](https://tools.ietf.org/html/rfc2661)
  - [RFC 2637 - Point-to-Point Tunneling Protocol (PPTP)](https://tools.ietf.org/html/rfc2637)

- 对于第 4 层，你最需要了解的是 TCP/IP 了。
  - [RFC 793 - Transmission Control Protocol](https://tools.ietf.org/html/rfc793) - 最初的 TCP 标准定义，但不包括 TCP 相关细节。
  - [RFC 813 - Window and Acknowledgement Strategy in TCP](https://tools.ietf.org/html/rfc813) - TCP 窗口与确认策略，并讨论了在使用该机制时可能遇到的问题及解决方法。
  - [RFC 879 - The TCP Maximum Segment Size and Related Topics](https://tools.ietf.org/html/rfc879) - 讨论 MSS 参数对控制 TCP 分组大小的重要性，以及该参数与 IP 分段大小的关系等。
  - [RFC 896 - Congestion Control in IP/TCP Internetworks](https://tools.ietf.org/html/rfc896) - 讨论拥塞问题和 TCP 如何控制拥塞。

  - [RFC 2581 - TCP Congestion Control](https://tools.ietf.org/html/rfc2581) - 描述用于拥塞控制的四种机制：慢启动、拥塞防御、快重传和快恢复。后面这个 RFC 被 [RFC 5681](https://tools.ietf.org/html/rfc5681) 所更新。还有 [RFC 6582 - The NewReno Modification to TCP’s Fast Recovery Algorithm](https://tools.ietf.org/html/rfc6582) 中一个改进的快速恢复算法。
  - [RFC 2018 - TCP Selective Acknowledgment Options](https://tools.ietf.org/html/rfc2018) - TCP 的选择确认。
  - [RFC 2883 - An Extension to the Selective Acknowledgement (SACK) Option for TCP](https://tools.ietf.org/html/rfc2883) - 对于 RFC 2018 的改进。
  - [RFC 2988 - Computing TCP’s Retransmission Timer](https://tools.ietf.org/html/rfc2988) - 讨论与 TCP 重传计时器设置相关的话题，重传计时器控制报文在重传前应等待多长时间。也就是经典的 TCP Karn/Partridge 重传算法。
  - [RFC 6298 - Computing TCP’s Retransmission Timer](https://tools.ietf.org/html/rfc6298) - TCP Jacobson/Karels Algorithm 重传算法。
  - 关于 Linux 下的 TCP 参数，你需要仔仔细细地读一下[TCP 的 man page](http://man7.org/linux/man-pages/man7/tcp.7.html) 。

- 对于第 7 层协议，HTTP 协议是重点要学习的
  - 《[HTTP 权威指南](https://book.douban.com/subject/10746113/) 》，这本书有点厚，可以当参考书来看。这本书中没有提到 HTTP/2 的事，但是可以让你了解到 HTTP 协议的绝大多数特性。
  - 关于[HTTP/2](https://en.wikipedia.org/wiki/HTTP/2)
    - [Gitbook - HTTP/2 详解](https://legacy.gitbook.com/book/ye11ow/http2-explained/details)
    - [http2 explained](http://daniel.haxx.se/http2/)（[中译版](https://www.gitbook.com/book/ye11ow/http2-explained/details)）
    - [HTTP/2 for a Faster Web](https://cascadingmedia.com/insites/2015/03/http-2.html)
    - [Nginx HTTP/2 白皮书](https://www.nginx.com/wp-content/uploads/2015/09/NGINX_HTTP2_White_Paper_v4.pdf)

## 异步I/O模型和Lock-Free编程

### 异步 I/O 模型

基本上来说，异步 I/O 模型的发展技术是： select -> poll -> epoll -> aio -> libevent -> libuv。

- Java 相关的 I/O 模型
  - [Thousands of Threads and Blocking I/O: The Old Way to Write Java Servers Is New Again (and Way Better)](https://www.slideshare.net/e456/tyma-paulmultithreaded1) ，这个 PPT 中不仅回顾和比较了各种 I/O 模型，而且还有各种比较细节的方案和说明，是一篇非常不错的文章。
  - Java 相关的 PPT - 道格·莱亚（Doug Lea）的 [Scalable IO in Java](http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf)，这样你会对一些概念有个了解。

- 各种异步 I/O 的实现和设计方式
  - [IBM - Boost application performance using asynchronous I/O](https://www.ibm.com/developerworks/library/l-async/) ，这是一篇关于 AIO 的文章。
  - [Lazy Asynchronous I/O For Event-Driven Servers](https://www.usenix.org/legacy/event/usenix04/tech/general/full_papers/elmeleegy/elmeleegy_html/html.html) ，这篇文章也很不错。
  - 异步 I/O 模型中的 [Windows I/O Completion Ports](https://docs.microsoft.com/en-us/windows/desktop/FileIO/i-o-completion-ports) , 你也需要了解一下。如果 MSDN 上的这个手册不容易读，你可以看看这篇文章 [Inside I/O Completion Ports](http://sysinternals.d4rk4.ru/Information/IoCompletionPorts.html)。另外，关于 Windows，[Windows Internals](https://book.douban.com/subject/6935552/) 这本书你可以仔细读一下，非常不错的。其中有一节 I/O Processing 也是很不错的，这里我给一个网上免费的链接[I/O Processing](https://flylib.com/books/en/4.491.1.85/1/) 你可以看看 Windows 是怎么玩的。
  - Libevent。你可以看一下其主要维护人员尼克·马修森（Nick Mathewson）写的 [Libevent 2.0 book](http://www.wangafu.net/~nickm/libevent-book/)。还有一本国人写的电子书 《[Libevent 深入浅出](https://aceld.gitbooks.io/libevent/content/)》。
  - Libuv。你可以看一下其官网的 [Libuv Design Overview](http://docs.libuv.org/en/v1.x/design.html) 了解一下。

- Reactor 模式
  - [Understanding Reactor Pattern: Thread-Based and Event-Driven](https://dzone.com/articles/understanding-reactor-pattern-thread-based-and-eve)
  - [Reactor Pattern](https://www.dre.vanderbilt.edu/~schmidt/PDF/Reactor2-93.pdf)
  - [The reactor pattern and non-blocking IO](https://www.celum.com/en/blog/technology/the-reactor-pattern-and-non-blocking-io)

### Lock-Free 编程相关

- 关于无锁的数据结构
  - [Dr.Dobb’s: Lock-Free Data Structures](http://www.drdobbs.com/lock-free-data-structures/184401865)
  - [Andrei Alexandrescu: Lock-Free Data Structures](https://erdani.com/publications/cuj-2004-10.pdf)

- 并行编程
  - [Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://www.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html) ，这是大牛 [保罗·麦肯尼（Paul E. McKenney）](https://www.linkedin.com/in/paulmckenney/) 写的书。
  - 并发编程中的一些概念：[Non-blocking algorithm](https://en.wikipedia.org/wiki/Non-blocking_algorithm) 、[Read-copy-update](https://en.wikipedia.org/wiki/Read-copy-update) 和 [Seqlock](https://en.wikipedia.org/wiki/Seqlock)。

- 论文
  - [Implementing Lock-Free Queues](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.53.8674&rep=rep1&type=pdf)， 这也是一篇很不错的论文，我把它介绍在了我的网站上 ，文章为“[无锁队列的实现](https://coolshell.cn/articles/8239.html)”。
  - [Simple, Fast, and Practical Non-Blocking and Blocking Concurrent Queue Algorithms](http://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf) ，这篇论文给出了一个无阻塞和阻塞的并发队列算法。

- 博客
  - [1024cores](http://www.1024cores.net/) - 德米特里·伐由科夫（Dmitry Vyukov）的和 lock-free 编程相关的网站。
  - [Paul E. McKenney](http://paulmck.livejournal.com/) - 保罗（Paul）的个人网站。
  - [Concurrency Freaks](http://concurrencyfreaks.blogspot.com/) - 关于并发算法和相关模式的网站。
  - [Preshing on Programming](http://preshing.com/) - 加拿大程序员杰夫·普莱辛（Jeff Preshing）的技术博客，主要关注 C++ 和 Python 两门编程语言。他用 C++11 实现了类的反射机制，用 C++ 编写了 3D 小游戏 Hop Out，还为该游戏编写了一个游戏引擎。他还讨论了很多 C++ 的用法，比如 C++14 推荐的代码写法、新增的某些语言构造等，和 Python 很相似。阅读这个技术博客上的内容能够深深感受到博主对编程世界的崇敬和痴迷。
  - [Sutter’s Mill](http://herbsutter.com/) - 赫布·萨特（Herb Sutter）是一位杰出的 C++ 专家，曾担任 ISO C++ 标准委员会秘书和召集人超过 10 年。他的博客有关于 C++ 语言标准最新进展的信息，其中也有他的演讲视频。博客中还讨论了其他技术和 C++ 的差异，如 C# 和 JavaScript，它们的性能特点、怎样避免引入性能方面的缺陷等。
  - [Mechanical Sympathy](http://mechanical-sympathy.blogspot.com/) - 博主是马丁·汤普森（Martin Thompson），他是一名英国的技术极客，探索现代硬件的功能，并提供开发、培训、性能调优和咨询服务。他的博客主题是 Hardware and software working together in harmony，里面探讨了如何设计和编写软件使得它在硬件上能高性能地运行。非常值得一看。

- C/C++ 的类库
  - [Boost.Lockfree](http://www.boost.org/doc/libs/1_60_0/doc/html/lockfree.html) - Boost 库中的无锁数据结构。
  - [ConcurrencyKit](https://github.com/concurrencykit/ck) - 并发性编程的原语。
  - [Folly](https://github.com/facebook/folly) - Facebook 的开源库（它对 MPMC 队列做了一个很好的实现）。
  - [Junction](https://github.com/preshing/junction) - C++ 中的并发数据结构。
  - [MPMCQueue](https://github.com/rigtorp/MPMCQueue) - 一个用 C++11 编写的有边界的“多生产者 - 多消费者”无锁队列。
  - [SPSCQueue](https://github.com/rigtorp/SPSCQueue) - 一个有边界的“单生产者 - 单消费者”的无等待、无锁的队列。
  - [Seqlock](https://github.com/rigtorp/Seqlock) - 用 C++ 实现的 Seqlock。
  - [Userspace RCU](http://liburcu.org/) - liburcu 是一个用户空间的 RCU（Read-copy-update，读 - 拷贝 - 更新）库。
  - [libcds](https://github.com/khizmax/libcds) - 一个并发数据结构的 C++ 库。
  - [liblfds](https://liblfds.org/) - 一个用 C 语言编写的可移植、无许可证、无锁的数据结构库。

## Java 底层知识

### Java 字节码相关

- [Java Zone: Introduction to Java Bytecode](https://dzone.com/articles/introduction-to-java-bytecode) ，这篇文章图文并茂地向你讲述了 Java 字节码的一些细节，是一篇很不错的入门文章。
- [IBM DeveloperWorks: Java bytecode](https://www.ibm.com/developerworks/library/it-haggar_bytecode/index.html) ，虽然这篇文章很老了，但是这篇文章是一篇非常好的讲 Java 字节码的文章。
- [Java Bytecode and JVMTI Examples](https://github.com/jon-bell/bytecode-examples)，这是一些使用 [JVM Tool Interface](http://docs.oracle.com/javase/7/docs/platform/jvmti/jvmti.html) 操作字节码的比较实用的例子。包括方法调用统计、静态字节码修改、Heap Taggin 和 Heap Walking。

当然，一般来说，我们不使用 JVMTI 操作字节码，而是用一些更好用的库。这里有三个库可以帮你比较容易地做这个事。

- [asmtools](https://wiki.openjdk.java.net/display/CodeTools/asmtools) - 用于生产环境的 Java .class 文件开发工具。
- [Byte Buddy](http://bytebuddy.net/) - 代码生成库：运行时创建 Class 文件而不需要编译器帮助。
- [Jitescript](https://github.com/qmx/jitescript) - 和 [BiteScript](https://github.com/headius/bitescript) 类似的字节码生成库。

就我而言，我更喜欢 Byte Buddy，它在 2015 年还获了 Oracle 的 “[Duke’s Choice](https://www.oracle.com/corporate/pressrelease/dukes-award-102815.html)”大奖，其中说 Byte Buddy 极大地发展了 Java 的技术。

使用字节码编程可以玩出很多高级玩法，最高级的还是在 Java 程序运行时进行字节码修改和代码注入。听起来是不是一些很黑客，也很黑科技的事？是的，这个方式使用 Java 这门静态语言在运行时可以进行各种动态的代码修改，而且可以进行无侵入的编程。

要做到这个事，你还需要学习一个叫 Java Agent 的技术。Java Agent 使用的是 “[Java Instrumentation API](https://stackoverflow.com/questions/11898566/tutorials-about-javaagents)”，其主要方法是实现一个叫 premain() 的方法（嗯，一个比 main() 函数还要超前执行的 main 函数），然后把你的代码编译成一个 jar 文件。

在 JVM 启动时，使用这样的命令行来引入你的 jar 文件：java -javaagent:yourAwesomeAgent.jar -jar App.jar。更为详细的文章你可以参看：“[Java Code Geeks: Java Agents](https://www.javacodegeeks.com/2015/09/java-agents.html)”，你还可以看一下这个示例项目：[jvm-monitoring-agent](https://github.com/toptal/jvm-monitoring-agent) 或是 [EntryPointKR/Agent.java](https://gist.github.com/EntryPointKR/152f089f6f3884047abcd19d39297c9e)。如果想用 ByteBuddy 来玩，你可以看看这篇文章 “[通过使用 Byte Buddy，便捷地创建 Java Agent](http://www.infoq.com/cn/articles/Easily-Create-Java-Agents-with-ByteBuddy)”。如果你想学习如何用 Java Agent 做监控，你可以看一下这个项目 [Stage Monitor](http://www.stagemonitor.org/)。

### JVM 相关

- [The Java Virtual Machine Specification Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/jvms8.pdf) 。对于规格说明书的阅读，我认为是系统了解 JVM 规范的最佳文档，这个文档可以让你对于搞不清楚或是诡异的问题恍然大悟。关于中文翻译，有人在 GitHub 上开了个 Repo - “[java-virtual-machine-specification](https://github.com/waylau/java-virtual-machine-specification)”。
- [JVM Anatomy Park](https://shipilev.net/jvm-anatomy-park/) JVM 解剖公园，这是一个系列的文章，每篇文章都不长，但是都很精彩，带你一点一点地把 JVM 中的一些技术解开。
- [JSR 133](http://www.jcp.org/en/jsr/detail?id=133)。还有马里兰大学的威廉·皮尤（William Pugh）教授收集的和 Java 内存模型相关的文献 - [The Java Memory Model](http://www.cs.umd.edu/~pugh/java/memoryModel/) ，你可以前往浏览。
- 《[The Garbage Collection Handbook](https://book.douban.com/subject/6809987/)》。
- [Garbage Collection Tuning Guide](http://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/) ，它是 Hotspot Java 虚拟机的垃圾回收调优指南，对你很有帮助。
