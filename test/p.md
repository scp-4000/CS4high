# 第4章 絕對的基礎

### 4.1 縮排及區塊結構

```
/* 以下是 C 程式碼 */
int n,r;
n=9;
r=1;
while ( n > 0 ){
    r *= n;
    n--;
}
```

```
/* 以下是任意縮排的 C 程式碼*/
    int n,r;
       n=9;
       r=1;
   while ( n > 0 ){
r *= n;
n--;
}
```
```
# 這是 python 程式碼
n = 9
r = 1
while n > 0 :
    r = r * n  <-----Python 也支援類似 C 的語法 : r *= n
    n = n - 1  <-----Python 也支援類似 C 的語法 : n -= 1
```

```
for i in range(1 , 10):
    for j in range(1 , 10):
        print(f'{j}x{i}={j*i:2d}', end=' ')  <----這行屬於第二個迴圈
    print()  <------這行屬於第一個迴圈

```

```
    多了一個空格會出現 unexpected indent
>>> a=2
    File "<stdin>", line 1
        a=2
        ^
IndentationError: unexpcted indent
```
##### 但在 Iptython 環境下並不會發生錯誤

```
In[1]; a=2  <----- 前面多一個空格在 Iptython 不會出現錯誤訊息
```


### 4.2 註解
```
# 設定 x 變數的值為 5
x = 5
x = 3   # 現在 x 變數值等於 3
x = "# This is not a comment"  <-------此行的 # 只是字串中的一個字元
```

### 4.3 變數及其設定

``` 
x = 5
```

```
>>> x  = "Hello" <---建立字串物件 "Hello" ，　讓變數 x 參照到該物件
>>> print(x)
Hello

>>> x = 5   <--------建立整數物件 5 ，讓變數 x 參照到該物件
>>> x
5
```
```
>>> x = 5
>>>print(x)
5

>>> del x
>>> print(x)
Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
NameError : name'x' is not defined
>>>
```
### 4.4 運算式
```
x = 3
y = 5
z = (x + y) / 2
```
```
>>> 3 / 2
1.5
>>> 3 // 2
1
>>> -1 // 2
-1     <--------------- -1 除以 2 等於 -0.5 ， 而小於 -0.5 的最大整數為 -1 。
                           注意!! 不是四捨五入喔!!
```
### 4.5 字串
```
x = "Hello, World"
```
```
x = "\t 這個字串開頭是一個 \"tab\" 字元."
x = "這個字串包含一個反斜線 (\\) 字元."
```
```
x = "Hello , world"
x = "Hello , world'
```
```
x = ' you can leave the " alone'
x = ' Don't need a backslash"
x = ' Can \'t get by without a backslash'
x = " Backslash your \" character!"
```
##### 不能將字串拆成多行 以下程式碼無法正常操作
```
x = This is a misguided attempt to
put a newline into a string without using backslash-n"
```

```
x = """Starting and ending a string with triple " characters permits embedded newlines , and the use of " and ' without backslashes"""
```

### 4.6 數字
```
>>> 5 + 2 - 3 * 2 
1

>>> 5 / 2  # 除法(/)運算結果為浮點數
2.5

>>> 5 / 2.0
2.5

>>> 5 // 2 # 使用(//)除法的結果是小於商數的最大整數
2

>>> 5.0  // 2 # 5.0是浮點數，所以運算結果變成浮點數
2.0

>>> 3000000000 # 很多程式語言中這個數值通常會超出整數型別的範圍
3000000000

>>> 3000000000 * 3 
9000000000

>>> 3000000000 *3.0  #3.0是浮點數 所以結果是浮點數
9000000000.0

>>> 2.0e-8 #用科學計數法表示一個浮點數
2e-08

>>> 3000000 * 3000000
9000000000000

>>> int( 200.2 )
200

>>> int()2e2
200

>>> float (200)
200.0

```
#### 4.6.4 複數
```

>>> (3+2j)
(3+2j)
```
```
>>> 3 + 2j - (4 + 4j)
(-1-2j)  <--------------用括弧表示-1-2j是單一物個件
>>> (1 + 2j) * (3 + 4j)
(-5+10j)
>>> 1j*1j
(-1+0j)
```
```
>>> z = 3+5j
>>> z.real
3.0
>>> z.imag
5.0
```

#### 4.6.5 進階的複數函式

```
>>> import cmath
>>> cmath.sqrt(-1)  <------明確指定要引用cmath 套件中的 sqrt()函式
1j
```


### 4.7 None值

```
>>> None == False
False
>>> None == 0
False
>>> None == None <-----None只等於自己
True
>>> False == 0
True
```

### 4.8 取得使用者的輸入
```
>>> name = input("Name? ")
Name? Jane 
>>> print(name)
Jane  
```
```
>>> age = int(input("Age? "))
Age? 28
>>> print(age)
28
>>>
```

# 第5章 基本資料結構：list、tuple、set

### 5.1 list類似陣列
```
# 建立3個元素的list
x = [1,2,3]
```
```
# 建立 list，包含數字、字串、和另一個list
x = [2,"two",[1,2,3]]
```
```
>>> x = [2, "two", [1, 2, 3]]
>>> len(x)
3
```

