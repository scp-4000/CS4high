#
```
圖說演算法: 使用C++
MP21827	作者：吳燦銘, 胡昭民

http://www.drmaster.com.tw/Bookinfo.asp?BookID=MP21827
```
```
第1章 大話運算思維與程式設計
1-1 程式設計的速效攻略
1-2 生活中到處都是演算法
1-3 程式設計邏輯簡介
1-4 C++的物件導向DNA

第2章 地表上最常見經典演算法
2-1 分治演算法
2-2 遞迴演算法
2-3 動態規劃演算法
2-4 不斷繞圈的疊代演算法
2-5 人人都有份的枚舉演算法
2-6 不對就回頭的回溯法
2-7 給我最好，其餘免談的貪心法

第3章 走入資料結構的異想世界
3-1 資料結構初體驗
3-2 超人氣資料結構簡介
3-3 盤根錯節的樹狀結構
3-4 學會藏寶圖的密技-圖形簡介
3-5 神奇有趣的雜湊表

第4章 新手快速學會的最夯排序演算法
4-1 看懂排序
4-2 氣泡排序法
4-3 選擇排序法
4-4 插入排序法
4-5 謝耳排序法
4-6 快速排序法
4-7 合併排序法
4-8 基數排序法
4-9 堆積樹排序法

第5章 搜尋演算法
5-1 常見的搜尋方法
5-2 循序搜尋演算法
5-3 二分搜尋演算法
5-4 內插搜尋法
5-5 費氏搜尋演算法

第6章 全方位應用的陣列與串列演算法
6-1 矩陣演算法與深度學習
6-2 陣列與多項式
6-3 徹底玩轉單向串列演算法
6-4 串列與多項式

第7章 實戰安全性演算法
7-1 輕鬆學會資料加密
7-2 一學就懂的雜湊演算法
7-3 破解碰撞與溢位處理

第8章 堆疊與佇列演算法徹底研究
8-1 陣列實作堆疊輕鬆學
8-2 串列實作堆疊
8-3 古老的河內塔演算法
8-4 八皇后演算法
8-5 陣列實作佇列
8-6 串列實作佇列
8-7 有趣的雙向佇列
8-8 一定有懂得優先佇列

第9章 超圖解的樹狀演算法
9-1 陣列實作二元樹
9-2 串列實作二元樹
9-3 二元樹走訪的入門捷徑
9-4 話說二元搜尋樹
9-5 二元樹節點插入
9-6 二元樹節點刪除
9-7 二元運算樹
9-8 二元排序樹
9-9 引線二元樹的奧秘
9-10延伸二元樹入門
9-11霍夫曼樹特訓班
9-12平衡樹
9-13決策樹的智慧

第10 章圖形演算法
10-1圖形的資料表示法
10-2圖形的走訪
10-3擴張樹的奧秘
10-4 圖形最短路徑法
```
# 第2章 地表上最常見經典演算法
### 費伯那序列的遞迴程式
```
#include<iostream>
using namespace std;

int fib(int);	//fib()函數的原型宣告 

int main()
{
    int i,n;
    cout<<"請輸入所要計算第幾個費式數列:";
    cin>>n;
    for(i=0;i<=n;i++) // 計算前1n個費氏數列 
		cout<<"fib("<<i<<")="<<fib(i)<<endl;
    return 0;
}

int fib(int n) 	
{
    	
    if (n==0)
        return 0; 
    else if(n==1 || n==2)	
        return 1;
    else		
        return (fib(n-1)+fib(n-2));
}
```

```
//計算10! 的值
#include <iostream>
#include <cstdlib>
using namespace std;

int main()
{
    int i,sum=1;
    for (i=1;i<=10;i++)  //定義for迴圈
    {
        sum*=i;   //sum=sum+*i
    } 
    cout<<i-1<<"!="<<sum<<endl;  //印出i和sum的值 
    return 0;
}
```
```
#include <iostream>
#include <cstdlib>

using namespace std;

int main()
{
	int x=1, sum=1000;
	while(sum>0) //while迴圈 
    {
	    sum-=x;
	    x++;
	}
	cout<<x-1<<endl;
	
    return 0;	
}
```

```
#include <iostream>
#include <math.h>

using namespace std;

bool is_prime(int n)
{
	int i=2;
	while (i<=n)
	{
		if(n%i==0) //如果整除,i是n的因數,回傳 false
		    return false;
		i=i+1;
		return true;
	}
}
int main()
{
	int n;
	cout<<"請輸入一個大於等於2的數字: "; 
	cin>>n;
	cout<<endl;
	if(n==2)
	{ 
	    cout<<n<<"是質數";
	    return 0;
	} 
	if(is_prime(n))
	    cout<<n<<"是質數";
	else
	    cout<<n<<"不是質數";

    return 0;	
}

```
#  第4章 新手快速學會的最夯排序演算法

```
#include <iostream>
#include <iomanip>
using namespace std;
int main(void)
{
    int data[6]={6,5,9,7,2,8};	// 原始資料 
    cout<<"氣泡排序法：\n原始資料為：";
	for (int i=0;i<6;i++)
	    cout<<setw(3)<<data[i];
	cout<<endl;

	for (int i=5;i>0;i--)// 掃瞄次數 
	{
		for (int j=0;j<i;j++)//比較、交換次數
		{
			if (data[j]>data[j+1])// 比較相鄰兩數，如第一數較大則交換 
			{
				int tmp;
				tmp=data[j];
				data[j]=data[j+1];
				data[j+1]=tmp;
			}
		}
		cout<<"第 "<<6-i<<" 次排序後的結果是："; //把各次掃描後的結果印出
		for (int j=0;j<6;j++)
			cout<<setw(3)<<data[j];
		cout<<endl;
	}
	cout<<"排序後結果為：";
	for (int i=0;i<6;i++)
		cout<<setw(3)<<data[i];
	cout<<endl;
	return 0;
}

```

```
#include <iomanip>
using namespace std;
void bubble (int *);   //宣告氣泡排序副程式
void showdata (int *); //宣告列印陣列副程式
int main(void)
{
    int data[6]={4,6,2,7,8,9}; //原始資料
    cout<<"改良氣泡排序法\n原始資料為：\t";
    showdata(data);
    bubble(data);
    return 0;
}
void showdata (int data[]) //利用迴圈列印資料
{
	for (int i=0;i<6;i++)
		cout<<setw(3)<<data[i];
	cout<<endl;
}
void bubble (int data[])
{
	for(int i=5;i>=0;i--)
	{
		int flag=0;  //flag用來判斷是否有執行交換的動作
		for (int j=0;j<i;j++)
		{
			if (data[j+1]<data[j])
			{
				int tmp;
				tmp=data[j];
				data[j]=data[j+1];
				data[j+1]=tmp;
				flag++;    //如果有執行過交換，則flag不為0
			}
		}
		if (flag==0)
			break;
		/*
		當執行完一次掃描就判斷是否做過交換動作，如果沒有交換過資料
		，表示此時陣列已完成排序，故可直接跳出迴圈
		*/
		cout<<"第 "<<6-i<<" 次排序：\t";
		for (int j=0;j<6;j++)
			cout<<setw(3)<<data[j];
		cout<<endl;		    
	}
	cout<<"排序後結果為：\t";
	showdata (data);
}
```

```

```
