# 系统底层知识

## Linux系统、内存和网络

### Linux 系统相关

学习 Linux 操作系统的原理是通向系统工程师的必经之路。我觉得，Unix/Linux 操作系统里的东西并不难学。你千万不要一下子扎到源代码里去，那样没用——你还是要在上层先通过读一些不错的文档来学习。下面我罗列了一些很不错的站点，其中有很多内容供你去钻研和探索。

我在这里默认你前面已经读过并读懂了我推荐的那些和 Unix/Linux 相关的图书了。所以，我相信你对 Unix/Linux 下的编程已经是有一些基础了，因此，你继续深挖 Linux 下的这些知识应该也不是很难的事了。

- [Red Hat Enterprise Linux 文档](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/?version=7) 。Red Hat Enterprise Linux（RHEL）是老牌 Linux 厂商 Red Hat 出品的面向商业的 Linux 发行版。Red Hat 网站上的这个文档中有很多很有价值的内容，值得一看。
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

计算机内存管理是每一个底层程序员需要了解的非常重要的事儿。当然，这里我们重点还是 Linux 操作系统相关的内存管理上的知识。

首先，LWN.net 上有一系列的 “What every programmer should know about memory” 文章你需要读一下。当然，你可以直接访问一个完整的 [PDF 文档](http://futuretech.blinkenlights.nl/misc/cpumemory.pdf)。下面是这个系列文章的网页版列表。读完这个列表的内容，你基本上就对内存有了一个比较好的知识体系了。

- [Part 1: Introduction](https://lwn.net/Articles/250967/) ，中译版为 “[每个程序员都应该了解的内存知识【第一部分】](https://www.oschina.net/translate/what-every-programmer-should-know-about-memory-part1)”
- [Part 2: CPU caches](https://lwn.net/Articles/252125/)
- [Part 3 (Virtual memory)](http://lwn.net/Articles/253361/)
- [Part 4 (NUMA systems)](http://lwn.net/Articles/254445/)
- [Part 5 (What programmers can do - cache optimization)](http://lwn.net/Articles/255364/)
- [Part 6 (What programmers can do - multi-threaded optimizations)](http://lwn.net/Articles/256433/)
- [Part 7 (Memory performance tools)](http://lwn.net/Articles/257209/)
- [Part 8 (Future technologies)](https://lwn.net/Articles/258154/)
- [Part 9 (Appendices and bibliography)](https://lwn.net/Articles/258188/)

然后是几篇和内存相关的论文。下面这三篇论文是我个人觉得能对你非常有帮助的文章，尤其是你要做一些程序的性能优化方面。

- [Memory Barriers: a Hardware View for Software Hackers](http://irl.cs.ucla.edu/~yingdi/web/paperreading/whymb.2010.06.07c.pdf)。内存的读写屏障是线程并发访问共享的内存数据时，从程序本身、编译器到 CPU 都必须遵循的一个规范。有了这个规范，才能保证访问共享的内存数据时，一个线程对该数据的更新能被另一个线程以正确的顺序感知到。在 SMP（对称多处理）这种类型的多处理器系统（包括多核系统）上，这种读写屏障还包含了复杂的缓存一致性策略。这篇文章做了详细解释。
- [A Tutorial Introduction to the ARM and POWER Relaxed Memory Models](http://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf)，对 ARM 和 POWER 的宽松内存模型的一个教程式的简介。本篇文章的焦点是 ARM 和 POWER 体系结构下多处理器系统内存并发访问一致性的设计思路和使用方法。与支持较强的 TSO 模型的 x86 体系结构不同，ARM 和 POWER 这两种体系结构出于对功耗和性能的考虑，使用了一种更为宽松的内存模型。本文详细讨论了 ARM 和 POWER 的模型。
- [x86-TSO: A Rigorous and Usable Programmer’s Model for x86 Multiprocessors](http://www.cl.cam.ac.uk/~pes20/weakmemory/cacm.pdf)，介绍 x86 的多处理器内存并发访问的一致性模型 TSO。

接下来是开发者最关心的内存管理方面的 lib 库。通常来说，我们有三种内存分配管理模块。就目前而言，BSD 的 jemalloc 有很大的影响力。后面我们可以看到不同公司的实践性文章。

- [ptmalloc](http://www.malloc.de/en/) 是 glibc 的内存分配管理。
- [tcmalloc](https://github.com/gperftools/gperftools) 是 Google 的内存分配管理模块，全称是 Thread-Caching malloc，基本上来说比 glibc 的 ptmalloc 快两倍以上。
- [jemalloc](http://jemalloc.net/) 是 BSD 提供的内存分配管理。其论文为 [A Scalable Concurrent malloc(3) Implementation for FreeBSD](https://people.freebsd.org/~jasone/jemalloc/bsdcan2006/jemalloc.pdf)，这是一个可以并行处理的内存分配管理器。

关于 C 的这些内存分配器，你可以参看 Wikipedia 的 “[C Dynamic Memory Allocation](https://en.wikipedia.org/wiki/C_dynamic_memory_allocation#Thread-caching_malloc_(tcmalloc))”这个词条。

下面是几篇不错的文章，让你感觉一下上面那三种内存分配器的一些比较和工程实践。

- [ptmalloc，tcmalloc 和 jemalloc 内存分配策略研究](https://owent.net/2013/867.html)
- [内存优化总结：ptmalloc、tcmalloc 和 jemalloc](http://www.cnhalo.net/2016/06/13/memory-optimize/)
- [Scalable memory allocation using jemalloc](https://www.facebook.com/notes/facebook-engineering/scalable-memory-allocation-using-jemalloc/480222803919)
- [Decreasing RAM Usage by 40% Using jemalloc with Python & Celery](https://zapier.com/engineering/celery-python-jemalloc/)

### 计算机网络

#### 网络学习

首先，推荐一本书——《[计算机网络（第五版）](https://book.douban.com/subject/10510747/)》，这本“计算机网络”和前面推荐的那本计算机网络不一样，前面那本偏扫盲，这本中有很多细节。这本书是国内外使用最广泛、最权威的计算机网络经典教材。全书按照网络协议模型自下而上（物理层、数据链路层、介质访问控制层、网络层、传输层和应用层）有系统地介绍了计算机网络的基本原理，并结合 Internet 给出了大量的协议实例。

这本书还与时俱进地引入了最新的网络技术，包括无线网络、3G 蜂窝网络、RFID 与传感器网络、内容分发与 P2P 网络、流媒体传输与 IP 语音，以及延迟容忍网络等。另外，本书针对当前网络应用中日益突出的安全问题，用了一整章的篇幅对计算机网络的安全性进行了深入讨论，而且把相关内容与最新网络技术结合起来阐述。这本书读起来并不枯燥，因为其中有很多小故事和小段子。

然后，有两个网上的教程和讲义也可以让人入门。

- 渥汰华大学的一个课程讲义你也可以一看 [Computer Network Design](http://www.site.uottawa.ca/~shervin/courses/ceg4185/lectures/) 。
- GeeksforGeeks 上也有一个简单的 [Computer Network Tutorials](https://www.geeksforgeeks.org/computer-network-tutorials/) 。

#### 网络调优

接下来，你可能需要一些非常实用的可以操作的技术，下面的几篇文章相信可以帮助到你。

- 《Linux 的高级路由和流量控制 HowTo》（[Linux Advanced Routing & Traffic Control HOWTO](http://lartc.org/) ），这是一个非常容易上手的关于 iproute2、流量整形和一点 netfilter 的指南。
- 关于网络调优，你可以看一下这个文档 [Red Hat Enterprise Linux Network Performance Tuning Guide](https://access.redhat.com/sites/default/files/attachments/20150325_network_performance_tuning.pdf)。
- 还有一些网络工具能够帮上你的大忙，这里有一个网络工具的 Awesome 列表 [Awesome Pcap Tools](https://github.com/caesar0301/awesome-pcaptools) ，其中罗列了各种网络工具，能够让你更从容地调试网络相关的程序。
- [Making Linux TCP Fast](https://netdevconf.org/1.2/papers/bbr-netdev-1.2.new.new.pdf) ，一篇非常不错的 TCP 调优的论文。
- 下面是在 PackageCloud 上的两篇关于 Linux 网络栈相关的底层文章，非常值得一读。

  - [Monitoring and Tuning the Linux Networking Stack: Receiving Data](https://blog.packagecloud.io/eng/2016/06/22/monitoring-tuning-linux-networking-stack-receiving-data/)
  - [Monitoring and Tuning the Linux Networking Stack: Sending Data](https://blog.packagecloud.io/eng/2017/02/06/monitoring-tuning-linux-networking-stack-sending-data/)

#### 网络协议

接下来，想要学习网络协议最好的方式就是学习通讯相关的 RFC。所以，在这里我会推荐一系列值得读的 RFC 给你。读 RFC 有几个好处，一方面可以学习技术，另一方面，你可以通过 RFC 学习到一个好的技术文档是怎么写的，还能看到各种解决问题的方案和思路。

对于第 2 层链路层，你可能需要了解一下 ARP：

- [RFC 826 - An Ethernet Address Resolution Protocol](https://tools.ietf.org/html/rfc826)

以及 Tunnel 相关的协议：

- [RFC 1853 - IP in IP Tunneling](https://tools.ietf.org/html/rfc1853)
- [RFC 2784 - Generic Routing Encapsulation (GRE)](https://tools.ietf.org/html/rfc2784)
- [RFC 2661 - Layer Two Tunneling Protocol “L2TP”](https://tools.ietf.org/html/rfc2661)
- [RFC 2637 - Point-to-Point Tunneling Protocol (PPTP)](https://tools.ietf.org/html/rfc2637)

对于第 4 层，你最需要了解的是 TCP/IP 了。和 TCP 相关的 RFC 相当多，这里给一系列经典的 RFC。这些 RFC 我都引用在了我在 CoolShell 上的《[TCP 的那些事儿（上）](https://coolshell.cn/articles/11564.html)》和《[TCP 的那些事儿（下）](https://coolshell.cn/articles/11609.html)》两篇文章中。如果你看不懂 RFC，你也可以去看我上述的文章。

- [RFC 793 - Transmission Control Protocol](https://tools.ietf.org/html/rfc793) - 最初的 TCP 标准定义，但不包括 TCP 相关细节。
- [RFC 813 - Window and Acknowledgement Strategy in TCP](https://tools.ietf.org/html/rfc813) - TCP 窗口与确认策略，并讨论了在使用该机制时可能遇到的问题及解决方法。
- [RFC 879 - The TCP Maximum Segment Size and Related Topics](https://tools.ietf.org/html/rfc879) - 讨论 MSS 参数对控制 TCP 分组大小的重要性，以及该参数与 IP 分段大小的关系等。
- [RFC 896 - Congestion Control in IP/TCP Internetworks](https://tools.ietf.org/html/rfc896) - 讨论拥塞问题和 TCP 如何控制拥塞。

- [RFC 2581 - TCP Congestion Control](https://tools.ietf.org/html/rfc2581) - 描述用于拥塞控制的四种机制：慢启动、拥塞防御、快重传和快恢复。后面这个 RFC 被 [RFC 5681](https://tools.ietf.org/html/rfc5681) 所更新。还有 [RFC 6582 - The NewReno Modification to TCP’s Fast Recovery Algorithm](https://tools.ietf.org/html/rfc6582) 中一个改进的快速恢复算法。
- [RFC 2018 - TCP Selective Acknowledgment Options](https://tools.ietf.org/html/rfc2018) - TCP 的选择确认。
- [RFC 2883 - An Extension to the Selective Acknowledgement (SACK) Option for TCP](https://tools.ietf.org/html/rfc2883) - 对于 RFC 2018 的改进。
- [RFC 2988 - Computing TCP’s Retransmission Timer](https://tools.ietf.org/html/rfc2988) - 讨论与 TCP 重传计时器设置相关的话题，重传计时器控制报文在重传前应等待多长时间。也就是经典的 TCP Karn/Partridge 重传算法。
- [RFC 6298 - Computing TCP’s Retransmission Timer](https://tools.ietf.org/html/rfc6298) - TCP Jacobson/Karels Algorithm 重传算法。

我个人觉得 TCP 最牛的不是不丢包，而是拥塞控制。对此，如果你感兴趣，可以读一下经典论文《[Congestion Avoidance and Control](http://ee.lbl.gov/papers/congavoid.pdf)》。

关于 Linux 下的 TCP 参数，你需要仔仔细细地读一下[TCP 的 man page](http://man7.org/linux/man-pages/man7/tcp.7.html) 。

对于第 7 层协议，HTTP 协议是重点要学习的。

首先推荐的是《[HTTP 权威指南](https://book.douban.com/subject/10746113/) 》，这本书有点厚，可以当参考书来看。这本书中没有提到 HTTP/2 的事，但是可以让你了解到 HTTP 协议的绝大多数特性。

HTTP 1.1 的原始 RFC 是 1999 年 6 月的 [RFC 2616](https://tools.ietf.org/html/rfc2616)，但其在 2014 后很快被下面这些 RFC 给取代了。

- [RFC 7230 - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing](https://tools.ietf.org/html/rfc7230)
- [RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://tools.ietf.org/html/rfc7231)
- [RFC 7232 - Hypertext Transfer Protocol (HTTP/1.1): Conditional Requests](https://tools.ietf.org/html/rfc7232)
- [RFC 7233 - Hypertext Transfer Protocol (HTTP/1.1): Range Requests](https://tools.ietf.org/html/rfc7233)
- [RFC 7234 - Hypertext Transfer Protocol (HTTP/1.1): Caching](https://tools.ietf.org/html/rfc7234)
- [RFC 7235 - Hypertext Transfer Protocol (HTTP/1.1): Authentication](https://tools.ietf.org/html/rfc7235)

关于[HTTP/2](https://en.wikipedia.org/wiki/HTTP/2)，这是 HTTP 的一个比较新的协议，它于 2015 年被批准通过，现在基本上所有的主流浏览器都默认启用这个协议。所以，你有必要学习一下这个协议。下面是相关的学习资源。

- [Gitbook - HTTP/2 详解](https://legacy.gitbook.com/book/ye11ow/http2-explained/details)
- [http2 explained](http://daniel.haxx.se/http2/)（[中译版](https://www.gitbook.com/book/ye11ow/http2-explained/details)）
- [HTTP/2 for a Faster Web](https://cascadingmedia.com/insites/2015/03/http-2.html)
- [Nginx HTTP/2 白皮书](https://www.nginx.com/wp-content/uploads/2015/09/NGINX_HTTP2_White_Paper_v4.pdf)
- HTTP/2 的两个 RFC：

  - [RFC 7540 - Hypertext Transfer Protocol Version 2 (HTTP/2)](https://httpwg.org/specs/rfc7540.html) ，HTTP/2 的协议本身
  - [RFC 7541 - HPACK: Header Compression for HTTP/2](https://httpwg.org/specs/rfc7541.html) ，HTTP/2 的压缩算法

最后，你可以上 Wikipedia 的 [Internet Protocol Suite](https://en.wikipedia.org/wiki/Internet_protocol_suite) 上看看，这是一个很不错的网络协议的词条汇集地。顺着这些协议，你可以找到很多有用的东西。

## 异步I/O模型和Lock-Free编程

### 异步 I/O 模型

异步 I/O 模型是我个人觉得所有程序员都必需要学习的一门技术或是编程方法，这其中的设计模式或是解决方法可以借鉴到分布式架构上来。再说一遍，学习这些模型，是非常非常重要的，你千万要认真学习。

史蒂文斯（Stevens）在《[UNIX 网络编程](https://book.douban.com/subject/4859464/)》一书 6.2 I/O Models 中介绍了五种 I/O 模型。

- 阻塞 I/O
- 非阻塞 I/O
- I/O 的多路复用（select 和 poll）
- 信号驱动的 I/O（SIGIO）
- 异步 I/O（POSIX 的 aio_functions）

然后，在前面我们也阅读过了 - [C10K Problem](https://en.wikipedia.org/wiki/C10k_problem) 。相信你对 I/O 模型也有了一定的了解。 这里，我们需要更为深入地学习 I/O 模型，尤其是其中的异步 I/O 模型。

首先，我们看一篇和 Java 相关的 I/O 模型的文章来复习一下之前的内容。[Thousands of Threads and Blocking I/O: The Old Way to Write Java Servers Is New Again (and Way Better)](https://www.slideshare.net/e456/tyma-paulmultithreaded1) ，这个 PPT 中不仅回顾和比较了各种 I/O 模型，而且还有各种比较细节的方案和说明，是一篇非常不错的文章。

然后，你可以看一篇 Java 相关的 PPT - 道格·莱亚（Doug Lea）的 [Scalable IO in Java](http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf)，这样你会对一些概念有个了解。

接下来，我们需要了解一下各种异步 I/O 的实现和设计方式。

- [IBM - Boost application performance using asynchronous I/O](https://www.ibm.com/developerworks/library/l-async/) ，这是一篇关于 AIO 的文章。
- [Lazy Asynchronous I/O For Event-Driven Servers](https://www.usenix.org/legacy/event/usenix04/tech/general/full_papers/elmeleegy/elmeleegy_html/html.html) ，这篇文章也很不错。
- 另外，异步 I/O 模型中的 [Windows I/O Completion Ports](https://docs.microsoft.com/en-us/windows/desktop/FileIO/i-o-completion-ports) , 你也需要了解一下。如果 MSDN 上的这个手册不容易读，你可以看看这篇文章 [Inside I/O Completion Ports](http://sysinternals.d4rk4.ru/Information/IoCompletionPorts.html)。另外，关于 Windows，[Windows Internals](https://book.douban.com/subject/6935552/) 这本书你可以仔细读一下，非常不错的。其中有一节 I/O Processing 也是很不错的，这里我给一个网上免费的链接[I/O Processing](https://flylib.com/books/en/4.491.1.85/1/) 你可以看看 Windows 是怎么玩的。
- 接下来是 Libevent。你可以看一下其主要维护人员尼克·马修森（Nick Mathewson）写的 [Libevent 2.0 book](http://www.wangafu.net/~nickm/libevent-book/)。还有一本国人写的电子书 《[Libevent 深入浅出](https://aceld.gitbooks.io/libevent/content/)》。
- 再接下来是 Libuv。你可以看一下其官网的 [Libuv Design Overview](http://docs.libuv.org/en/v1.x/design.html) 了解一下。

我简单总结一下，基本上来说，异步 I/O 模型的发展技术是： select -> poll -> epoll -> aio -> libevent -> libuv。Unix/Linux 用了好几十年走过这些技术的变迁，然而，都不如 Windows I/O Completion Port 设计得好（免责声明：这个观点纯属个人观点。相信你仔细研究这些 I/O 模型后，你会有自己的判断）。

看过这些各种异步 I/O 模式的实现以后，相信你会看到一个编程模式——Reactor 模式。下面是这个模式的相关文章（读这三篇就够了）。

- [Understanding Reactor Pattern: Thread-Based and Event-Driven](https://dzone.com/articles/understanding-reactor-pattern-thread-based-and-eve)
- [Reactor Pattern](https://www.dre.vanderbilt.edu/~schmidt/PDF/Reactor2-93.pdf)
- [The reactor pattern and non-blocking IO](https://www.celum.com/en/blog/technology/the-reactor-pattern-and-non-blocking-io)

然后是几篇有意思的延伸阅读文章。

- [The Secret To 10 Million Concurrent Connections -The Kernel Is The Problem, Not The Solution](http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html) - C10M 问题来了……
- 还有几篇可能有争议的文章，让你从不同的角度思考。

  - [Select is fundamentally broken](https://idea.popcount.org/2017-01-06-select-is-fundamentally-broken/)
  - [Epoll is fundamentally broken 1/2](https://idea.popcount.org/2017-02-20-epoll-is-fundamentally-broken-12/)
  - [Epoll is fundamentally broken 2/2](https://idea.popcount.org/2017-03-20-epoll-is-fundamentally-broken-22/)

### Lock-Free 编程相关

Lock-Free - 无锁技术越来越被开发人员重视，因为锁对于性能的影响实在是太大了，所以如果想开发出一个高性能的程序，你就非常有必要学习 Lock-Free 的编程方式。

关于无锁的数据结构，有几篇教程你可以看一下。

- [Dr.Dobb’s: Lock-Free Data Structures](http://www.drdobbs.com/lock-free-data-structures/184401865)
- [Andrei Alexandrescu: Lock-Free Data Structures](https://erdani.com/publications/cuj-2004-10.pdf)

然后强烈推荐一本免费的电子书：[Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://www.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html) ，这是大牛 [保罗·麦肯尼（Paul E. McKenney）](https://www.linkedin.com/in/paulmckenney/) 写的书。这本书堪称并行编程的经典书，必看。

此时，Wikipedia 上有三个词条你要看一下，以此了解并发编程中的一些概念：[Non-blocking algorithm](https://en.wikipedia.org/wiki/Non-blocking_algorithm) 、[Read-copy-update](https://en.wikipedia.org/wiki/Read-copy-update) 和 [Seqlock](https://en.wikipedia.org/wiki/Seqlock)。

接下来，读一下以下两篇论文 。

- [Implementing Lock-Free Queues](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.53.8674&rep=rep1&type=pdf)， 这也是一篇很不错的论文，我把它介绍在了我的网站上 ，文章为“[无锁队列的实现](https://coolshell.cn/articles/8239.html)”。
- [Simple, Fast, and Practical Non-Blocking and Blocking Concurrent Queue Algorithms](http://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf) ，这篇论文给出了一个无阻塞和阻塞的并发队列算法。

最后，有几个博客你要订阅一下。

- [1024cores](http://www.1024cores.net/) - 德米特里·伐由科夫（Dmitry Vyukov）的和 lock-free 编程相关的网站。
- [Paul E. McKenney](http://paulmck.livejournal.com/) - 保罗（Paul）的个人网站。
- [Concurrency Freaks](http://concurrencyfreaks.blogspot.com/) - 关于并发算法和相关模式的网站。
- [Preshing on Programming](http://preshing.com/) - 加拿大程序员杰夫·普莱辛（Jeff Preshing）的技术博客，主要关注 C++ 和 Python 两门编程语言。他用 C++11 实现了类的反射机制，用 C++ 编写了 3D 小游戏 Hop Out，还为该游戏编写了一个游戏引擎。他还讨论了很多 C++ 的用法，比如 C++14 推荐的代码写法、新增的某些语言构造等，和 Python 很相似。阅读这个技术博客上的内容能够深深感受到博主对编程世界的崇敬和痴迷。
- [Sutter’s Mill](http://herbsutter.com/) - 赫布·萨特（Herb Sutter）是一位杰出的 C++ 专家，曾担任 ISO C++ 标准委员会秘书和召集人超过 10 年。他的博客有关于 C++ 语言标准最新进展的信息，其中也有他的演讲视频。博客中还讨论了其他技术和 C++ 的差异，如 C# 和 JavaScript，它们的性能特点、怎样避免引入性能方面的缺陷等。
- [Mechanical Sympathy](http://mechanical-sympathy.blogspot.com/) - 博主是马丁·汤普森（Martin Thompson），他是一名英国的技术极客，探索现代硬件的功能，并提供开发、培训、性能调优和咨询服务。他的博客主题是 Hardware and software working together in harmony，里面探讨了如何设计和编写软件使得它在硬件上能高性能地运行。非常值得一看。

接下来，是一些编程相关的一些 C/C++ 的类库，这样你就不用从头再造轮子了（对于 Java 的，请参看 JDK 里的 Concurrent 开头的一系列的类）。

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

### 其它

- 关于 64 位系统编程，只要去一个地方就行了： [All about 64-bit programming in one place](https://software.intel.com/en-us/blogs/2011/07/07/all-about-64-bit-programming-in-one-place/)，这是一个关于 64 位编程相关的收集页面，其中包括相关的文章、28 节课程，还有知识库和相关的 blog。
- [What Scalable Programs Need from Transactional Memory](https://dl.acm.org/citation.cfm?id=3037750) ，事务性内存（TM）一直是许多研究的重点，它在诸如 IBM Blue Gene/Q 和 Intel Haswell 等处理器中得到了支持。许多研究都使用 STAMP 基准测试套件来评估其设计。然而，我们所知的所有 TM 系统上的 STAMP 基准测试所获得的加速比较有限。

例如，在 IBM Blue Gene/Q 上有 64 个线程，我们观察到使用 Blue Gene/Q 硬件事务内存（HTM）的中值加速比为 1.4 倍，使用软件事务内存（STM）的中值加速比为 4.1 倍。什么限制了这些 TM 基准的性能？在本论文中，作者认为问题在于用于编写它们的编程模型和数据结构上，只要使用合适的模型和数据结构，程序的性能可以有 10 多倍的提升。

- [Improving OpenSSL Performance](https://software.intel.com/en-us/articles/improving-openssl-performance) ，这篇文章除了教你如何提高 OpenSSL 的执行性能，还讲了一些底层的性能调优知识。
- 关于压缩的内容。为了避免枯燥，主要推荐下面这两篇实践性很强的文章。

  - [How eBay’s Shopping Cart used compression techniques to solve network I/O bottlenecks](https://www.ebayinc.com/stories/blogs/tech/how-ebays-shopping-cart-used-compression-techniques-to-solve-network-io-bottlenecks/) ，这是一篇很好的文章，讲述了 eBay 是如何通过压缩数据来提高整体服务性能的，其中有几个比较好的压缩算法。除了可以让你学到相关的技术知识，还可以让你看到一种比较严谨的工程师文化。
  - [Linkedin: Boosting Site Speed Using Brotli Compression](https://engineering.linkedin.com/blog/2017/05/boosting-site-speed-using-brotli-compression) ，LinkedIn 在 2017 年早些时候开始使用 [Brotli](https://en.wikipedia.org/wiki/Brotli) 来替换 gzip，以此带来更快的访问，这篇文章讲述了什么是 Brotli 以及与其它压缩程序的比较和所带来的性能提升。

- 这里有两篇关于 SSD 硬盘性能测试的文章。[Performance Testing with SSDs, Part 1](https://devs.mailchimp.com/blog/performance-testing-with-ssds-part-1/) 和 [Performance Testing with SSDs Part 2](https://devs.mailchimp.com/blog/performance-testing-with-ssds-pt-2/) ，这两篇文章介绍了测试 SSD 硬盘性能以及相关的操作系统调优方法。
- [Secure Programming HOWTO - Creating Secure Software](https://www.dwheeler.com/secure-programs/) ，这是一本电子书，其中有繁体中文的翻译，这本电子书讲了 Linux/Unix 下的一些安全编程方面的知识。

### 相关论文

- [Hints for Computer System Design](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/acrobat-17.pdf) ，计算机设计的忠告，这是 ACM 图灵奖得主 [Butler Lampson](https://en.wikipedia.org/wiki/Butler_Lampson) 在 Xerox PARC 工作时的一篇论文。这篇论文简明扼要地总结了他在做系统设计时的一些想法，非常值得一读。（用他的话来说，“Studying the design and implementation of a number of computer has led to some general hints for system design. They are described here and illustrated by many examples, ranging from hardware such as the Alto and the Dorado to application programs such as Bravo and Star“。）

- [The 5 minute rule for trading memory for disc accesses and the 5 byte rule for trading memory for CPU time](http://www.hpl.hp.com/techreports/tandem/TR-86.1.pdf) ，根据文章名称也可以看出，5 分钟法则是用来衡量内存与磁盘的，而 5 字节法则则是在内存和 CPU 之间的权衡。这两个法则是 Jim Gray 和 Franco Putzolu 在 1986 年的文章。

  在该论文发表 10 年后的 1997 年，Jim Gray 和 Goetz Graefe 又在 [The Five-Minute Rule Ten Years Later and Other Computer Storage Rules of Thumb](http://research.microsoft.com/en-us/um/people/gray/5_min_rule_SIGMOD.pdf) 中对该法则进行了重新审视。2007 年，也就是该论文发表 20 年后，这年的 1 月 28 日，Jim Gray 驾驶一艘 40 英尺长的船从旧金山港出海，目的是航行到附近的费拉隆岛，在那里撒下母亲的骨灰。出海之后，他就同朋友和亲属失去了联系。为了纪念和向大师致敬，时隔 10 多年后的 2009 年 Goetz Graefe 又发表了 [The Five-Minute Rule 20 Years Later (and How Falsh Memory Changes the Rules)](http://cacm.acm.org/magazines/2009/7/32091-the-five-minute-rule-20-years-later/fulltext)。

  注明一下，Jim Gray 是关系型数据库领域的大师。因在数据库和事务处理研究和实现方面的开创性贡献而获得 1998 年图灵奖。美国科学院、工程院两院院士，ACM 和 IEEE 两会会士。他 25 岁成为加州大学伯克利分校计算机科学学院第一位博士。在 IBM 工作期间参与和主持了 IMS、System R、SQL／DS、DB2 等项目的开发。后任职于微软研究院，主要关注应用数据库技术来处理各学科的海量信息。

## Java 底层知识

### Java 字节码相关

首先，Java 最黑科技的玩法就是字节码编程，也就是动态修改或是动态生成 Java 字节码。Java 的字节码相当于汇编，其中的一些细节你可以从下面的这几个教程中学习。

- [Java Zone: Introduction to Java Bytecode](https://dzone.com/articles/introduction-to-java-bytecode) ，这篇文章图文并茂地向你讲述了 Java 字节码的一些细节，是一篇很不错的入门文章。
- [IBM DeveloperWorks: Java bytecode](https://www.ibm.com/developerworks/library/it-haggar_bytecode/index.html) ，虽然这篇文章很老了，但是这篇文章是一篇非常好的讲 Java 字节码的文章。
- [Java Bytecode and JVMTI Examples](https://github.com/jon-bell/bytecode-examples)，这是一些使用 [JVM Tool Interface](http://docs.oracle.com/javase/7/docs/platform/jvmti/jvmti.html) 操作字节码的比较实用的例子。包括方法调用统计、静态字节码修改、Heap Taggin 和 Heap Walking。

当然，一般来说，我们不使用 JVMTI 操作字节码，而是用一些更好用的库。这里有三个库可以帮你比较容易地做这个事。

- [asmtools](https://wiki.openjdk.java.net/display/CodeTools/asmtools) - 用于生产环境的 Java .class 文件开发工具。
- [Byte Buddy](http://bytebuddy.net/) - 代码生成库：运行时创建 Class 文件而不需要编译器帮助。
- [Jitescript](https://github.com/qmx/jitescript) - 和 [BiteScript](https://github.com/headius/bitescript) 类似的字节码生成库。

就我而言，我更喜欢 Byte Buddy，它在 2015 年还获了 Oracle 的 “[Duke’s Choice](https://www.oracle.com/corporate/pressrelease/dukes-award-102815.html)”大奖，其中说 Byte Buddy 极大地发展了 Java 的技术。

使用字节码编程可以玩出很多高级玩法，最高级的还是在 Java 程序运行时进行字节码修改和代码注入。听起来是不是一些很黑客，也很黑科技的事？是的，这个方式使用 Java 这门静态语言在运行时可以进行各种动态的代码修改，而且可以进行无侵入的编程。

比如， 我们不需要在代码中埋点做统计或监控，可以使用这种技术把我们的监控代码直接以字节码的方式注入到别人的代码中，从而实现对实际程序运行情况进行统计和监控。如果你看过我的《编程范式游记》，你就知道这种技术的威力了，其可以很魔法地把业务逻辑和代码控制分离开来。

要做到这个事，你还需要学习一个叫 Java Agent 的技术。Java Agent 使用的是 “[Java Instrumentation API](https://stackoverflow.com/questions/11898566/tutorials-about-javaagents)”，其主要方法是实现一个叫 premain() 的方法（嗯，一个比 main() 函数还要超前执行的 main 函数），然后把你的代码编译成一个 jar 文件。

在 JVM 启动时，使用这样的命令行来引入你的 jar 文件：java -javaagent:yourAwesomeAgent.jar -jar App.jar。更为详细的文章你可以参看：“[Java Code Geeks: Java Agents](https://www.javacodegeeks.com/2015/09/java-agents.html)”，你还可以看一下这个示例项目：[jvm-monitoring-agent](https://github.com/toptal/jvm-monitoring-agent) 或是 [EntryPointKR/Agent.java](https://gist.github.com/EntryPointKR/152f089f6f3884047abcd19d39297c9e)。如果想用 ByteBuddy 来玩，你可以看看这篇文章 “[通过使用 Byte Buddy，便捷地创建 Java Agent](http://www.infoq.com/cn/articles/Easily-Create-Java-Agents-with-ByteBuddy)”。如果你想学习如何用 Java Agent 做监控，你可以看一下这个项目 [Stage Monitor](http://www.stagemonitor.org/)。

### JVM 相关

接下来讲讲 Java 底层知识中另一个非常重要的内容——JVM。

说起 JVM，你有必要读一下 JVM 的规格说明书，我在这里放一个 Java 8 的， [The Java Virtual Machine Specification Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/jvms8.pdf) 。对于规格说明书的阅读，我认为是系统了解 JVM 规范的最佳文档，这个文档可以让你对于搞不清楚或是诡异的问题恍然大悟。关于中文翻译，有人在 GitHub 上开了个 Repo - “[java-virtual-machine-specification](https://github.com/waylau/java-virtual-machine-specification)”。

另外，也推荐一下 [JVM Anatomy Park](https://shipilev.net/jvm-anatomy-park/) JVM 解剖公园，这是一个系列的文章，每篇文章都不长，但是都很精彩，带你一点一点地把 JVM 中的一些技术解开。

学习 Java 底层原理还有 Java 的内存模型，官方文章是 [JSR 133](http://www.jcp.org/en/jsr/detail?id=133)。还有马里兰大学的威廉·皮尤（William Pugh）教授收集的和 Java 内存模型相关的文献 - [The Java Memory Model](http://www.cs.umd.edu/~pugh/java/memoryModel/) ，你可以前往浏览。

对于内存方面，道格·利（Doug Lea）有两篇文章也是很有价值的。

- [The JSR-133 Cookbook for Compiler Writers](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)，解释了怎样实现 Java 内存模型，特别是在考虑到多处理器（或多核）系统的情况下，多线程和读写屏障的实现。
- [Using JDK 9 Memory Order Modes](http://gee.cs.oswego.edu/dl/html/j9mm.html)，讲了怎样通过 VarHandle 来使用 plain、opaque、release/acquire 和 volatile 四种共享内存的访问模式，并剖析了底层的原理。

垃圾回收机制也是需要好好学习的，在这里推荐一本书 《[The Garbage Collection Handbook](https://book.douban.com/subject/6809987/)》，在豆瓣上的得分居然是 9.9（当然，评价人数不多）。这本书非常全面地介绍了垃圾收集的原理、设计和算法。但是这本书也是相当难啃的。中文翻译《[垃圾回收算法手册](https://book.douban.com/subject/26740958/)》翻译得很一般，有人说翻译得很烂。所以，如果可能，还是读英文版的。如果你对从事垃圾回收相关的工作有兴趣，那么你需要好好看一下这本书。

当然，更多的人可能只需要知道怎么调优垃圾回收， 那么推荐读读 [Garbage Collection Tuning Guide](http://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/) ，它是 Hotspot Java 虚拟机的垃圾回收调优指南，对你很有帮助。

[Quick Tips for Fast Code on the JVM](https://gist.github.com/djspiewak/464c11307cabc80171c90397d4ec34ef) 也是一篇很不错的文章，里面有写出更快的 Java 代码的几个小提示，值得一读。
