# Prolog Day 3

Prolog真是一位解题高手，Sudoku是我非常喜欢的一个游戏，Programming Logically!

不过对于不熟悉Prolog谓词的而言，又成了一个比较头疼所事，如果不告诉我可以用fd_all_difference来判断一个列表中元素没有重复值，真的不会想
到用“谓词”。  
其实觉得用Prolog来解决一下AI问题是很有用的，比如做一个棋类游戏的AI，告诉Prolog规则，恐怕就能将我击败:-|

先找了一下Prolog的输出谓词：  

    
    
       geto(X) 如 X与输入流中的下一个字符匹配,则目标成功。
        get(X) 如 X与输入流中的下一个打印字符匹配,则目标成功
       skip(X) 读入并跳过当前输入流中的字符,直到找到一个可与X匹配的字符
       read(X) 读入当前输入流的下一个项,并使之与X匹配
        put(X) 把整数X输出到当前输出流(X必须例化)
            nl  对当前输出流输出控制符"回车换行"
        tab(X) 输出X个空格符到当前输出流(X必须例化)
      write(X) 把项X输出到当前输出流
    display(X) 与write(X)相似,只是它忽略运算符说明,以结构形式输出项
     op(X,Y,Z) 说明名为Z的运算符,其优先级为X,结合规则为Y
    

* 修改数独解决器来解决6＊6数独和9＊9数独问题

6＊6 和 9＊9 其实都一样，不过修改下Puzzle的构造

    
    valid([]).
    valid([Head|Tail]) :-
       fd_all_different(Head),
       valid(Tail).
    
    sudoku(Puzzle, Solution) :-
       Solution = Puzzle,
       Puzzle = [S11, S12, S13, S14, S15, S16,
                 S21, S22, S23, S24, S25, S26,
                 S31, S32, S33, S34, S35, S36,
                 S41, S42, S43, S44, S45, S46,
                 S51, S52, S53, S54, S55, S56,
                 S61, S62, S63, S64, S65, S66],
       fd_domain(Puzzle, 1, 6),
       
       Row1 = [S11, S12, S13, S14, S15, S16],
       Row2 = [S21, S22, S23, S24, S25, S26],
       Row3 = [S31, S32, S33, S34, S35, S36],
       Row4 = [S41, S42, S43, S44, S45, S46],
       Row5 = [S51, S52, S53, S54, S55, S56],
       Row6 = [S61, S62, S63, S64, S65, S66],
    
       Col1 = [S11, S21, S31, S41, S51, S61],
       Col2 = [S12, S22, S32, S42, S52, S62],
       Col3 = [S13, S23, S33, S43, S53, S63],
       Col4 = [S14, S24, S34, S44, S54, S64],
       Col5 = [S15, S25, S35, S45, S55, S65],
       Col6 = [S16, S26, S36, S46, S56, S66],
    
       Square1 = [S11, S12, S13, S21, S22, S23],
       Square2 = [S14, S15, S16, S24, S25, S26],
       Square3 = [S31, S32, S33, S41, S42, S43],
       Square4 = [S34, S35, S36, S44, S45, S46],
       Square5 = [S51, S52, S53, S61, S62, S63],
       Square6 = [S54, S55, S56, S64, S65, S66],
    
       valid([Row1, Row2, Row3, Row4, Row5, Row6,
             Col1, Col2, Col3, Col4, Col5, Col6,
             Square1, Square2, Square3, Square4, Square5, Square6]).
    		

* 让数独解决器输出格式更美观的解决方法

这其实无非在每一行结束的时候换行- -  
可以选择在Sudoku规则中放一个输出每一行的谓词序列，不过不清楚Prolog在“回答”的时候是如何格式化的:-(  
在文件中加入以下代码即可“格式化”地输出解题的结果。

    
    write('\n'), write(Row1),
    write('\n'), write(Row2),
    write('\n'), write(Row4),		  
    ...
    		

* 采用一个皇后列表的方式解决八皇后问题。使用一个1～8范围内的数字代表每个皇后，而不是元组。通过皇后在列表中的位置获取其行号并且通过其在列表中的值获得其列号。

其实书中的‘optimized_queens’就是可以用1～8来代表皇后的，因为每一行肯定有一个皇后，所以可以用行号或者列号来代表皇后。

<- [ Prolog Day 2 ](Prolog_day_2.md)

