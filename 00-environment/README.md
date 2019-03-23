*Concepts you may want to Google beforehand: linux, mac, terminal, compiler, emulator, nasm, qemu*

**目标：安装运行本教程所需的软件**

我正在使用Mac，虽然Linux更好，因为它已经拥有所有标准工具
适合你。

在mac上, [安装Homebrew](http://brew.sh) 然后执行命令 `brew install qemu nasm`

如果你安装了xcode，你不要使用xcode带的`nasm`，因为他大多数情况下不起作用。 使用brew安装的nasm，它在 `/usr/local/bin/nasm`

在某些系统上，qemu被分成多个二进制文件. 你可能需要执行命令 `qemu-system-x86_64 binfile`

