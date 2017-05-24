#Kotlin基本语法

##变量
* 不可变变量：val修饰

		val s= "Sample" //自动推断出字符串
		val i= 23//整型，立即赋值

* 也可以指定类型：
  
		val s:Stirng = "Sample" //指定String 类型
	    val activity:Context = this
	    
* 可变变量：var修饰 <br>
  
		varx =5x +=1//自动推断出 int 类型

**不管变量时var还是val都要初始化值，这点保证了空安全**

##基本数据类型
### 1.数字类型：
	
数字类型 | 
------------ | 
Double | 
Float | 
Long | 
Int | 
Short | 
Byte | 

* Kotlin没有隐式拓宽转换，如java当中的int可以饮食转换为long,必须要显示类型转换

		val a:Double = 5.2
		val b:Int = a.toInt()//显示转， b等于5
		
		val c:Float = 5.2F
		val d:Int = c.toInt()//d等于5


* 显示类型转换的方法：
		
		toByte():Byte
		toShort():Short
		toInt():Int
		toLong():Long
		toFloat():Float
		toDoubel():Double
		toChar():Char
		
### 2.字符串
* 使用Char类型表示

		val e:Char = 'q'


### 3.布尔
* 使用Boolean类型表示：

		val f:Boolean = true
		
		
### 4.字符串
* 使用String 表示

		val g:String = "Hello World"


### 5.字符串模板
* 字符串模板，可以包含一些小段代码，会把求值结果合并到字符串中
* 模板表达式以 美元符号（$）开头

		val h = "me"
		val j = "it is $h"


* 模板中的任意表达式，用大括号：
	
		val k = "h length is ${h.length}"//h length is 2
		

### 6.数组
* 使用Array类来创建和操作数组，它定义了get和set函数，size属性，及其他的成员函数

* 使用库函数arrayOf()来创建一个数组并传递元素值给他
		
		arrayOf(1,2,3)
		array[1,2,3]//以上语句创建的
		
* []可以用于访问数组元素，实际上[]被惊醒了操作符的重载，调用的是Array类的get和set方法

* 库函数arrayOfNulls()可以用于创建一个指定大小，元素都为空的数组

		//使用装箱操作
		val arr1 =arrayOf(1,2,3)	
		
		//原生类型数组，还有BtyeArray,ShorArray等
		val arr2:IntArray = IntArrayOf(1,2,3)
		
		//直接指定长度
		val arr3 = arrayOfNulls<Int>(5)
		
		//长度为0的空数组
		val arr3 = emptyArray<Int>()
		
		//访问数组元素
		val arr4  = arrayOf(1,2,3)
		println(arr4[1])//输出“2”,建议用这个方法
		println(arr4.get(1))//输出“2”
		
		//修改元素
		arr4[1]=10
		println(arr4[1])//输出“10”
		
		//遍历数组
		for(arr in arr4){
			println(arr)
		}
		
		//遍历数组下标
		for(arr in arr4.indices){
			println(arr)
		}
		
		
##控制流
		
### 1.if表达式
* Kotlin里可以作为一个表达式，返回一个值
	
		val l =4
		val m = 5
		//作为表达式
		val n = if(l>m)else m

### 2.when表达式
* when取代 Java switch操作符

		val o = 3
		when(o){
			1-> print("o == 1")
			2-> print("o == 2")
		else->{
			print("o == 3")
		}
		}
				
### 3.For循环

		val arr5 = arrayOf(1,2,3,4,5)
		for(arr in arr5){
			println(arr)
		}
		
### 4.while循环
* 和java一样


##函数声明
* 使用fun关键字声明

			//返回类型lnt
			fun sum(p:lnt,q:lnt):lnt{
				return p+q
			}
			
			//表达式作为返回值
			fun sum(p:Int,q:Int)= p+q
			
			//函数返回无意义的值，相当于JAVA里的void
			fun sum(p:Int,q:Int):Unit{
			}
			
			//Unit 返回类型可以省略
			fun sum(p:Int,q:Int){
			}



##空安全
* 问号表示该变量可以为空

			override fun onCreate(savedInstanceState:Bundle?){
				super.onCreate(savedInstanceState)
				setContentView(R.layout.activity_main)
			}


##定义类
* 使用class关键字声明类

			//冒号表示继承
  			class MainAcitvity:AppCompatActivity(){
  			}
	


  
  


