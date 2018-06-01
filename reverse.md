c語言程式
編譯與組譯
預處理階段
```
gcc –E 123.c –o 123.i
```

![圖證](https://github.com/0Isolesty0/image/blob/master/%E9%A0%90%E8%99%95%E7%90%86%E9%9A%8E%E6%AE%B5.PNG)

查看123.i
()[https://github.com/0Isolesty0/reverse/blob/master/123.i]
編譯階段
產生組語
```
gcc –S 123.i  –o 123.s
```
產生AT&T語法格式的組語(gcc預設使用的格式)
查看123.s的架構
```
	.file	"123.c"
	.section	.rodata
.LC0:
	.string	"%d\n"
	.text
	.globl	main
	.type	main, @function
main:
.LFB2:
	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	subq	$16, %rsp
	movl	$0, -8(%rbp)
	movl	$9, -12(%rbp)
	movl	$1, -4(%rbp)
	jmp	.L2
.L3:
	movl	-4(%rbp), %eax
	addl	$1, %eax
	addl	%eax, %eax
	movl	%eax, -8(%rbp)
	movl	-8(%rbp), %eax
	movl	%eax, -4(%rbp)
	subl	$1, -12(%rbp)
.L2:
	cmpl	$0, -12(%rbp)
	jg	.L3
	movl	-8(%rbp), %eax
	movl	%eax, %esi
	movl	$.LC0, %edi
	movl	$0, %eax
	call	printf
	movl	$0, %eax
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE2:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```
組譯階段
```
gcc -c 123.s -o 123.o

```
連結階段

![圖證](https://github.com/0Isolesty0/image/blob/master/%E7%B5%84%E8%AD%AF%EF%BC%8C%E9%80%A3%E7%B5%90.PNG)

```
gcc 123.o -o 123
```
gcc -S -masm=att XXXXX.c -o XXXXX_att.s
產生Intel語法格式的組語(微軟預設使用的格式)
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel.s
要去掉一堆註解:請加上參數-fno-asynchronous-unwind-tables
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel_OK.s -fno-asynchronous-unwind-tables
組譯過程
```
將組合語言程式碼轉成機器可以執行的指令(instructions)
每一個組語語句都對應一機器指令。
組譯器的組譯過程相對於編譯器來講比較簡單
沒有複雜的語法，也沒有語意，也不需要做指令最佳化，只是根據組語指令和機器指令的對照表一一翻譯就可以
連結過程
```