### 5.2 list的索引與切片
```
>>> x = ["first", "second", "third", "fourth"]
>>> x[0]
'first'
>>> x[2]
'third'
```
```
>>> a = x[-1]
>>> a
'fourth'
>>> x[-2]
'third'

```
```
>>> x = ["first", "second", "third", "fourth"]    
>>> x[1:-1]
['second', 'third']
>>> x[0:3]
['first', 'second', 'third']
>>> x[-2:-1]
['third']
```
```
>>> x[-1:2]
[]
```
```
>>> x[:3]
['first', 'second', 'third']
>>> x[2:]
['third', 'fourth']
```
```
>>> y = x[:]
>>> y[0] = '1 st'
>>> y
['1 st', 'second', 'third', 'fourth']
>>> x
['first', 'second', 'third', 'fourth']
```
### 5.3 修改list
```
>>> x = [1, 2, 3, 4]
>>> x[1] = "two"
>>> x
[1, 'two', 3, 4]
```
```
>>> x = [0, 1, 2, 3]
>>> x[1:3] = ["one","two"]
>>> x
[0, 'one', 'two', 3]
```
```
>>> x = [0, 1, 2, 3]
>>> x[1:3] = ["one","two","three"]
>>> x
[0, 'one', 'two', 'three', 3]
>>> x [0:4] = ["a", "b"]
>>> x
['a','b',3]
```
```
>>> x = [1, 2, 3, 4]
>>> x[len(x):] = [5, 6, 7]                # 於list最後面附加多個值
>>> x
[1, 2, 3, 4, 5, 6, 7]
>>> x[:0] = [-1, 0]                       # 於list 最前面插入多個值
>>> x
[-1, 0, 1, 2, 3, 4, 5, 6, 7]
>>> x[1:-1] = []                          # 移除list 中多個元素
>>> x
[-1, 7]
```
```
>>> x = [1, 2, 3]
>>> x.append("four")
>>> x
[1, 2, 3, 'four']
```
```
>>> x = [1, 2, 3, 4]
>>> y = [5, 6, 7]
>>> x.append(y)  
>>> x
[1, 2, 3, 4, [5, 6, 7]]
```
```
>>> x = [1, 2, 3, 4]
>>> y = [5, 6, 7]
>>> x.extend(y)  
>>> x
[1, 2, 3, 4, 5, 6, 7]  
```
```
>>> x = [1, 2, 3]
>>> x.insert(2, "hello")
>>> print(x)
[1, 2, 'hello', 3]
>>> x.insert(0, "start")
>>> print(x)
['start', 1, 2, 'hello', 3]
```
```
>>> x = [1, 2, 3]
>>> x.insert(-1, "hello")
>>> print(x)
[1, 2, 'hello', 3]
```
```

>>> x = ['a', 2, 'c', 7, 9, 11]
>>> del x[1]
>>> x
['a', 'c', 7, 9, 11]
>>> del x[:2]
>>> x
[7, 9, 11]
```
```
>>> x = [1, 2, 3, 4, 3, 5]
>>> x.remove(3)
>>> x
[1, 2, 4, 3, 5]
>>> x.remove(3)
>>> x
[1, 2, 4, 5]
>>> x.remove(3)
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: list.remove(x): x not in list
```
```
>>> x = [1, 3, 5, 6, 7]
>>> x.reverse()
>>> x
[7, 6, 5, 3, 1]
```

### 5.4 list的排序
```
>>> x = [3, 8, 4, 0, 2, 1]
>>> x.sort()
>>> x
[0, 1, 2, 3, 4, 8]
```
```
>>> x = [2, 4, 1, 3]
>>> y = x[:]
>>> y.sort()
>>> y
[1, 2, 3, 4]
>>> x
[2, 4, 1, 3]
```
```
>>> x = ["Life", "Is", "Enchanting"]
>>> x.sort()
>>> x
['Enchanting', 'Is', 'Life']
```
```
>>> x = [1, 2, 'hello', 3]
>>> x.sort()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<' not supported between instances of 'str' and 'int'

```
```
>>> x = [[3, 5], [2, 9], [2, 3], [4, 1], [3, 2]]
>>> x.sort()
>>> x
[[2, 3], [2, 9], [3, 2], [3, 5], [4, 1]]
```
```
>>> x = [[3, 5], [2, 9], [2, 3], [4, 1], [3, 2]]
>>> x.sort()
>>> x
[[2, 3], [2, 9], [3, 2], [3, 5], [4, 1]]
```
#### 5.4.1 自定義排序
```
def compare_num_of_chars(string1):
    return len(string1)
```
```
>>> def compare_num_of_chars(string1):
...     return len(string1)
>>> word_list = ['Python', 'is', 'better', 'than', 'C']
>>> word_list.sort()
>>> print(word_list)
['C', 'Python', 'better', 'is', 'than']
>>> word_list = ['Python', 'is', 'better', 'than', 'C']
>>> word_list.sort(key=compare_num_of_chars)
>>> print(word_list)
['C', 'is', 'than', 'Python', 'better']

```
#### 5.4.2 sortde()函式
```
>>> x = (4, 3, 1, 2)
>>> y = sorted(x)
>>> y
[1, 2, 3, 4] 
>>> z = sorted(x, reverse=True)
>>> z
[4, 3, 2, 1]
```
### 5.5 其他常用的list操作

