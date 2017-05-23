
##C语言基本语法：
###1.基本数据类型
* char类型的长度为:1   和java不一样  * int类型的长度为:4* float类型的长度为:4* double类型的长度为:8 * short类型的长度为:2 * long类型的长度为:4    和java不一样 * C语言中没有boolean   用0表示假用非0表示真* signed 有符号 可以表示负数 取值范围-128~127  -2^7 ~2^7-1* unsigned 不可以表示负数 取值范围 0~255* void 不确定的类型 就代表任意类型 

###2.输入输出函数
* 输出:printf  要按照对应的占位符输出 * 输入:scanf("数据类型",地址);
* **如何取地址：&取地址的意**
* %d  -  int<br>
  %ld - long int<br>
  %c  - char<br>
  %f -  float<br>
  %u – 无符号数<br>
  %hd – 短整型<br>
  %lf – double<br>
  %x – 十六进制输出 int 或者long int 或者short int<br>
  %o -  八进制输出<br>
  %s – 字符串<br>

  int len;<br>
  scanf(“%d”, &len);<br>


###3.指针
* **指针就代表内存地址**
* ** 内存空间你就看成是一些连续的小房间 每个房间就是一个存储单元 每个存储单元的大小是1byte 每个房间里面住着数据 <br>
  想操作每个房间里面的数据  我们可以按照一定的规则给每个房间编号(门牌号)  就是内存地址 **
* ** --- * --- **号三种含义
  1. **代表相乘**
  2. ** 在一种数据类型的后面加上* 就代表这种数据类型的指针 int* **
  3. ** 如果在指针变量的前面加上*  就代表取出改地址对应的数据  **
  
####3.1指针的常见错误 
1. 声明的数据类型  要和你定义的指针类型一致
2. 野指针  指针变量未经赋值 不可以使用

####3.2指针的好处
1. 指针可以直接操作硬件  智能家居 小米 
2. 指针快速传递数据
3. 返回一个以上的值 
4. 可以方便的表示字符串 用字符数组  *
5. 指针可以表示复杂的数据结构  结构体(javaBean)

函数返回一个以上的值
通过被掉函数修改主调函数普通变量的值
1. 实参必须是普通变量的地址
2. 形参必须是指针变量
3. 被掉函数中通过修改 *形参名的方式修改主调函数相关变量的值

		change(int* a, int* b) { 
			*a = 1;
			*b = 2;
		}
	    main() { 
			int a = 3, b = 5;
			change(&a, &b);
			printf(“a=%d, b=%d\n”, a, b);
			system(“pause”);
		}

####3.3指针和数组的关系
1. 数组是一块连续的内存空间 
2. 数组名实际上就是数组中第一个元素的地址 
3. 数组就是指针

* 数组名
	int a[5]; // a是数组名，5是数组的大小，元素个数
* 数组名称是个指针常量，它存放的是数组中第一个元素的地址
	int a[5];
	&a[0]  等价于 &a
* 下标和指针的关系
	int a[5];
	a[i] 等价于 *(a + i)  // 这里i的范围是0~4(数组长度 -1)

####3.4指针的长度
**不管什么类型的指针都是4个字节**

####3.5多级指针
** 在一种数据类型的后面有几个* 就代表几级指针  int**  **

	int i = 10;
	int* p1 = &i;    // 一级指针
	int** p2 = &p1;   // 二级指针
	int*** p3 = &p2;   // 三级指针
	int**** p4 = &p3;   // 四级指针 
	****p4 = 99; // 修改变量i的值为99;


####3.6指针和指针变量的关系
* 指针就是地址，地址就是指针
* 地址就是内存单元的编号
* 指针变量是存放地址的变量
* 指针和指针变量是两个不同的概念
* 但是要注意： 通常我们叙述时会把指针变量简称为指针，实际它们含义并不一样
* 指针里存的是100,  指针: 地址
* 指针里存的是地址, 指针: 指针变量


####3.7函数的指针
1. 定义int (*pf)(int x, int y);
2. 赋值 pf = add;
3. 引用 pf(3,5);

###4.动态内存和静态内存
* **静态内存**是系统是程序编译执行后系统自动分配,由系统自动释放, 静态内存是栈分配的.<br>
  内存在程序编译的时候就已经分配好，这块内存在程序的整个运行期间都存在。例如全局变量，static 变量。<br>
  在栈上创建。在执行函数时，函数内局部变量的存储单元都可以在栈上创建，函数执行结束时这些存储单元自动被释放。栈内存分配运算内置于处理器的指令集中，效率很高，但是分配的内存容量有限。<br>
  
  
* **动态内存**是开发者手动分配的, 是堆分配的. 必须自己手动释放 <br>
  int i = 10;  栈分配的空间一般不会超过2M <br>
  Person p =   new Person(); 堆分配的空间最大可和可以你电脑的内存一样大 <br>
  从堆上分配，亦称动态内存分配。程序在运行的时候用malloc 或new 申请任意多少的内存，程序员自己负责在何时用 free 或delete 释放内存。动态内存的生存期由我们决定，使用非常灵活，但问题也最多.<br>
  
  	
		malloc(memory allocate) 申请空间函数
		free(地址); 回收内存
	    realloc  re- allocate

###5.堆和栈的区别
* 申请方式 <br>
由系统自动分配.例如,声明一个局部变量int b; 
系统自动在栈中为b开辟空间.例如当在调用涵数时，需要保存的变量，最明显的是在递归调用时，要系统自动分配一个栈的空  间，后进先出的，而后又由系统释放这个空间.

* 堆 <br>   
需要程序员自己申请，并指明大小，在c中用malloc函数   
如char*  p1  =  (char*) malloc(10);   //14byte
但是注意p1本身是在栈中的.

###6.结构体

		struct Student {
			int age;
			float score;
			char sex;
		};
		main() {
			struct Student stu = {18, 88.5, 'M'};
		}


####6.1使用结构体变量

		struct Student stu = {80,55.5,'F'};
		struct Student stu2;
		stu2.age = 10;
	    stu2.score = 88.8f;
		stu2.sex= ‘M';

		printf("%d %f %c\n", st.age, st.score, st.sex);

		// 结构体指针
		struct Student * pStu;
		pStu = &stu;
		pStu->age 在计算机内部会被转换为 (* pStu).age
		pStu ->age的含义: pStu所指向的结构体变量中的age这个成员
		

###7.UNIO 联合体

		struct Date {
      		int year;
      		int month;
      		int day;
		}; 
		union Mix {
     		ong i; 
     		int k; 
    		char ii;
		};
		main() { 
       		printf("date:%d\n",sizeof(struct Date)); 
       		printf("mix:%d\n",sizeof(union Mix)); 
       		system("pause");
		} 

###8.枚举
* 枚举是一个被命名整形常数的集合

		enum WeekDay {
     		Monday=0,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday
		};

		main() {
       		enum WeekDay day = Sunday;
       		printf("%d\n",day);
      	    system("pause");
		}
		
###9.typedef
* 声明自定义数据类型，配合各种原有数据类型来达到简化编程的目的的类型定义关键字。 

		#include <stdio.h> 
		#include <stdlib.h>
		typedef int i;
		typedef long l;
		main() {
       		i m = 10;
       		l n = 123123123;
       		printf("%d\n", m);
       		printf("%ld\n", n);
       		system("pause");       
		}
		



























