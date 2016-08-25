#Build spark with Idea on windows7
##Party1 导入编译
* git下载Spark源码[spark_2.0.0](https://github.com/apache/spark.git)
		

		$ git clone https://github.com/apache/spark.git
* 修改pom.xml文件，java版本，maven版本等

		$ git checkout -b develop
* 切到develop brach, 运行(windows上建议用git bash，在导入IDEA之前，在命令行编译步骤不可省略)

		$ sbt clean compile or sbt assembly
* 以mvn项目的形式导入，建议用mvn,因为maven依赖解析快，sbt慢且会出现卡死。
* 等待项目导入完毕》》》》》》》》》》》》》》》》》》》==
* 这个时候预编译的作用来了，打开project-structure，选择spark-streaming-flume-sink module，将target文件的exclude取消，并且把target/scala-2.11/src_managed/main目录下面的compiled   _avro设为sourcefolder
* 还有module spark-catalyst下面的tagert，与target/scala-2.11/src_managed/main下面的antlr4，同样分别执行上一部的操作。
* 当然你可能还会遇到其他的module有这个问题，当运行rebuild出现找不到某个module的class的时候用这种方法解决，比较耗时。
* 都解决之后点击rebuild，等待build完成
* 编译成功
##part2 运行

####我们的目标是单步debug，以example module为例

* 在run tab下面配置一个application设置主类为SparkPi
* 这个时候直接点击run，会报一吨的class not defined错误
* 打开项目根目录的pom.xml
* 找到<module>examples</module>按Ctrl点开module的设置
* 把依赖的scope几乎全部设为compile,默认是provided
* 点击run,运行成功
* 当然还有一种远程调试的方法[连城教你build Spark](https://www.zhihu.com/question/24869894)
* 一切完成可以放心学习源码了。