#### 5.5.1 使用 in 算符測試 list 的某個元素值是否存在
```

>>> 3 in [1, 3, 4, 5]
True
>>> 3 not in [1, 3, 4, 5]
False
>>> 3 in ["one", "two", "three"]
False
>>> 3 not in ["one", "two", "three"]
True
```
#### 5.5.2 使用 + 算符串聯list
```
>>> z = [1, 2, 3] + [4, 5]
>>> z
[1, 2, 3, 4, 5]
```
#### 5.5.3 使用 * 算符初始化list
```

>>> z = [None] * 4
>>> z
[None, None, None, None]
```
```
>>> z = [3, 1] * 2
>>> z
[3, 1, 3, 1]
```

#### 5.5.4 最小和最大值
```
>>> min([3, 7, 0, -2, 11])
-2
>>> max([4, "Hello", [1, 2]])
Traceback (most recent call last):
  File "<pyshell#58>", line 1, in <module>
    max([4, "Hello",[1, 2]])
TypeError: '>' not supported between instances of 'str' and 'int'
```
#### 5.5.5 用index() 找出元素在list的索引值
```

>>> x = [1, 3, "five", 7, -2]
>>> x.index(7)
3
>>> x.index(5)
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: 5 is not in list
```
#### 5.5.6
```
>>> x = [1, 2, 2, 3, 5, 2, 5]
>>> x.count(2)
3
>>> x.count(5)
2
>>> x.count(4)
0
```
### 5.6 多層list和深層副本
```
>>> m = [[0, 1, 2], [10, 11, 12], [20, 21, 22]]
>>> m[0]
[0, 1, 2]
>>> m[0][1]
1
>>> m[2]
[20, 21, 22]
>>> m[2][2]
22
```
```
>>> nested = [0]
>>> original = [nested, 1]
>>> original 
[[0], 1]
```
```
>>> nested[0] = 'zero'
>>> original
[['zero'], 1]
>>> original[0][0] = 0
>>> nested
[0]
>>> original
[[0], 1]

```
```
>>> nested = [2]
>>> original
[[0], 1]
```
```
>>> original = [[0], 1]
>>> shallow = original[:]
>>> import copy
>>> deep = copy.deepcopy(original)
```
```

>>> shallow[1] = 2
>>> shallow
[[0], 2]
>>> original
[[0], 1]
>>> shallow[0][0] = 'zero'
>>> original
[['zero'], 1]
```
```
>>> deep[0][0] = 5
>>> deep
[[5], 1]
>>> original
[['zero'], 1]
```
### 5.7 tuple

#### 5.7.1 tuple 基礎
```
>>> x = ('a', 'b', 'c')   

>>> x[2]
'c'
>>> x[1:]
('b', 'c')
>>> len(x)
3
>>> max(x)
'c'
>>> min(x)
'a'
>>> 5 in x
False
>>> 5 not in x
True```
```
```
>>> x[2] = 'd'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```
```
>>> x + x
('a', 'b', 'c', 'a', 'b', 'c')
>>> 2 * x
('a', 'b', 'c', 'a', 'b', 'c')
```
```
>>> x[:]
('a', 'b', 'c')
>>> x * 1
('a', 'b', 'c')
>>> x + ()
('a', 'b', 'c')
```
#### 5.7.2 單一元素的tuple 需要加上逗號
```
>>> x = 3
>>> y = 4
>>> (x + y)   # This adds x and y.
7
>>> (x + y,)  # Including a comma indicates the parentheses denote a tuple.
(7,)
>>> ()        # To create an empty tuple, use an empty pair of parentheses.
()
```
#### 5.7.3 tuple 自動解包、自動打包
```
>>> (one, two, three, four) =  (1, 2, 3, 4)
>>> one
1
>>> two
2
```
```
one, two, three, four = 1, 2, 3, 4
```
```
>>> x = (1, 2, 3, 4)
>>> a, b, *c = x
>>> a, b, c
(1, 2, [3, 4])
>>> a, *b, c = x
>>> a, b, c
(1, [2, 3], 4)
>>> *a, b, c = x
>>> a, b, c
([1, 2], 3, 4)
>>> a, b, c, d, *e = x
>>> a, b, c, d, e
(1, 2, 3, 4, [])
```
```
>>> [a, b] = [1, 2]
>>> [c, d] = 3, 4
>>> [e, f] = (5, 6)
>>> (g, h) = 7, 8
>>> i, j = [9, 10]
>>> k, l = (11, 12)
>>> a
1
>>> [b, c, d]
[2, 3, 4]
>>> (e, f, g)
(5, 6, 7)
>>> h, i, j, k, l
(8, 9, 10, 11, 12)
```
#### 5.7.4  list與tuple的轉換
```
>>> list((1, 2, 3, 4))
[1, 2, 3, 4]
>>> tuple([1, 2, 3, 4])
(1, 2, 3, 4)
```
```
>>> list("Hello")
['H', 'e', 'l', 'l', 'o']
```
### 5.8 set

#### 5.8.1 set 的操作

```
>>> x = set([1, 2, 3, 1, 3, 5])    #也可以用 set()函式來把一個序列型別(例如list或tuple)轉換成無序的set
>>> x
{1, 2, 3, 5}                       #集合中重複的資料會被刪除
>>> x.add(6)      #可以用add()函式來添加set中的元素
>>> x
{1, 2, 3, 5, 6}    
>>> x.remove(5)               #用remove()函式可以移除set中的元素
>>> x
{1, 2, 3, 6}   
>>> 1 in x       #關鍵字in可以檢查物件是否位於set中
True
>>> 4 in x                     
False
>>> y = set([1, 7, 8, 9])
>>> x | y                 #可以用|來求出兩個set的聯集 相當於邏輯中的OR
{1, 2, 3, 6, 7, 8, 9}
>>> x & y                  #可以用&來求出兩個set的交集 相當於邏輯中的AND
{1}
>>> x ^ y              #可以用|來求出兩個set的對稱差(只屬於一個set而不屬於另外一個) 相當於邏輯中XOR
{2, 3, 6, 7, 8, 9}

