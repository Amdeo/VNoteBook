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

## fgets

```C++
#include <stdio.h>
char *fgets(char *str, int n, FILE *stream);
```

使用 
```C++
char a[10];
fgets(a,10,stdin) # 获取键盘输入
fgets(a,10,stdout) # 获取终端输出内容
fgets(a,10,fp) # 获取文件内容
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

## fputs

`字符写入函数`

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

```C++
#include<stdio.h>
#define N 5
int main(){
    //从键盘输入的数据放入a，从文件读取的数据放入b
    int a[N], b[N];
    int i, size = sizeof(int);
    FILE *fp;
    if( (fp=fopen("D:\\demo.txt", "rb+")) == NULL ){  //以二进制方式打开
        puts("Fail to open file!");
        exit(0);
    }
  
    //从键盘输入数据 并保存到数组a
    for(i=0; i<N; i++){
        scanf("%d", &a[i]);
    }
    //将数组a的内容写入到文件
    fwrite(a, size, N, fp);
    //将文件中的位置指针重新定位到文件开头
    rewind(fp);
    //从文件读取内容并保存到数组b
    fread(b, size, N, fp);
    //在屏幕上显示数组b的内容
    for(i=0; i<N; i++){
        printf("%d ", b[i]);
    }
    printf("\n");
    fclose(fp);
    return 0;
}
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



## fscanf

## fprintf

格式化读写文件

```
int fscanf ( FILE *fp, char * format, ... );
int fprintf ( FILE *fp, char * format, ... );
```

```C++
#include<stdio.h>
#define N 2
struct stu{
    char name[10];
    int num;
    int age;
    float score;
} boya[N], boyb[N], *pa, *pb;
int main(){
    FILE *fp;
    int i;
    pa=boya;
    pb=boyb;
    if( (fp=fopen("D:\\demo.txt","wt+")) == NULL ){
        puts("Fail to open file!");
        exit(0);
    }
    //从键盘读入数据，保存到boya
    printf("Input data:\n");
    for(i=0; i<N; i++,pa++){
        scanf("%s %d %d %f", pa->name, &pa->num, &pa->age, &pa->score);   
    }
    pa = boya;
    //将boya中的数据写入到文件
    for(i=0; i<N; i++,pa++){
        fprintf(fp,"%s %d %d %f\n", pa->name, pa->num, pa->age, pa->score);   
    }
    //重置文件指针
    rewind(fp);
    //从文件中读取数据，保存到boyb
    for(i=0; i<N; i++,pb++){
        fscanf(fp, "%s %d %d %f\n", pb->name, &pb->num, &pb->age, &pb->score);
    }
    pb=boyb;
    //将boyb中的数据输出到显示器
    for(i=0; i<N; i++,pb++){
        printf("%s  %d  %d  %f\n", pb->name, pb->num, pb->age, pb->score);
    }
    fclose(fp);
    return 0;
}
```

## 随机读写文件

随意读写内容

`  用来将位置指针移动到文件开头 `

```
void rewind ( FILE *fp );
```

` 用来将位置指针移动到任意位置 `

```
int fseek ( FILE *fp, long offset, int origin );
```



` 在移动位置指针之后，就可以用前面介绍的任何一种读写函数进行读写了。由于是二进制文件，因此常用 fread() 和 fwrite() 读写。 `

```C++
#include<stdio.h>
#define N 3
struct stu{
    char name[10]; //姓名
    int num;  //学号
    int age;  //年龄
    float score;  //成绩
}boys[N], boy, *pboys;
int main(){
    FILE *fp;
    int i;
    pboys = boys;
    if( (fp=fopen("d:\\demo.txt", "wb+")) == NULL ){
        printf("Cannot open file, press any key to exit!\n");
        getch();
        exit(1);
    }
    printf("Input data:\n");
    for(i=0; i<N; i++,pboys++){
        scanf("%s %d %d %f", pboys->name, &pboys->num, &pboys->age, &pboys->score);
    }
    fwrite(boys, sizeof(struct stu), N, fp);  //写入三条学生信息
    fseek(fp, sizeof(struct stu), SEEK_SET);  //移动位置指针
    fread(&boy, sizeof(struct stu), 1, fp);  //读取一条学生信息
    printf("%s  %d  %d %f\n", boy.name, boy.num, boy.age, boy.score);
    fclose(fp);
    return 0;
}
```

获取文件的大小

```
long int ftell ( FILE * fp );
```

- 先使用fseek将文件指针定位到文件末尾，在使用ftell() 返回内部指针距离文件开头第字节数，这个返回值hi等于文件的大小

```C++
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
long fsize(FILE *fp);
int main(){
    long size = 0;
    FILE *fp = NULL;
    char filename[30] = "D:\\1.mp4";
    if( (fp = fopen(filename, "rb")) == NULL ){  //以二进制方式打开文件
        printf("Failed to open %s...", filename);
        getch();
        exit(EXIT_SUCCESS);
    }
   
    printf("%ld\n", fsize(fp));
    return 0;
}
long fsize(FILE *fp){
    long n;
    fpos_t fpos;  //当前位置
    fgetpos(fp, &fpos);  //获取当前位置
    fseek(fp, 0, SEEK_END);
    n = ftell(fp);
    fsetpos(fp,&fpos);  //恢复之前的位置
    return n;
}
```

