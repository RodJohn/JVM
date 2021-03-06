
# String

    每当我们创建字符串常量时，JVM会首先检查字符串常量池，
    如果该字符串已经存在常量池中，那么就直接返回常量池中的实例引用。
    如果字符串不存在常量池中，就会实例化该字符串并且将其放到常量池中。
 
## 定义

字面量定义

    String a = "chenssy";

    编译期间，
    在常量池中查找或者创建chenssy"对象
    将栈中的a指向常量池中的"chenssy"对象

new关键字定义

    String c = new String("chenssy");

    运行期间
    在常量池中查找或者创建chenssy常量
    new关键字在堆中创建一个对象chenssy
    用chenssy常量的引用构建堆chenssy对象
    堆chenssy对象赋值给栈中的c
    应用关系是：c--->chenssy--->chenssy常量。
 
图例

![1](https://github.com/RodJohn/JVM/blob/master/img/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%B8%B8%E9%87%8F%E6%B1%A0.png)

示例

    @Test
    public void test2(){
        String str1="aaa";
        String str2="aaa";
        System.out.println(str1==str2);
        //true 
        //可以看出str1跟str2是指向同一个对象

        String str3=new String("aaa");
        String str4=new String("aaa");
        System.out.println(str3==str4);
        //false 
        //可以看出用new的方式是生成不同的对象 
    }


## 运算符+

常量

      常量（字面量、final）相加
      能明确值的常量
      在编译期运算结果就确定为一个字面量字符串


变量

      字符串变量相加，
      内部实现是先new一个StringBuilder，
      然后通过append()实现相加


示例

      @Test
      public void test3(){
          String str1="hello";
          String str2="world";
          String str3="helloworld";
          String str4="hello"+"world";
          String str5=str1+str2;
          String str6=new String("hello");
          String str7=new String("world");
          String str8=str6+str7;
          System.out.println(str3==str4);
          //true
          System.out.println(str3==str5);
          //false  *
          System.out.println(str3==str8);
          //false
          System.out.println(str3==str9);
          //false
      }


      String str4="hello"+"world";
      在class文件中被优化成String str4="helloworld";


      @Test
      public void test4() {
          String s0 = "ab";
          final String s1 = "b";
          String s2 = "b";
          String s3 = getS1();
          String s10 = "a" + s1;
          String s11 = "a" + s2;
          String s12 = "a" + s3;
          System.out.println((s0 == s10));
          //true
          System.out.println((s0 == s11));
          //false
          System.out.println((s0 == s12));
          //false
      }

      private static String getS1() {
          return "b";
      }


## intern

作用

      调用intern()方法时，java查找常量池中是否有相同unicode的字符串常量，
      如果有，则返回其引用，
      如果没有，则在常量池中增加一个unicode等于str的字符串并返回它的引用。

示例

      String str1 = "abbb"; 
      String str2 = new String("abbb").intern(); 
      System.out.println(str1==str2); //true




参考

    https://www.cnblogs.com/xiaoxi/p/6036701.html            
    https://blog.csdn.net/ychenfeng/article/details/77413206 

