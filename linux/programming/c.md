# c PROGRAMMING @ LINUX==使用gcc
```
GCC 編譯器基本使用教學與範例
https://blog.gtwang.org/programming/gcc-comipler-basic-tutorial-examples/
```

```
# 編譯 C 程式，指定輸出檔名
gcc -o hello hello.c

# 執行編譯好的程式
./hello
```
```
使用 gcc 自製 C/C++ 靜態、共享與動態載入函式庫教學
2017/02/03
https://blog.gtwang.org/programming/howto-create-library-using-gcc/
```
```
C 語言動態記憶體配置教學：malloc、free 等函數
https://blog.gtwang.org/programming/c-memory-functions-malloc-free/

```
```
C 語言 fork 使用教學與範例，多行程 Multi-Process 平行化程式設計
https://blog.gtwang.org/programming/c-fork-tutorial-multi-process-programming/
```
```
C/C++ 程式設計教學：main 函數讀取命令列參數，argc 與 argv 用法
https://blog.gtwang.org/programming/c-cpp-tutorial-argc-argv-read-command-line-arguments/
```

#
```
圖說演算法：使用C語言
書號：MP21816	作者：吳燦銘、胡昭民

http://www.drmaster.com.tw/Bookinfo.asp?BookID=MP21816
```

```
第1章 進入演算法的世界
1-1 生活中到處都是演算法
1-2 常見演算法簡介

第2章 常用的資料結構
2-1 認識資料結構
2-2 資料結構的種類
2-3 樹狀結構
2-4 圖形簡介
2-5 雜湊表

第3章 排序演算法
3-1 認識排序
3-2 氣泡排序法
3-3 選擇排序法
3-4 插入排序法
3-5 謝耳排序法
3-6 合併排序法
3-7 快速排序法
3-8 基數排序法

第4章 搜尋與雜湊演算法
4-1 常見搜尋法介紹
4-2 常見的雜湊法簡介
4-3 碰撞與溢位處理

第5章 陣列與鏈結串列演算法
5-1 矩陣
5-2 建立單向鏈結串列

第6章 堆疊與佇列演算法
6-1 陣列實作堆疊
6-2 鏈結串列實作堆疊
6-3 河內塔演算法
6-4 八皇后演算法
6-5 陣列實作佇列
6-6 鏈結串列實作佇列
6-7 雙向佇列
6-8 優先佇列

第7章 樹狀演算法
7-1 陣列實作二元樹
7-2 鏈結串列實作二元樹
7-3 二元樹走訪
7-4 二元樹節點搜尋
7-5 二元樹節點插入
7-6 二元樹節點的刪除
7-7 堆積樹排序法 4

第8章 圖形演算法
8-1 圖形的走訪
8-2 最小花費擴張樹（MST）
8-3 圖形最短路徑法
```
#
```
#include <stdio.h>
#include <stdlib.h>

int fib(int);			/* fib()函數的原型宣告 */

int main(void)
{
   int i,n;
   printf("請輸入要計算到第幾個費式數列:");
   scanf("%d",&n); 
   
   for(i=0;i<=n;i++)			/* 計算前1n個費氏數列 */
      printf("fib(%d)=%d\n",i,fib(i));		

   
   return 0;
}

int fib(int n) 		/* 定義函數fib()*/
{
    	
   if (n==0)
      return 0; /* 如果n=0 則傳回 0*/ 
   else if(n==1 || n==2)	/* 如果n=1或n=2，則傳回1 */
      return 1;
   else				/* 否則傳回 fib(n-1)+fib(n-2) */
      return (fib(n-1)+fib(n-2));
}

```


```
/* 以for迴圈計算 n! */
#include<stdio.h>
#include<stdlib.h>

int main()
{ 
	int i,j,n,sum = 1;
	printf("請輸入n="); 
	scanf("%d",&n);
	
	for(i=0;i<=n;i++)	 /* 0~4階層 */
	{  
	   for(j=i;j>0;j--) /* n!=n*(n-1)*(n-2)*...*1 */
	   sum *= j;		 /* sum=sum*j */
	   printf("%d!=%3d\n",i,sum);
	   sum	= 1;
	}
	return 0;
}

```

第3章 排序演算法

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int i,j,tmp;
	int data[8]={16,25,39,27,12,8,45,63};	/* 原始資料 */
	printf("氣泡排序法：\n原始資料為：");
	for (i=0;i<8;i++)
		printf("%3d",data[i]);
	printf("\n");

	for (i=7;i>=0;i--)		/* 掃瞄次數 */
	{
		for (j=0;j<i;j++)/*比較、交換次數*/
		{
			if (data[j]>data[j+1])	/* 比較相鄰兩數，如第一數較大則交換 */
			{
				tmp=data[j];
				data[j]=data[j+1];
				data[j+1]=tmp;
			}
		}
		printf("第 %d 次排序後的結果是：",8-i); /*把各次掃描後的結果印出*/
		for (j=0;j<8;j++)
			printf("%3d",data[j]);
		printf("\n");
	}
	printf("排序後結果為：");
	for (i=0;i<8;i++)
		printf("%3d",data[i]);
	printf("\n");
	
    system("pause");
	return 0;
}
```


```
#include <stdio.h>
#include <stdlib.h>

void select (int *);     /*宣告排序法副程序*/
void showdata (int *);   /*宣告列印陣列副程序*/

int main()
{
	int data[8]={16,25,39,27,12,8,45,63};
	printf("原始資料為：");
	int i;
	for (i=0;i<8;i++)
	    printf("%3d",data[i]);
	printf("\n-------------------------------------");
	select (data);
	printf("排序後資料：");
	for (i=0;i<8;i++)
	    printf("%3d",data[i]);
    printf("\n");
    
	
	return 0;
}

void showdata (int data[])
{
	int i;
	for (i=0;i<8;i++)
	    printf("%3d",data[i]);
	printf("\n");
}

void select (int data[])
{
	int i,j,tmp,k;
	for(i=0;i<7;i++)    /*掃描5次*/
	{   
		for(j=i+1;j<8;j++)  /*由i+1比較起，比較5次*/
		{	
			if(data[i]>data[j])  /*比較第i及第j個元素*/
			{	
			    tmp=data[i];
			    data[i]=data[j];
			    data[j]=tmp;	
			}
		}
	}
	printf("\n");
}

```

```


```


```


```

```


```


```


```
