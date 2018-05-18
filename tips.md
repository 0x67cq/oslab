# 这个实验需要注意的点

BIOS中断的int 10 对于偏移量是有默认的段的。可以在wiki上看到

> AL = Write mode, BH = Page Number, BL = Color, CX = String length, DH = Row, DL = Column, ES:BP = Offset of string

所以在setup.s里打印信息的时候需要把段置为setup的内存起始


汇编代码的段（segment）作用在于可以扩大寻址范围&分离代码的作用范围。由于8086的段寄存器只有16位所以寻址范围只有2的16次方=64K，所以为了扩大寻址范围使用了cs:ip这种实模式寻址方式。然后对于一些特定的汇编语言里，标号表示的数据在被标号表示偏移的时候使用的都是相对偏移，所以类似于上面的int 10，BP是这个汇编文件汇编成二进制文件之后的相对于开头的偏移距离，而需要配上es这种段寄存器才是真实的物理内存地址。