```
#### 5.8.2 frozenset
```
>>> x = set([1, 2, 3, 1, 3, 5]) 
>>> z = frozenset(x)
>>> z
frozenset({1, 2, 3, 5})
>>> z.add(6)
Traceback (most recent call last):
  File "<pyshell#79>", line 1, in <module>
    z.add(6)
AttributeError: 'frozenset' object has no attribute 'add'
>>> x.add(z)
>>> x
{1, 2, 3, 5, frozenset({1, 2, 3, 5})}
```
# 第6章 字串

### 6.1 字串為字元序列(sequence)
```
>>> x = "Hello"
>>> x[0]
'H'
>>> x[-1]
'o'
>>> x[1:]
'ello'
```
```
>>> x = "Goodbye\n"
>>> x = x[:-1]
>>> x
'Goodbye'
```
```
>>> len("Goodbye")
7
```
### 6.2 基本的字串操作
```
>>> x = "Hello " + "World"
>>> x
'Hello World'
```
```
>>> 8 * "x"
'xxxxxxxx'

```

### 6.3 特殊字元和轉義字元

#### 6.3.2 數值(八進位和十六進位)以及Unicode轉義字元
```
>>> 'm'
'm'
>>> '\155'
'm'
>>> '\x6D'
'm'
```
```
>>> '\n'
'\n'
>>> '\012'
'\n'
>>> '\x0A'
'\n'
```
```
>>> unicode_a ='\N{LATIN SMALL LETTER A}'      #透過Unicode 名稱 表示Unicode 字元
>>> unicode_a
'a'                                            #Unicode 字元集包括常見的 ASCII字元
>>> unicode_a_with_acute = '\N{LATIN SMALL LETTER A WITH ACUTE}'      
>>> unicode_a_with_acute
'á'
>>> "\u00E1"                                   #透過\u後面跟著4碼十六進位數字表示Unicode字元
'á'
>>>
```
#### 6.3.3 用print()函式輸出帶有轉義字元的字串
```
>>> 'a\n\tb'
'a\n\tb'
>>> print('a\n\tb')
a
    b
```
```
>>> print("abc\n")
abc

>>> print("abc\n", end="")           
abc
>>>
```
### 6.4 字串的method

#### 6.4.1 用spli和join()切割與連接字串
```
>>> " ".join(["join", "puts", "spaces", "between", "elements"])
'join puts spaces between elements'
```
```
>>> "::".join(["Separated", "with", "colons"])
'Separated::with::colons'
```
```
>>> "".join(["Separated", "by", "nothing"])
'Separatedbynothing'
```
```
>>> x = "You\t\t can have tabs\t\n \t and newlines \n\n mixed in"
>>> x.split()
['You', 'can', 'have', 'tabs', 'and', 'newlines', 'mixed', 'in']
>>> x = "Mississippi"
>>> x.split("ss")
['Mi', 'i', 'ippi']
```
```
>>> x = 'a b c d'
>>> x.split(' ', 1)
['a', 'b c d']
>>> x.split(' ', 2)
['a', 'b', 'c d']
>>> x.split(' ', 9)
['a', 'b', 'c', 'd']

