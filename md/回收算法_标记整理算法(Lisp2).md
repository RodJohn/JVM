    
# 原理

	最原始的Lisp2 算法

    第一次搜索，查找存活对象，并设定目标位置
    第二次搜索，更新指针为目标位置
    第三次搜索，移动对象到目标位置
    

![](https://github.com/RodJohn/JVM/blob/master/img/gcmarkcompact.jpg)

# 优点--空间利用率高

    不产生内存碎片
    

# 缺点--时间复杂度高

       进行三次可达性分析
             
移动对象

       将STW  
       存活率高的时候需要大量移动内存



    
# 适用情况

	对象存活率低


