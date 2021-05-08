# [ReTrace: Collecting Execution Trace with Virtual Machine Deterministic Replay](https://labs.vmware.com/academic/publications/retrace) 论文阅读笔记

Retrace 将传统的 trace collection 分为两步：capturing, expansion

- Capturing
  - 在 VM 中执行一遍，把 non-deterministic 按顺序记录到 replay log
- Expansion
  - （没明说，我猜的）在 VM 中重新执行，并且检测 non-deterministic，碰到后在 replay log 取，然后执行


## Reference

- [qemu/docs/replay.txt](https://github.com/qemu/qemu/blob/master/docs/replay.txt)