```
#### 6.4.2 用int() 和float()函示將字串轉換為數字
```
>>> float('123.456')
123.456
>>> float('xxyy') 
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: could not convert string to float: 'xxyy'
>>> int('3333')
3333
>>> int('123.456')                       #整數中不能有小數點
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: invalid literal for int() with base 10: '123.456'
>>> int('10000', 8)                   #把'10000'用八進位基底來解釋成10進位整數'
4096
>>> int('101', 2)
5
>>> int('ff', 16)
255
>>> int('123456', 6)              #'123456'無法用六進位基底來解釋
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: invalid literal for int() with base 6: '123456'
```
#### 6.4.3 用sptrip(()、lstrip()、rstrip()移除多於空白
```
>>> x = "  Hello,    World\t\t "
>>> x.strip()
'Hello,    World'
>>> x.lstrip()
'Hello,    World\t\t '
>>> x.rstrip()
'  Hello,    World'
```
```
>>> import string
>>> string.whitespace
' \t\n\r\x0b\x0c'
>>> " \t\n\r\v\f"
' \t\n\r\x0b\x0c'
```
```
>>> x = "www.python.org"
>>> x.strip("w")                       #移除所有w字元
'.python.org'
>>> x.strip("gor")                     #移除所有 g、o、r字元
'www.python.'
>>> x.strip(".gorw")                    #移除所有.、 g、o、r、w字元
'python'
```
#### 6.4.4 isdigit()、isalpha()、islower()、isupper()和字串相關常數
```
>>> x = "123"
>>> x.isdigit()
True
>>> x.isalpha()
False
>>> x = "M"
>>> x.islower()
False
>>> x.isupper()
True
```
### 6.5 從物件轉換成字串

#### 6.5.2 find()、rfind()、index()、rindex()
```
>>> x = "Mississippi"
>>> x.find("ss")
2
>>> x.find("zz")
-1
```
```
>>> x = "Mississippi"
>>> x.find("ss", 3)
5
>>> x.find("ss", 0, 3)
-1
```
```
>>> x = "Mississippi"
>>> x.rfind("ss")
5
```
#### 6.5.3 count()
```
>>> x = "Mississippi"
>>> x.count("ss")
2
```
#### 6.5.4 startswith()、endswith()
```
>>> x = "Mississippi"
>>> x.startswith("Miss")
True
>>> x.startswith("Mist")
False
>>> x.endswith("pi")
True
>>> x.endswith("p")
False
```
```
>>> x.endswith(("i", "u"))
True
```

### 6.6 使用format() method來格式化字串

#### 6.6.1 peplace()
```
>>> x = "Mississippi"
>>> x.replace("ss", "+++")
'Mi+++i+++ippi
```
#### 6.6.2 maketrans()、translate()
```
>>> x = "~x ^ (y % z)"
>>> table = x.maketrans("~^()", "!&[]")
>>> x.translate(table)
'!x & [y % z]'
```
#### 6.6.5 透過list修改字串
```
>>> text = "Hello, World"
>>> wordList = list(text)
>>> wordList[6:] = []                    
>>> wordList.reverse()
>>> text = "".join(wordList)      
>>> print(text)                          
,olleH
```
### 6.7 以 repr() 和str 將物件轉換成字串表達
```
>>> repr([1, 2, 3])
'[1, 2, 3]'
>>> x = [1]
>>> x.append(2)
>>> x.append([3, 4])
>>> 'the list x is ' + repr(x)
'the list x is [1, 2, [3, 4]]'
```
### 6.8 以 forMat()method來格式化字串

#### 6.8.1 用位置參數、編號參數來替換
```
>>> "{0} is the {1} of {2}".format("Ambrosia", "food", "the gods") #1
'Ambrosia is the food of the gods'
>>> "{{Ambrosia}} is the {0} of {1}".format("food", "the gods")    #2
'{Ambrosia} is the food of the gods'
```
#### 6.8.2 使用指名參數 (named parameter)
```
>>> "{food} is the food of {user}".format(food="Ambrosia", 
...       user="the gods") 
'Ambrosia is the food of the gods'
```
```
>>> "{0} is the food of {user[1]}".format("Ambrosia", 
...          user=["men", "the gods", "others"]) 
'Ambrosia is the food of the gods'
```
#### 6.8.3 格式化設定
```
>>> "{0:10} is the food of gods".format("Ambrosia")      
'Ambrosia   is the food of gods'
>>> "{0:>10} is the food of gods".format("Ambrosia")        
'  Ambrosia is the food of gods'
>>> "{0:&>10} is the food of gods".format("Ambrosia")           
'&&Ambrosia is the food of gods'
```
```
>>> "{0:{1}} is the food of gods".format("Ambrosia", 10)   
'Ambrosia   is the food of gods'
>>> "{food:{width}} is the food of gods".format(food="Ambrosia", width=10)
'Ambrosia   is the food of gods'
```
### 6.9 以 % 算符來格式化字串
```
>>> "%s is the %s of %s" % ("Ambrosia", "food", "the gods")
'Ambrosia is the food ```of the gods'
```
```
>>> "%s is the %s of %s" % ("Nectar", "drink", "gods")
'Nectar is the drink of gods'
>>> "%s is the %s of the %s" % ("Brussels Sprouts", "food", 
...        "foolish")
'Brussels Sprouts is the food of the foolish'
```
```
>>> x = [1, 2, "three"]
>>> "The %s contains: %s" % ("list", x)
"The list contains: [1, 2, 'three']"
```
#### 6.9.1 %算符的格式化參數
```
>>> "Pi is <%-6.2f>" % 3.14159 # use of the formatting sequence: %–6.2f
'Pi is <3.14  >'
```
#### 6.9.2 %算符的指名參數
```
>>> num_dict = {'e': 2.718, 'pi': 3.14159}
>>> print("%(pi).2f - %(pi).4f - %(e).2f" % num_dict)
3.14 - 3.1416 - 2.72
```
### 6.10 以 f-strings來格式化字串
```
>>> value = 42
>>> message = f"The answer is {value}"
>>> print(message)
The answer is 42
```
```
>>> pi = 3.1415
>>> print(f"pi is {pi:{10}.{2}}")
pi is        3.1
```
### 6.10 bytes物件
```
>>> unicode_a_with_acute = '\N{LATIN SMALL LETTER A WITH ACUTE}'
>>> unicode_a_with_acute
'á'
>>> xb = unicode_a_with_acute.encode()    
>>> xb
b'\xc3\xa1'                               
>>> xb += 'A'                              
Traceback (most recent call last):
  File "<pyshell#35>", line 1, in <module>
    xb += 'A'
