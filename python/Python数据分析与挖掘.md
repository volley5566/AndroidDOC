# Python数据分析与挖掘
## 概述


## Pytorch快速入门及在线体验
https://zhuanlan.zhihu.com/p/29779361


## 用 Python 玩转数据分析
https://www.coursera.org/learn/hipython



### Python数据挖掘课程
http://blog.csdn.net/Eastmount/article/category/6423551/1	
### Python数据分析-基础技术篇
http://www.imooc.com/learn/843

### 可汗学院公开课：统计学
http://open.163.com/special/Khan/khstatistics.html

### 数据分析必须想清楚的两个概念：指标和维度
http://www.cnblogs.com/xitingxie/p/5718572.html

## 数据分析
* pandas 常用的函数
http://www.jianshu.com/p/8bf430281a5c
* 《利用python进行数据分析》读书笔记系列
http://www.cnblogs.com/batteryhp/p/4868348.html


## 缺失值处理
* python数据分析与挖掘实践—拉格朗日插值法
http://blog.csdn.net/u012749168/article/details/71036170
* 拉格朗日插值python实现
http://blog.csdn.net/lhrsdl/article/details/48035959

## 线性回归模型
*  用python玩点有趣的数据分析——一元线性回归分析实例
http://blog.csdn.net/dnxbjyj/article/details/71914943
* 在Python中使用线性回归预测数据
http://python.jobbole.com/81215/
* scikit-learn的线性回归模型 利用pandas处理数据
http://blog.csdn.net/shulixu/article/details/50924991
*  Python实现机器学习一（实现一元线性回归）
http://blog.csdn.net/lulei1217/article/details/49385531
* Python实现机器学习二（实现多元线性回归）
http://blog.csdn.net/lulei1217/article/details/49386295



## 数据分析和挖掘
#### 数据分析与数据挖掘技术的概念
* 数据分析：已知的信息 进行统计
* 数据挖掘: 得到未知的信息预测  
数据挖掘是数据分析的提升

#### 数据分析与挖掘技术的用途
* 更好的发现事物的规律 （啤酒和尿不湿）

#### 数据挖掘过程：
1. 定义目标：分析的需求
2. 获取数据
3. 数据探索：初步研究数据，发现特征 
4. 数据预处理 （数据清洗{去掉脏数据}，数据集成{集中}，数据变换{规范化}，数据规约{精简}）
5. 挖掘建模（分类，聚类，关联，预测）
6. 模型评价与发布


## 数据分析和挖掘的相关模块

#### 相关模块简介
1. numpy：可以高效处理数据 提供数组支持，很多模块都依赖他，比如pandas,scipy,matplotlib都依赖他，这个模块是基础
2. pandas 主要用于数据探索和数据分析
3. matplotlib 作图模块，解决可视化问题
4. scipy 主要进行数值计算，同时支持矩阵计算，并提供了高等数据处理功能
5. statsmodels 这个模块主要用于统计分析
6. Gensim 这个模块主要用于文本挖掘
7. sklearm,keras前者机器学习 ，后者深度学习
8. scikit-learn 强大的数据建模库（数据挖掘）

#### 相关模块的基本操作
* numby
切片：按照下表取值，然后切开片段的元素 <br> 数组[其实下标:最终下标+1]
* pandas 
1. Series : 某一串数字 有顺序 会自动生成index索引
	* 自定义索引 <br> pda.Series([1,2,3],index=["one","two","three"])
2. DataFrame: 数据框  类似表格 行列
   * pda.DataFrame([......],[......],[......]])
   * pda.DataFrame({ 
       "one":4,
       "two":[3,5.6],
       "three":list (str(986))
     })  字典方式创建
    
   * head():调取数据框头部数据，默认显示前5行 
     head(2)
   * tail():调取尾部数据，默认显示后5行
   * describe():统计情况 (列的数据)
     1. count: 有多少个元素
     2. mean: 平均数
     3. std: 标准差 
     4. min: 最小值
     5. 25%：每列的25分位数  
     6. 50%：每列的50分位数
     7. 75%：每列的75分位数 
     8. max:最大数

   * 统计学中的p分位数：就是先把一列数按从小到大排序,如果一共有n个数,那么四分之一分位数就是第n*0.25个数,四分之三分位数就是第n*0.75个数,以此类推,p分位数就是第n*p个数.如果n*p不是整数则往最接近的较大的整数上归.
   *  d.T 转至 列变行  行变列

## 数据导入


## 数据可视化
* 正态分布概念
http://blog.sina.com.cn/s/blog_6406a7740102v3fc.html


## 数据探索与数据清洗
* 数据探索：及早发现数据的一些简单规律或者特征
* 数据清洗：留下可靠的数据，避免脏数据的干扰

#### 数据探索
* 数据探索的核心：
  1. 数据质量的分析（跟数据清洗密切联系）
  2. 数据特征分析（分布，对比，周期性，相关性，常见统计量等） 发现数据的基本规律


* 数据清洗：
  1. 缺失值处理（通过describe与len直接发现，通过0数据发现）
  2. 异常值处理（通过散点图发现）<br>
     一般遇到缺失值，处理方式为（删除，插补，不处理）；<br>
  插补的方式主要有：均值插补，中位数插补，众插补，固定值插补，最近数据插补，回归插补，拉格朗日差值，牛顿插值法，分段插值法等等 <br>
  4. 遇到异常值，一般处理方式为视为缺失值，删除，修补(平均数，中位数等等)不处理


* 数据清洗的操作步骤：
  1. 导入数据
  2. 先使用describe函数 查看基本统计量 发现异常数据
  3. 缺失值发现: 
     * describe中count 与 len(data) 差值 就是现实有几条缺失值
     * 0数据发现：decribe中有无0数据
     * 画散点图（横轴为价格，纵轴为评论数）：通过图发现异常的点
       在程序中查找到点
       1. 得到所有的行数和列数 
  4. 处理缺失值：中位数处理

  
 * 数据探索
   * 探索数据的分布规律
   * 处理的基本思路：
     1. 处理成直方图：看对应的频率的分部情况
     2. 首先得到 上限 和 下限  组距
     3. 极差：最大值 - 最小值 得到距离
     4. 组距：极差/组数 
     5. 绘制直方图


## 数据建模

#### 数据建模概念
* 数据建模： 对现实世界各类数据的抽象组织，建立一个适合的模型对数据进行处理 <br>
  在数据分析与挖掘中，我们通常要根据一些数据建立起特定的模型，然后处理 <br>
  模型的建立需要依赖于算法，一般常见的算法有：
  1. 分类
  2. 聚类
  3. 关联
  4. 回归等


#### Python数据分类实现过程
* 数据分类主要处理现实生活中的分类问题：
  1. 首先明确需求并对数据进行观察
  2. 其次，确定算法
  3. 确定步骤
  4. 编程实现

#### 常见的分类算法
1. KNN算法
2. 贝克斯方法
3. 决策树
4. 人工神经网络
5. 支持向量机（SVM）


#### 关联规则算法
1. 关联分析Apriori算法学习笔记-Python
http://www.jianshu.com/p/1fec92315b17




## 人工智能相关
* 基于MXNet的交通标志识别深度神经网络构建
http://www.infoq.com/cn/articles/an-introduction-to-customizing-a-neural-network
*  用python实现QQ机器人 
http://blog.chinaunix.net/uid-31012107-id-5765857.html
* Keras:基于Python的深度学习库
http://keras-cn.readthedocs.io/en/latest/


  
  
 
     
  








     


