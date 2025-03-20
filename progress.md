# 大实验每周进展汇总

方向：基于Starry + Dora为小车提供操作系统支持。

## 3.14 ~ 3.20

- 确定选题，建立开发环境
- 成功在x86_64虚拟机Debian 12.5系统上运行qemu x86_64和aarch64架构的Starry + Dora (`dora -h`)

### 踩坑记录

#### 编译需打开`NET=y`选项

参考 https://echoli.cn/dora/zero/env.html 的内容编译Starry，发现无法运行。调试后发现网络模块报错，阅读`Makefile`文件，在`make`指令中加入`NET=y`后成功运行。

#### 使用`musl`作为库而不是`libc`

同上资料的问题，使用`libc`编译dora会缺运行库，从Debian上复制运行库到磁盘文件中，仍然无法正常运行。改用`musl`编译的版本则不需动态链接库，可直接在Starry-Old上运行。

#### dora运行卡死

在各种环境（x86_64，aarch64）中成功运行`dora -h`无问题，运行`dora up`则会在应当第一次输出时卡死，原因不明。
