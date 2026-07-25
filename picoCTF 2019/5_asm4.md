# asm4  

<br>

URL: https://learn.cylabacademy.org/library/5  

<br>

```
Reverse Engineering
Hard
400 pts
by Sanjay C
picoCTF 2019

What will asm4("picoCTF_3de4a") return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source
```

<br>

## フラグ取得の過程  

"Source"と書かれているリンクをクリックすると「test.S」という名前のファイルをダウンロードできる。  

fileコマンドで調べる。  

```
$ file test.S 
test.S: ASCII text
```

テキストファイルなので、エディターで内容を見てみる。  

```
asm4:
	<+0>:	endbr32 
	<+4>:	push   ebp
	<+5>:	mov    ebp,esp
	<+7>:	push   ebx
	<+8>:	sub    esp,0x10
	<+11>:	mov    DWORD PTR [ebp-0x10],0x24b
	<+18>:	mov    DWORD PTR [ebp-0xc],0x0
	<+25>:	jmp    0x11cc <asm4+31>
	<+27>:	add    DWORD PTR [ebp-0xc],0x1
	<+31>:	mov    edx,DWORD PTR [ebp-0xc]
	<+34>:	mov    eax,DWORD PTR [ebp+0x8]
	<+37>:	add    eax,edx
	<+39>:	movzx  eax,BYTE PTR [eax]
	<+42>:	test   al,al
	<+44>:	jne    0x11c8 <asm4+27>
	<+46>:	mov    DWORD PTR [ebp-0x8],0x1
	<+53>:	jmp    0x123b <asm4+142>
	<+55>:	mov    edx,DWORD PTR [ebp-0x8]
	<+58>:	mov    eax,DWORD PTR [ebp+0x8]
	<+61>:	add    eax,edx
	<+63>:	movzx  eax,BYTE PTR [eax]
	<+66>:	movsx  edx,al
	<+69>:	mov    eax,DWORD PTR [ebp-0x8]
	<+72>:	lea    ecx,[eax-0x1]
	<+75>:	mov    eax,DWORD PTR [ebp+0x8]
	<+78>:	add    eax,ecx
	<+80>:	movzx  eax,BYTE PTR [eax]
	<+83>:	movsx  eax,al
	<+86>:	sub    edx,eax
	<+88>:	mov    eax,edx
	<+90>:	mov    edx,eax
	<+92>:	mov    eax,DWORD PTR [ebp-0x10]
	<+95>:	lea    ebx,[edx+eax*1]
	<+98>:	mov    eax,DWORD PTR [ebp-0x8]
	<+101>:	lea    edx,[eax+0x1]
	<+104>:	mov    eax,DWORD PTR [ebp+0x8]
	<+107>:	add    eax,edx
	<+109>:	movzx  eax,BYTE PTR [eax]
	<+112>:	movsx  edx,al
	<+115>:	mov    ecx,DWORD PTR [ebp-0x8]
	<+118>:	mov    eax,DWORD PTR [ebp+0x8]
	<+121>:	add    eax,ecx
	<+123>:	movzx  eax,BYTE PTR [eax]
	<+126>:	movsx  eax,al
	<+129>:	sub    edx,eax
	<+131>:	mov    eax,edx
	<+133>:	add    eax,ebx
	<+135>:	mov    DWORD PTR [ebp-0x10],eax
	<+138>:	add    DWORD PTR [ebp-0x8],0x1
	<+142>:	mov    eax,DWORD PTR [ebp-0xc]
	<+145>:	sub    eax,0x1
	<+148>:	cmp    DWORD PTR [ebp-0x8],eax
	<+151>:	jl     0x11e4 <asm4+55>
	<+153>:	mov    eax,DWORD PTR [ebp-0x10]
	<+156>:	add    esp,0x10
	<+159>:	pop    ebx
	<+160>:	pop    ebp
	<+161>:	ret    
```

上記コードの動作を解析して「picoCTF_3de4a」という文字がどのような出力になるかを調べれば良いことになる。  

しかし、このコードを1行ずつ解析していくのは大変手間がかかる作業になる。そこで、以下のサイトを参考にして、C言語のコードに変換する。  

［参考］GCCのドキュメントサイト：https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html  

C言語に変換したコードは以下になる。  

