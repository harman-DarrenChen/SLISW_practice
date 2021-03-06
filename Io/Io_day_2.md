# Io Day 2

##做

* 计算fibonacci数列

```
#循环的方法
array := List clone
array := list(1, 1)
#change the value of a to cal fib(a)
a ::= 10
for(i, 2, a, 1, array append(array at(i-1) + array at(i-2)) println)
#Output
list(1, 1, 2)
list(1, 1, 2, 3)
list(1, 1, 2, 3, 5)
list(1, 1, 2, 3, 5, 8)
list(1, 1, 2, 3, 5, 8, 13)
list(1, 1, 2, 3, 5, 8, 13, 21)
list(1, 1, 2, 3, 5, 8, 13, 21, 34)
list(1, 1, 2, 3, 5, 8, 13, 21, 34, 55)
list(1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89)
==> list(1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89)
#递归的方法
fib := method( n,
        if(((n == 1) or (n == 2)),return(1))
        #loop until n == i
        reFib := method( n, i, n1, n2,
            if((n == i),return(n1 + n2))
                return(reFib(n,(i+1),n2,(n2 + n1)))
        )
        #The first condition of reFib
        return(reFib( n, 3, 1, 1))
)
fib(1) println
fib(2) println
fib(10) println
#Output
1
1
55
```    		

* 在分母为0的情况下，如何让运算符返回0？

```  
Number setSlot("division", Number getSlot("/"))

Number setSlot("/",
 method( denominator,
       if((denominator == 0),return (0))
       return(self division( denominator))
    )
)

(1 / 0) println
(2 / 1) println
#Output
0
2
```    		

* 对二维数组进行求和 

``` 
#Define a 2D array
2d_array := list(
		 list(1, 2, 3),
		 list(4, 5, 6),
		 list(7, 8, 9)
)
sum := 0
#Nested foreach statement
2d_array foreach(r, r foreach(v, (sum = sum + v)))
"The sum of this 2D array is: " print
sum println
#Output
The sum of this 2D array is: 45
```    		

* 对列表增加一个名为myAverage的槽，以计算列表中所有数字的平均值。如果列表没有数字会发生什么？
    
```       
List myAverage := method(
    sum := 0 
    self foreach(k, 
        if((k type != "Number"),
            Exception raise("There is a NaN-value in the list, please check your list." ),
        sum =( sum + k))
    )
    return (sum/(self size))
)

list(1, 2, 3) myAverage println
list(1, "a", 3) myAverage println
#Output
2
Exception: There is a NaN-value in the list, please check your list.
---------
Exception raise                      myAverage.io 5
List myAverage                       myAverage.io 13
CLI doFile                           Z_CLI.io 140
CLI run                              IoState_runCLI() 1  		
```

* 对二维列表写一个原型。该原型的dim(x, y)方法可为一个包含y个列表的列表分配内存，其中每个列表都有x个元素，set(x, y)方法可以设置列表中的值，get(x, y)方法可返回列表中的值。

``` 
2DList := List clone
#This method should be considered later
2DList dim := method(x, y,
	   if( (self proto type == "List"),
	   	   return 2DList clone dim(x, y)
	   )
	   self setSize(x)
	   for(i, 0, (x-1), 1,
	   		  self atPut(i, (list() setSize(y)))
	   )
	   return self
)
#set the value at(x) at(y)
2DList set := method(x, y, value,
	   self at(x) atPut(y, value)
	   return self
)
#get the value 
2DList get := method(x, y,
	   return (self at(x) at(y))
)

matrix := 2DList clone dim(3, 3)
for(i, 0, 2, 1, for(n, 0, 2, 1, matrix set(i, n, i+n))) println
matrix get(1, 1) println
#Output
list(list(0, 1, 2), list(1, 2, 3), list(2, 3, 4))
2 
```    		

* 把矩阵写入文件，并从文件中读取矩阵。

```  
#Define a matrix
matrix := list(
	   list(1, 2, 3),
	   list(4, 5, 6),
	   list(7, 8, 9)
)
#Create a new file named test.txt
data := File open("test.txt")
#Transform the matrix into a sequence and write it into the file
data File write(matrix serialized)
data close
#Read solution 1: use File open(still a serialized file)
readData := File open("test.txt")
readData readLine println
readData close
#Read solution 2: use doFile
readData2 := doFile("test.txt")
readData2 println
readData2 close
#Output
list(list(1, 2, 3);, list(4, 5, 6);, list(7, 8, 9););
list(list(1, 2, 3), list(4, 5, 6), list(7, 8, 9))
```    		

* 写一个猜数字程序。

``` 
#Guess number
standardIO := File standardInput
guess := nil
counter := 0
#Get a random number between 1~100
answer := (Random value(99)+1) floor

while( counter < 10,
	   "Guess a number(1..100):" println
	   guess := standardIO readLine() asNumber()
	   if((guess == answer), 
	   			 "You are right!" println;break,
				 if((guess > answer), 
				 		   "Too big" println, 
				 		   "Too small" println)
	   )
       counter = counter + 1
)
#Output
Guess a number(1..100):
50 
Too small
Guess a number(1..100):
75
Too small
Guess a number(1..100):
90
Too small
Guess a number(1..100):
95
Too big
Guess a number(1..100):
93
Too big
Guess a number(1..100):
92
You are right!
```

<- [ Io day 1](Io_day_1.md) | [ Io day 3](Io_day_3.md) ->

