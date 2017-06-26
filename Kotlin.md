# Kotlin基本语法

## 变量
* 不可变变量：val修饰

		val s= "Sample" //自动推断出字符串
		val i= 23//整型，立即赋值

* 也可以指定类型：
  
		val s:Stirng = "Sample" //指定String 类型
	    val activity:Context = this
	    
* 可变变量：var修饰 <br>
  
		varx =5x +=1//自动推断出 int 类型

**不管变量时var还是val都要初始化值，这点保证了空安全**

## 基本数据类型
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
		
		
## 控制流
		
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


## 函数声明
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



## 空安全
* 问号表示该变量可以为空

			override fun onCreate(savedInstanceState:Bundle?){
				super.onCreate(savedInstanceState)
				setContentView(R.layout.activity_main)
			}


## 定义类
* 使用class关键字声明类

			//冒号表示继承
  			class MainAcitvity:AppCompatActivity(){
  			}
	
***********


## 类

* 使用 class 关键字声明类。
* 类声明由类名、类头（指定其类型参数、主构造函数等）和由大括号包围的类体构成。
* 一个类可以有一个主构造函数和一个或多个次构造函数。

### 1.主构造函数

		//类名:WeatherinfoModel
		//主构造函数:constructor(val weatherinfo: WeatherinfoBean)
		class WeatherinfoModel public constructor(val weatherinfo: WeatherinfoBean)   {
    //类体
    init {
        //主构造函数不能包含任何的代码，
        //初始化的代码可以放到 init 块中
    }
	}  
	

如果主构造函数没有任何注解或者可见性修饰符（private、 protected、 internal 和 public），可以省略这个 constructor 关键字。


### 2.次构造函数

类也可以声明前缀有 constructor的次构造函数

		
		class Person {
				constructor(parent: Person){
					parent.children.add(this);
				}
		}  
		
		
### 3.创建类的实例

Kotlin并没有new关键字，简单粗暴：

		var person = Person()
		


****************
## 继承

* 声明一个显示的父类:

		open class Base {
			open fun v(){
			}
		}
		
* 子类冒号继承，override 标注在子类中覆盖：

		class Child: Base {
			ovrride fun v(){
			}
		}
		
* 如果累没有主构造函数，那么每次构造函数必须使用使用 super 关键字初始化其基类型：

		
		class MyView :View {
			constructor(ctx: Context):super(ctx)
    	  constructor(ctx: Context, attrs:    AttributeSet) : super(ctx, attrs)
		}
		
		
****************		
## 泛型

* 泛型类

		class Application<M>(m:M){}
		
	

* 泛型函数
  
类型参数要放在函数名称之前：  

		fun <M> addSubscription(observable: Observable<M>, subscriber: Subscriber<M>) {
       //.........
		}
		
		
	
	
****************	
## 抽象类

		abstract class ApiCallback<M> {
    		abstract fun onSuccess(model: M)
    		abstract fun onFailure(msg: String?)
    		abstract fun onFinish()
		}
		
1、抽象方法必须为 public 或者 protected，缺省情况下默认为 public；<br>
2、抽象类不能用来创建对象；<br>
3、如果一个类继承于一个抽象类，则子类必须实现父类的抽象方法。如果子类没有实现父类的抽象方法，则必须将子类也定义为为 abstract 类。如果抽象类中含有抽象属性，再实现子类中必须将抽象属性初始化，除非子类也为抽象类。

### 抽象方法

1、抽象方法必须用 abstract 关键字进行修饰；<br>
2、抽象方法默认被 open 修饰，可以不用手动添加 open；<br>
3、抽象方法没有具体的实现；<br>
4、含有抽象方法的类成为抽象类，必须由 abtract 关键字修饰。

### 抽象属性

抽象属性就是在 var 或 val 前被 abstract 修饰。


****************
## 嵌套类

