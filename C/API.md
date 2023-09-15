##### malloc()

> 申请一块连续的指定大小(字节)的内存块(堆)区域，以void*类型返回分配的内存区域地址

```c
void* = malloc(size_t size);
void* = malloc(字节数);
```

###### 实例

```c
// 定义一个int类型的指针p
int *p;
// 强制类型转换为int类型的指针，sizeof(数据类型)返回size_t类型的值，表示申请int大小(四个字节)的空间
p = (int *)malloc(sizeof(int));
```



##### fread()

> 从文件读取数据到内存，注意配合fclose(文件指针)

```c
size_t = fread(void *ptr, size_t size, size_t count, FILE *stream);
size_t = fread(指向存储读取数据的内存指针, 数据项大小(单位字节), 读取数据项数量, 要读取文件的指针);
```

###### 实例

```c
// 初始化整型变量n为500kb
int n = 500 * pow(2, 10);
// 定义char指针res
char* res;
// 打开名为test.txt的文件
FILE* file = fopen("test.txt", "r");
// 异常处理，判断是否成功打开该文件
if (file == NULL) {
	printf("文件未找到\n");
}
res2 = (char*)malloc(n);
// 从file指针指向文件中读取n个字节，保存到指针res指向的内存地址
fread(res, sizeof(char), n, file);
// 关闭流
fclose(file);
```



##### strncpy()

> 将一个字符串的一部分或整个字符串复制到另一个字符串中

```c
char* strncpy(char* destination, const char* source, size_t num);
```

- `destination`：目标字符串的指针，用于存储复制后的字符串
- `source`：源字符串的指针，即要复制的字符串
- `num`：要复制的字符数
