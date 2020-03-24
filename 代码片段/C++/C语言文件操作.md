# C语言文件操作

|    文件     |                                 硬件设备                                  |
| ---------- | ----------------------------------------------------------------------- |
| stdin      | 	标准输入文件，一般指键盘；scanf()、getchar() 等函数默认从 stdin 获取输入。     |
| stdout     | 	标准输出文件，一般指显示器；printf()、putchar() 等函数默认向 stdout 输出数据。 |
| stderr	 | 标准错误文件，一般指显示器；perror() 等函数默认向 stderr 输出数据（后续会讲到）。 |
| stdprn	 | 标准打印文件，一般指打印机。                                                 |

## fopen

`以只读的方式打开文件`

```
FILE *fp = fopen("demo.txt", "r");
```

**控制读写权限的字符串**

| 打开方式 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| "r"      | 以“只读”方式打开文件。只允许读取，不允许写入。文件必须存在，否则打开失败。 |
| "w"      | 以“写入”方式打开文件。如果文件不存在，那么创建一个新文件；如果文件存在，那么清空文件内容（相当于删除原文件，再创建一个新文件）。 |
| "a"      | 以“追加”方式打开文件。如果文件不存在，那么创建一个新文件；如果文件存在，那么将写入的数据追加到文件的末尾（文件原有的内容保留）。 |
| "r+"     | 以“读写”方式打开文件。既可以读取也可以写入，也就是随意更新文件。文件必须存在，否则打开失败。 |
| "w+"     | 以“写入/更新”方式打开文件，相当于`w`和`r+`叠加的效果。既可以读取也可以写入，也就是随意更新文件。如果文件不存在，那么创建一个新文件；如果文件存在，那么清空文件内容（相当于删除原文件，再创建一个新文件）。 |
| "a+"     | 以“追加/更新”方式打开文件，相当于a和r+叠加的效果。既可以读取也可以写入，也就是随意更新文件。如果文件不存在，那么创建一个新文件；如果文件存在，那么将写入的数据追加到文件的末尾（文件原有的内容保留）。 |



**控制读写方式的字符串**

| 打开方式 | 说明                              |
| -------- | --------------------------------- |
| "t"      | 文本文件。如果不写，默认为`"t"`。 |
| "b"      | 二进制文件。                      |

关闭文件

```C++
int fclose(FILE *fp);
```



## fgetc

`以字符的方式读取文件`

```C++
int fgetc (FILE *fp);
```

示例

```C++
#include<stdio.h>
int main(){
    FILE *fp;
    char ch;
   
    //如果文件不存在，给出提示并退出
    if( (fp=fopen("D:\\demo.txt","rt")) == NULL ){
        puts("Fail to open file!");
        exit(0);
    }
    //每次读取一个字节，直到读取完毕
    while( (ch=fgetc(fp)) != EOF ){
        putchar(ch);
    }
    putchar('\n');  //输出换行符
    fclose(fp);
    return 0;
}
```



## feof

`判断文件内部指针是否指向了文件末尾`

```C++
int feof ( FILE * fp );
```



## ferror

`判断文件操作是否出错`

```C++
int ferror ( FILE *fp );
```

```C++
#include<stdio.h>
int main(){
    FILE *fp;
    char ch;
  
    //如果文件不存在，给出提示并退出
    if( (fp=fopen("D:\\demo.txt","rt")) == NULL ){
        puts("Fail to open file!");
        exit(0);
    }
    //每次读取一个字节，直到读取完毕
    while( (ch=fgetc(fp)) != EOF ){
        putchar(ch);
    }
    putchar('\n');  //输出换行符
    if(ferror(fp)){
        puts("读取出错");
    }else{
        puts("读取成功");
    }
    fclose(fp);
    return 0;
}
```



## fgetc

`向指定的文件中写入一个字符`

```C++
#include<stdio.h>
int main(){
    FILE *fp;
    char ch;
    //判断文件是否成功打开
    if( (fp=fopen("D:\\demo.txt","wt+")) == NULL ){
        puts("Fail to open file!");
        exit(0);
    }
    printf("Input a string:\n");
    //每次从键盘读取一个字符并写入文件
    while ( (ch=getchar()) != '\n' ){
        fputc(ch,fp);
    }
    fclose(fp);
    return 0;
}
```



## fread

`用来从指定文件中读取块数据。所谓块数据，也就是若干个字节的数据，可以是一个字符，可以是一个字符串，可以是多行数据，并没有什么限制。`

```
size_t fread ( void *ptr, size_t size, size_t count, FILE *fp );
```



## fwrite

`用来向文件中写入块数据`

```
size_t fwrite ( void * ptr, size_t size, size_t count, FILE *fp );
```

- ptr 为内存区块的[指针](http://c.biancheng.net/c/80/)，它可以是数组、变量、结构体等。fread() 中的 ptr 用来存放读取到的数据，fwrite() 中的 ptr 用来存放要写入的数据。
- size：表示每个数据块的字节数。
- count：表示要读写的数据块的块数。
- fp：表示文件指针。