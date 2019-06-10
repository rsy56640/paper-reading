# [Time, Clocks, and the Ordering of Events in a Distributed System](https://lamport.azurewebsites.net/pubs/time-clocks.pdf) 论文阅读笔记



之前看过一点分布式算法：[Distributed Computing —— Principles, Algorithms, and System 笔记](<https://blog.csdn.net/rsy56640/article/details/89020572>)，看这篇就比较轻松了。



**happens-before relation**: $a\to b$, event $a$ happens before event $b$ if

- $a$ 和 $b$ 在同一进程，并且 $a$ sequences before $b$
- $a​$ 和 $b​$ 在不同进程，并且 $a​$ synchronizes before $b​$，即 $a​$ 是一个消息发送事件，$b​$ 是一个消息接收事件
- $\to$ 具有传递性

*happens-before* 是偏序关系（partial ordering），称 $a$ 与 $b$ 是并发的，即 $a||b$，如果 $a\not \to b$ 并且 $b\not\to a$。



## Logical Clock

logical clock 是每一个进程自己的递增的 counter（递增步幅不定），当一个事件发生时就产生一个 timestamp，$C_i(a)$。

如果 $a\to b​$，那么

- $a$ 和 $b$ 在同一进程，有 $C(a)<C(b)$
- 进程 $p_i$ 的发送事件 $a$ 和进程 $p_j$ 的接受事件 $b$，有 $C_i(a)<C_j(b)$

于是有
$$
a\to b \Rightarrow C(a) < C(b)
$$
反之不成立



## Ordering the Events Totally

在进程间定义全序关系 $\prec$，可以任意指定

定义事件全序关系 $a\Rightarrow b$，事件 $a\in p_i$，事件 $b\in p_j$，如果

- $C_i(a)<C_j(b)$ 或者
- $C_i(a)=C_j(b)\ \land\ p_i\prec p_j$

于是有 $a\to b$ 推出 $a\Rightarrow b$

有句话他在 intro(Ref[1]) 中强调了：

> The synchronization is specified in terms of a State Machine.
>
> （**在 FIFO 通信模型中**）A process can execute a command timestamped $T$ when it has learned of all commands issued by all other processes with timestamps less than or equal to $T$. 



## Physical Clocks

$C_i(t)$ 表示进程 $p_i$ 在物理时刻 $t$ 时的进程逻辑时钟的值。

- $|C_i^{'}(t)-1|<k$
- $|C_i(t)-C_j(t)|<\epsilon$

为了保证：在物理时刻 $t$ 从 $p_j$ 发出的信息到达 $p_i$ 的时钟 $C_i(t+t_0)$ 一定比 $C_j(t)$ 大，我们需要找到一个 $\mu$，使得 $C_i(t+\mu)-C_j(t) > 0$，其中 $\mu$ 是比传输时间小的值。

粗略估计，当 $\mu \ge \frac{\epsilon}{1-k}$ 时，$C_i(t+\mu)-C_j(t) > 0$ 成立。（这保证了现实世界中的同步关系，即所有进程所组成的系统之外的 *happens-before* 关系）



最后给了个定理，没看懂说的啥，以后看吧。




## Reference

- [Lamport introduction](https://lamport.azurewebsites.net/pubs/pubs.html#time-clocks)
- [Lamport’s “Time, Clocks and the Ordering of events in a Distributed System.”](https://blogs.wandisco.com/lamports-time-clocks-and-the-ordering-of-events-in-a-distributed-system/)
- [Lamport timestamps - Wiki](https://en.wikipedia.org/wiki/Lamport_timestamps)
- [论文笔记：Time, clocks, and the ordering of events in a distributed system](https://zhuanlan.zhihu.com/p/34057588)
- [Time and clocks and ordering of events in a distributed system](https://medium.com/coinmonks/time-and-clocks-and-ordering-of-events-in-a-distributed-system-cdd3f6075e73)
- [【每周论文】Time, Clocks, and Ordering of Events in a Distributed System](https://blog.csdn.net/violet_echo_0908/article/details/77430511)
- [time-clocks原版英文PPT](https://download.csdn.net/download/qq_38789572/10516152)
- [Week 7: Time, Clocks, and Ordering of Events in a Distributed System](https://swizec.com/blog/week-7-time-clocks-and-ordering-of-events-in-a-distributed-system/swizec/6444)