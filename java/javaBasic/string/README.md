# String
在判断String存在什么地方时，需要先明确常量池与堆的概念

##常量池简单说明
常量池(constant pool)指的是在编译期被确定，并被保存在已编译的.class文件中的一些数据。它包括了关于类、方法、接口等中的常量，也包括字符串常量

##String存储位置
- **编译时**能确定的变量直接存在常量池中
- **运行时**才能确定的（运算符中包含变量），却是在堆空间创建对象

##intern()方法
存在于.class文件中的常量池，在运行期被JVM装载，并且可以**扩充**

String的intern()方法就是扩充常量池的一个方法，当一个String实例str调用intern()方法时，Java查找常量池中是否有相同Unicode的字符串常量：
- 如果有，则返回其的引用
- 如果没有，则在常量池中增加一个Unicode等于str的字符串并返回它的引用

```java
s3 = new String("123");//在堆空间中创建对象
s4 = s3.intern();//s4指向的对象在常量池中
```