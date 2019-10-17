#
```
圖說演算法：使用Python
書號：MP21811	作者：吳燦銘、胡昭民
http://www.drmaster.com.tw/Bookinfo.asp?BookID=MP21811
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

# 第1章
```
def fib(n):	# 定義函數fib()
    if n==0 :
        return 0 # 如果n=0 則傳回 0
    elif n==1 or n==2:
        return 1
    else:   # 否則傳回 fib(n-1)+fib(n-2)
        return (fib(n-1)+fib(n-2))

n=int(input('請輸入所要計算第幾個費式數列:'))
for i in range(n+1):# 計算前n個費氏數列
    print('fib(%d)=%d' %(i,fib(i)))

```

```
# 以for迴圈計算 n! 
sum = 1
n=int(input('請輸入n='))
for i in range(0,n+1):
    for j in range(i,0,-1):
        sum *= j    # sum=sum*j
    print('%d!=%3d' %(i,sum))
    sum=1
```

# 第3章 排序演算法
```
data=[16,25,39,27,12,8,45,63]	# 原始資料 
print('氣泡排序法：原始資料為：')
for i in range(8):
    print('%3d' %data[i],end='')
print()

for i in range(7,-1,-1): #掃描次數
    for j in range(i):
        if data[j]>data[j+1]:#比較,交換的次數
            data[j],data[j+1]=data[j+1],data[j]#比較相鄰兩數,如果第一數較大則交換
    print('第 %d 次排序後的結果是：' %(8-i),end='') #把各次掃描後的結果印出
    for j in range(8):
        print('%3d' %data[j],end='')
    print()
	
print('排序後結果為：')
for j in range(8):
    print('%3d' %data[j],end='')
print()

```

```
def showdata (data):
    for i in range(8):
        print('%3d' %data[i],end='')
    print()

def select (data):
    for i in range(7):
        for j in range(i+1,8):
            if data[i]>data[j]: #比較第i及第j個元素
                data[i],data[j]=data[j],data[i]
    print()

data=[16,25,39,27,12,8,45,63]
print('原始資料為：')
for i in range(8):
    print('%3d' %data[i],end='')
print('\n-------------------------------------')
select(data)
print("排序後資料：")
for i in range(8):
    print('%3d' %data[i],end='')
print('')
```

# 第4章 搜尋與雜湊演算法
```
import random

val=0
data=[0]*80
for i in range(80):
    data[i]=random.randint(1,150)
while val!=-1:
    find=0
    val=int(input('請輸入搜尋鍵值(1-150)，輸入-1離開：'))
    for i in range(80):
        if data[i]==val:
            print('在第 %3d個位置找到鍵值 [%3d]' %(i+1,data[i]))
            find+=1
    if find==0 and val !=-1 :
        print('######沒有找到 [%3d]######' %val)
print('資料內容：')
for i in range(10):
    for j in range(8):
        print('%2d[%3d]  ' %(i*8+j+1,data[i*8+j]),end='')
    print('')

```
### 二元搜尋法

```
import random

def bin_search(data,val):
    low=0
    high=49
    while low <= high and val !=-1:
        mid=int((low+high)/2)
        if val<data[mid]:
            print('%d 介於位置 %d[%3d]及中間值 %d[%3d]，找左半邊' \
                   %(val,low+1,data[low],mid+1,data[mid]))
            high=mid-1
        elif val>data[mid]:
            print('%d 介於中間值位置 %d[%3d] 及 %d[%3d]，找右半邊' \
                  %(val,mid+1,data[mid],high+1,data[high]))
            low=mid+1
        else:
            return mid
    return -1

val=1
data=[0]*50
for i in range(50):
    data[i]=val
    val=val+random.randint(1,5)

while True:
    num=0
    val=int(input('請輸入搜尋鍵值(1-150)，輸入-1結束：'))
    if val ==-1:
        break
    num=bin_search(data,val)
    if num==-1:
        print('##### 沒有找到[%3d] #####' %val)
    else:
        print('在第 %2d個位置找到 [%3d]' %(num+1,data[num]))

print('資料內容：')
for i in range(5):
    for j in range(10):
        print('%3d-%-3d' %(i*10+j+1,data[i*10+j]), end='')
    print()
```

#
```


```

```

```

