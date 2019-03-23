*Concepts you may want to Google beforehand: interrupts, CPU
registers*

**目标：让我们之前的静默启动扇区打印一些文本**

我们将在无限循环引导扇区和打印上进行一些改进屏幕上的东西。 我们将为此提出一个中断。

在这个例子中，我们将把“Hello,world”字符串的每个字符写入寄存器al（ax的下半部分），将字节0x0e写入ah（ax的较高部分）并引发中断0x10，这是视频的一般中断服务。

`0x0e` 告诉视频中断我们要运行的实际功能是'在tty模式下写入al的内容'。

我们只设置tty模式一次虽然在现实世界中我们不能确定`ah`的内容是不变的. 我们睡眠时，其他一些进程可能会在CPU上运行,没有正确清理并在`ah`上留下垃圾数据。

对于这个例子，我们不需要处理它，因为我们是在CPU上运行的唯一东西。

我们的新引导扇区看起来像这样:
```nasm
mov ah, 0x0e ; tty mode
mov al, 'H'
int 0x10
mov al, 'e'
int 0x10
mov al, 'l'
int 0x10
int 0x10 ; 'l' is still on al, remember?
mov al, 'o'
int 0x10
mov al, ','
int 0x10
mov al, 'w'
int 0x10
mov al, 'o'
int 0x10
mov al, 'r'
int 0x10
mov al, 'l'
int 0x10
mov al, 'd'
int 0x10

jmp $ ; jump to current address = infinite loop

; padding and magic number
times 510 - ($-$$) db 0
dw 0xaa55 
```

您可以使用检查二进制数据 `xxd file.bin`

无论如何，你知道演习:

`nasm -fbin boot_sect_hello.asm -o boot_sect_hello.bin`

`qemu boot_sect_hello.bin`

您的引导扇区会说“Hello”并挂起无限循环