```
#include <stdio.h>
#include <stdlib.h>

int asm4(char* in)
{
    int value;

    asm (
        "nop;"
        "nop;"
        "nop;"
        //"push   ebp;"
        //"mov    ebp,esp;"
        "push   ebx;"
        "sub    esp,0x10;"
        "mov    DWORD PTR [ebp-0x10],0x24b;"
        "mov    DWORD PTR [ebp-0xc],0x0;"
        "jmp    _asm_31;"
    "_asm_27:"
        "add    DWORD PTR [ebp-0xc],0x1;"
    "_asm_31:"
        "mov    edx,DWORD PTR [ebp-0xc];"
        "mov    eax,DWORD PTR [ebp+0x8];"
        "add    eax,edx;"
        "movzx  eax,BYTE PTR [eax];"
        "test   al,al;"
        "jne    _asm_27;"
        "mov    DWORD PTR [ebp-0x8],0x1;"
        "jmp    _asm_142;"
    "_asm_55:"
        "mov    edx,DWORD PTR [ebp-0x8];"
        "mov    eax,DWORD PTR [ebp+0x8];"
        "add    eax,edx;"
        "movzx  eax,BYTE PTR [eax];"
        "movsx  edx,al;"
        "mov    eax,DWORD PTR [ebp-0x8];"
        "lea    ecx,[eax-0x1];"
        "mov    eax,DWORD PTR [ebp+0x8];"
        "add    eax,ecx;"
        "movzx  eax,BYTE PTR [eax];"
        "movsx  eax,al;"
        "sub    edx,eax;"
        "mov    eax,edx;"
        "mov    edx,eax;"
        "mov    eax,DWORD PTR [ebp-0x10];"
        "lea    ebx,[edx+eax*1];"
        "mov    eax,DWORD PTR [ebp-0x8];"
        "lea    edx,[eax+0x1];"
        "mov    eax,DWORD PTR [ebp+0x8];"
        "add    eax,edx;"
        "movzx  eax,BYTE PTR [eax];"
        "movsx  edx,al;"
        "mov    ecx,DWORD PTR [ebp-0x8];"
        "mov    eax,DWORD PTR [ebp+0x8];"
        "add    eax,ecx;"
        "movzx  eax,BYTE PTR [eax];"
        "movsx  eax,al;"
        "sub    edx,eax;"
        "mov    eax,edx;"
        "add    eax,ebx;"
        "mov    DWORD PTR [ebp-0x10],eax;"
        "add    DWORD PTR [ebp-0x8],0x1;"
    "_asm_142:"
        "mov    eax,DWORD PTR [ebp-0xc];"
        "sub    eax,0x1;"
        "cmp    DWORD PTR [ebp-0x8],eax;"
        "jl     _asm_55;"
        "mov    eax,DWORD PTR [ebp-0x10];"
        "add    esp,0x10;"
        "pop    ebx;"
        //"pop    ebp;"
        //"ret    ;"
        "nop;"
        "nop;"
        "nop;"
            :"=r"(value)
            : [pInput] "m"(in)
    );
    
    return value;
}

int main(int argc, char** argv)
{
    printf("0x%x\n", asm4("picoCTF_3de4a"));
    
    return 0;
}
```

ジャンプ命令をラベルに変更、入力パラメータの名前もレジスター名から変更。関数のセットアップと解放処理はコンパイラーによって処理されるため、アセンブリー内ではコメントアウト。  
GCCのドキュメントや各種サイトの情報にもとづいて、お作法通りに記述したものになる。  

このC言語コードをsolver.cとして保存し、gccコマンドでコンパイルする。  

```
$ gcc -masm=intel -m32 solver.c -o solver
```

以下のエラーが出力された。  

```
$ gcc -masm=intel -m32 solver.c -o solver
In file included from solver.c:1:
/usr/include/stdio.h:28:10: fatal error: bits/libc-header-start.h: No such file or directory
   28 | #include <bits/libc-header-start.h>
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~
compilation terminated.
```

gcc-multilibが必要なため、インストールする。  

```
$ sudo apt install gcc-multilib
```

gcc-multilibをインストール後、改めてコンパイルする。  
作成された実行ファイルsolverを実行する。  

```
$ ./solver
0x207
```

この「0x20c」がフラグになる。  
この問題は、「pciCTF{}」を付けず、この値をそのまま入力する内容になっている。  

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## フラグ  

> 0x207  