TypeError: can't concat str to bytes
>>> xb.decode()                           
'á'
```
# 第7章 字典

### 7.1 什麼是字典?
```
>>> x = []        
>>> y = {}        
```
```
>>> y[0] = 'Hello'
>>> y[1] = 'Goodbye'
```
```
>>> x[0] = 'Hello'
Traceback (innermost last):
  File "<stdin>", line 1, in ?
IndexError: list assignment index out of range
```
```
>>> print(y[0])
Hello
>>> y[1] + ", Friend."
'Goodbye, Friend.'
```
```
>>> y["two"] = 2
>>> y["pi"] = 3.14
>>> y["two"] * y["pi"]
6.28
```
```
>>> english_to_french = {}                    #建立空字典 一定要先建立(不一定是空的)
>>> english_to_french['red'] = 'rouge'          
>>> english_to_french['blue'] = 'bleu'
>>> english_to_french['green'] = 'vert'
>>> print("red is", english_to_french['red'])   
red is rouge

```

### 7.2 其他字典操作
```
>>> english_to_french = {'red': 'rouge', 'blue': 'bleu', 'green': 'vert'}
```
```
>>> len(english_to_french)
3
```
#### 7.2.1 keys() 、values()和items()method
```
>> list(english_to_french.keys())
['green', 'blue', 'red']
```
```
>>> list(english_to_french.values())
 ['vert', 'bleu', 'rouge']
```
```
>>> list(english_to_french.items())
[('green', 'vert'), ('blue', 'bleu'), ('red', 'rouge')]
```
### 7.2.2 get()和setdefault()method
```
>>> list(english_to_french.items())
[('green', 'vert'), ('blue', 'bleu'), ('red', 'rouge')]
>>> del english_to_french['green']
>>> list(english_to_french.items())
 [('blue', 'bleu'), ('red', 'rouge')]
```
```
>>> 'red' in english_to_french
True
>>> 'orange' in english_to_french
False
```
```
>>> print(english_to_french.get('blue', 'No translation'))
bleu
>>> print(english_to_french.get('chartreuse', 'No translation'))
No translation
```
```
>>> print(english_to_french.setdefault('chartreuse', 'No translation'))
No translation
```
#### 7.2.3 copy() 和update()method
```
>>> x = {0: 'zero', 1: 'one'}
>>> y = x.copy()
>>> y
{0: 'zero', 1: 'one'}
```
```
>>> z = {1: 'One', 2: 'Two'}
>>> x = {0: 'zero', 1: 'one'}
>>> x.update(z)
>>> x
{0: 'zero', 1: 'One', 2: 'Two'}
```
### 7.3 字數統計
```
>>> sample_string = "To be or not to be"
>>> occurrences = {}
>>> for word in sample_string.split():
...     occurrences[word] = occurrences.get(word, 0) + 1   #1
...
>>> for word in occurrences:
...     print("The word", word, "occurs", occurrences[word], \
...            "times in the string")
...
The word To occurs 1 times in the string
The word be occurs 2 times in the string
The word or occurs 1 times in the string
The word not occurs 1 times in the string
The word to occurs 1 times in the string
```
### 7.5 稀疏矩陣
```
matrix = [[3, 0, -2, 11], [0, 9, 0, 0], [0, 7, 0, 0], [0, 0, 0, -5]]
```
```
matrix = {(0, 0): 3, (0, 2): -2, (0, 3): 11, 
          (1, 1): 9, (2, 1): 7, (3, 3): -5}
```
```
if (rownum, colnum) in matrix:
    element = matrix[(rownum, colnum)]
else:
    element = 0
```

### 7.6 以字典作為快取
```
def sole(m, n, t):
    # . . . do some time-consuming calculations . . .
    return(result)
```
```
sole_cache = {}
def sole(m, n, t):
    if (m, n, t) in sole_cache:
        return sole_cache[(m, n, t)]
    else:
        # . . . do some time-consuming calculations . . .
        sole_cache[(m, n, t)] = result
        return result