* 类里面可以嵌套在其他类：
		
		class A {
    		val a: String = "a"

    		class B {
        		val b: String = "b"
    		}
		}

访问：

		val a = A.B().b//a输出为“b”
		
* 如果想让类 B 能访问类 A 的成员，可以加 inner 标记：

		class A {
    		val a: String = "a"

    		inner class B {
       		 val b: String = a
		    }
	    }
	    
访问：

		val a = A().B().b//a输出为“a”
		
************
## 对象

有时候，我们需要创建一个对某个类做轻微改动的类的对象，而不是为之显式声明新的子类。

### 1.对象表达式

抽象类不能用来创建对象，可以创建一个继承自某个（或某些）类型的匿名内部类的对象:

		ApiClient.retrofit().loadData("101190201"), object : ApiCallback<WeatherinfoModel>() {
            override fun onSuccess(model: WeatherinfoModel) {
                //……
            }

            override fun onFailure(msg: String?) {
                //……
            }

            override fun onFinish() {
                //……
            }}
            
            
### 2.对象声明

* 单例模式
在 object 关键字后跟一个名称，声明单例模式：


		object ApiClient {
    	  fun retrofit(): ApiStores {
    	  //……
        		return retrofit.create(ApiStores::class.java)
       	}
		}

引用该对象：

		ApiClient.retrofit()

* 伴生对象

使用 companion 关键字标记：

		class ApiStores {
    			companion object A {
        		//baseUrl
        		val API_SERVER_URL = "http://				www.weather.com.cn/"
   			 }
		}
		
这样就能直接访问该伴生对象的成员：
		
		val url = ApiStores.API_SERVER_URL
		
可以省略伴生对象的名称 A，伴生对象也适合接口。


## 数据类
数据类提供了访问它们属性 getter 和 setter，toString()等：

		data class WeatherinfoModel constructor(val weatherinfo: WeatherinfoBean) {
    
    			data class WeatherinfoBean(
            		val city: String,
            		val cityid: String
    			)
		}
		
数据类必须满足以下要求：

1、主构造函数需要至少有一个参数；<br>
2、主构造函数的所有参数需要标记为 val 或 var；<br>
3、数据类不能是抽象、开放、密封或者内部的；<br>
4、在 1.1 之前，数据类只能实现接口。

## 复制
在很多情况下，我们只需要改变一个对象某些属性，其余部分保持不变，这里可以用到数据类的 copy，以上面的 WeatherinfoModel 为例，Retrofit 请求成功，我有个回调：


		override fun onSuccess(model: WeatherinfoModel) {
    Log.d("wxl",model.toString())//输出“WeatherinfoModel(weatherinfo=WeatherinfoBean(city=无锡, cityid=101190201))”
    Log.d("wxl", "city=" + model.weatherinfo.city + ",cityid=" + model.weatherinfo.cityid)//输出“city=无锡,cityid=101190201”
    val weatherinfoBean = model.weatherinfo.copy(city = "上海")
    val weatherinfoModel = WeatherinfoModel(weatherinfoBean)
    Log.d("wxl", "city1=" + 		weatherinfoModel.weatherinfo.city + ",cityid1=" + weatherinfoModel.weatherinfo.cityid)//输出“city1=上海,cityid1=101190201”
		}

## 委托
所谓委托模式 ，就是为其他对象提供一种代理以控制对这个对象的访问，在 Java 开发过程中，是继承模式之外的很好的解决问题的方案。

		interface Base {
   			 fun print()
		}

		class A(val a: Int) : Base {
    		override fun print() {
        		Log.d("wxl", "a=" + a)
    		}
		}

		class B (val base: Base):Base by base

调用：

		val a = A(1)
		Log.d("wxl", "a=" + B(a).print())
		
类 B 居然能调用类 A 方法，关键字 by 表示 base 将会在 B 中内部存储, 并且编译器将生成转发给 base 的所有 Base 的方法。