```
# 第8章 流程控制

### 8.3 for 迴圈
```
x = [1.0, 2.0, 3.0]
for n in x:
    print(1 / n)
```
#### 8.3.1 range()函式
```
x = [1, 3, -7, 4, 9, -5, 4]
for i in range(len(x)):
    if x[i] < 0:
        print("Found a negative number at index ", i)
```
#### 8.3.2 以range(m,n)控制數列範圍
```
>>> list(range(3, 7))           
[3, 4, 5, 6]
>>> list(range(2, 10))          
[2, 3, 4, 5, 6, 7, 8, 9]        
>>> list(range(5, 3))
[]
```
```
>>> list(range(0, 10, 2))
[0, 2, 4, 6, 8]
>>> list(range(5, 0, -1))
[5, 4, 3, 2, 1]
```
#### 8.3.4 for迴圈與tuple解包多重設定變數

```
omelist = [(1, 2), (3, 7), (9, 5)]
result = 0
for t in somelist:
    result = result + (t[0] * t[1])
```
```
somelist = [(1, 2), (3, 7), (9, 5)]
result = 0

for x, y in somelist:
    result = result + (x * y)
```
#### 8.3.5 enumerate()函式
```
x = [1, 3, -7, 4, 9, -5, 4]
for i, n in enumerate(x):                                   
    if n < 0:                                           
        print("Found a negative number at index ", i)   
```
#### 8.3.6 zip() 函式
```
>>> x = [1, 2, 3, 4]
>>> y = ['a', 'b', 'c']           
>>> z = zip(x, y)
>>> list(z)
[(1, 'a'), (2, 'b'), (3, 'c')]   

```
### 8.4 用生成式快速建立新的list與字典
```
>>> x = [1, 2, 3, 4]
>>> x_squared = []
>>> for item in x:
...     x_squared.append(item * item)
... 
>>> x_squared
[1, 4, 9, 16]
```
#### 8.4.1 生成式
```
>>> x = [1, 2, 3, 4]
>>> x_squared = [item * item for item in x]
>>> x_squared
[1, 4, 9, 16]
```
```
>>> x = [1, 2, 3, 4]
>>> x_squared = [item * item for item in x if item > 2]

>>> x_squared
[9, 16]
```
```
>>> x = [1, 2, 3, 4]
>>> x_squared_dict = {item: item * item for item in x}
>>> x_squared_dict
{1: 1, 2: 4, 3: 9, 4: 16}
```
#### 8.4.2 產生器
```
>>> x = [1, 2, 3, 4]
>>> x_squared = (item * item for item in x)
>>> x_squared
<generator object <genexpr> at 0x102176708>
>>> for square in x_squared:
...     print(square,)
...
1 4 9 16
```
### 8.5 敘述、區塊、和縮排
```
>>> x = 1; y = 0; z = 0
>>> if x > 0: y = 1; z = 10
... else: y = -1
... 
>>> print(x, y, z)
1 1 10
```
#### 8.5.1 敘述、區塊、縮排
```
>>>
>>>   x = 1
File "<stdin>", line 1
    x = 1
    ^
   IndentationError: unexpected indent
>>>
```
```
>>> x = 1
>>> if x == 1: 
...    y = 2
...    if v > 0:
...        z = 2
...        v = 0
...
>>> x = 2
```
```
>>> x = 1
>>> if x == 1:
           y = 2
        z = 2
File "<stdin>", line 3
       z = 2
       ^
    IndentationError: unindent does not match any outer indentation level
```
#### 8.5.2 將一行敘述拆成多行
```
>>> print('string1', 'string2', 'string3' \
...    , 'string4', 'string5')
string1 string2 string3 string4 string5
>>> x = 100 + 200 + 300 \
...    + 400 + 500
>>> x
1500
>>> v = [100, 300, 500, 700, 900,
...    1100, 1300]
>>> v
[100, 300, 500, 700, 900, 1100, 1300]
>>> max(1000, 300, 500,
...        800, 1200)
1200
>>> x = (100 + 200 + 300
...          + 400 + 500)
>>> x
1500
```
### 8.6 布林值與運算式的真假運算

#### 8.6.2 布林算符與比較算符
```
>>> [2] and [3, 4]
[3, 4]
>>> [] and 5
[]
>>> [2] or [3, 4]
[2]
>>> [] or 5
5
>>> 


>>> x = [0]
>>> y = [x, 1]
>>> x is y[0]            
True
>>> x = [0]              
>>> x is y[0]
False
>>> x == y[0]
True
```
# 第9章 函式

### 9.1 基本函式定義
```
>>> def fact(n): 
...     """Return the factorial of the given number."""            
...     r = 1
...     while n > 0:
...         r = r * n
...         n = n - 1
...     return r                                     
...
```
```
>>> fact(4)                            
24                                     
>>> x = fact(4)                       
>>> x 
24
>>>
```
### 9.2 函式的參數定義與引數傳遞
```
>>> def power(x, y):
...     r = 1
...     while y > 0:
...         r = r * x
...         y = y - 1
...     return r
... 
>>> power(3, 3)
27
```
```
>>> power(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: power() missing 1 required positional argument: 'y'
>>>
```
```
>>> def power(x, y=2):
...     r = 1
...     while y > 0:
...         r = r * x
...         y = y - 1
...     return r
...
```
```
>>> power(3, 3)
27
>>> power(3)
9
```
#### 9.2.2 用參數名稱傳遞引數
```
def list_file_info(size=False, create_date=False, mod_date=False, ...):
    ...get file names...
    if size:
        # code to get file sizes goes here
    if create_date:
        # code to get create dates goes here
    # do any other stuff desired
    
    return fileinfostructure
```
```
fileinfo = list_file_info(size=True, mod_date=True)

>>> power(2, 3)
8
>>> power(3, 2)
9
>>> power(y=2, x=3)
9
```
#### 9.2.3 帶有*和**的參數:一個參數接收多出來的引數
```
>>> def maximum(*numbers):
...     if len(numbers) == 0:
...         return None
...     else:
...         maxnum = numbers[0]
...         for n in numbers[1:]:
...             if n > maxnum:
...                 maxnum = n
...         return maxnum
...
```
```
>>> maximum(3, 2, 8)
8
>>> maximum(1, 5, 9, -2, 2)
9
```
```
>>> def example_fun(x, y, **other):
...     print("x: {0}, y: {1}, keys in 'other': {2}".format(x, 
...           y, list(other.keys())))
...     other_total = 0
...     for k in other.keys():
...         other_total = other_total + other[k]
...     print("The total of values in 'other' is {0}".format(other_total))

```
### 9.3 用可變 （mutable）物件作為引數時要小心
```
>>> def f(n, list1, list2):
...    list1.append(3)
...    list2 = [4, 5, 6]
...    n = n + 1
...
>>> x = 5
>>> y = [1, 2]
>>> z = [4, 5]
>>> f(x, y, z)
>>> x, y, z
(5, [1, 2, 3], [4, 5])
```
### 9.4 local、global、nonlocal變數
```
def fact(n):
    """Return the factorial of the given number."""
    r = 1
    while n > 0:
        r = r * n
        n = n - 1
    return r
```
```
>>> def fun():
...     global a
...     a = 1
...     b = 2
...

>>> a = "one"
>>> b = "two"
```
```
>>> fun()
>>> a
1
>>> b
'two'
```
```
top level-> g_var: 0 nl_var: 0
in test-> g_var: 0 nl_var: 2
in inner_test-> g_var: 1 nl_var: 4
in test-> g_var: 1 nl_var: 4
top level-> g_var: 1 nl_var: 0
```
### 9.5 將變數參照到函式
```
>>> def f_to_kelvin(degrees_f):                     #A
...     return 273.15 + (degrees_f - 32) * 5 / 9
...
>>> def c_to_kelvin(degrees_c):                      #B
...     return 273.15 + degrees_c
...
>>> abs_temperature = f_to_kelvin                    #C
>>> abs_temperature(32)
273.15
>>> abs_temperature = c_to_kelvin                      #D
>>> abs_temperature(0)
273.15
```
```
>>> t = {'FtoK': f_to_kelvin, 'CtoK': c_to_kelvin}      #1
>>> t['FtoK'](32)                                       #A
273.15
>>> t['CtoK'](0)                                        #B
273.15
```
### 9.6 lambda 匿名函式
```
>>> t2 = {'FtoK': lambda deg_f: 273.15 + (deg_f - 32) * 5 / 9, #1 
...       'CtoK': lambda deg_c: 273.15 + deg_c}                #1
>>> t2['FtoK'](32)
273.15
```
### 9.7 產生器(走訪器)函式
```
>>> def four():
...     x = 0                                    #A
...     while x < 4:
...         print("in generator, x =", x)
...         yield x                               #B
...         x += 1                               #C
... 
>>> for i in four():
...     print(i)
...
in generator, x = 0
0
in generator, x = 1
1
in generator, x = 2
2
in generator, x = 3
3
```
```
>>> 2 in four()
in generator, x = 0
in generator, x = 1
in generator, x = 2
True
>>> 5 in four()
in generator, x = 0
in generator, x = 1
in generator, x = 2
in generator, x = 3
False
```
### 9.8 修飾器（Decorator）
```
>>> def decorate(func):
...     print("in decorate function, decorating", func.__name__)
...     def wrapper_func(*args):
...         print("Executing", func.__name__)
...         return func(*args)
...     return wrapper_func
...
>>> def myfunction(parameter):
...     print(parameter)
...
>>> myfunction = decorate(myfunction)
in decorate function, decorating myfunction
>>> myfunction("hello")
Executing myfunction
hello
```
```
>>> def decorate(func):
...     print("in decorate function, decorating", func.__name__)  #1
...     def wrapper_func(*args):
...         print("Executing", func.__name__)
...         return func(*args)
...     return wrapper_func                                       
...
>>> @decorate                                                     
... def myfunction(parameter):
...     print(parameter)
...
in decorate function, decorating myfunction                      
>>> myfunction("hello")
Executing myfunction
hello
```
