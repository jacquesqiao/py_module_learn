### python module package导入的一些知识总结

1. import 语句总是绝对导入的，相对导入只用于from xxx import.
1. 只有同属一个package时，module才能用

	```python
	from ..a import b
	```
	导入上一层目录的module。

1. python xxx.py的方式执行python脚本的时候，无法用相对导入import上一层目录的函数，因为这种方式xxx.py与上层目录不属于同一个package。例如执行：

	```shell
	python mod_3.py
	```
	会报错：
	
	```shell
	Traceback (most recent call last):
	  File "mod_3.py", line 2, in <module>
	    from ..mod_1 import test
	ValueError: Attempted relative import in non-package
	```
	
1. 但是可以在py_module_learn上一层目录执行：
	
	```python
	import py_module_learn.pkg_1.mod_3 
	```
	
1. 使用python xxx.py执行的时候，默认搜索sys.path中的路径下的module，所以可以通过修改sys.path的方式，添加相对搜索路径：

	```python
	import sys
	sys.path.append("..")
	```
	
	例如到pkg_1目录下执行：
	
	```python
	python mod_2.py
	```
	
	是可以的，然而这种执行方式和执行命令的位置有关，例如如果在上一层目录执行：
	
	```shell
	python pkg_1/mod_2.py
	```
	
	会报错：
	
	```shell
	Traceback (most recent call last):
	  File "pkg_1/mod_2.py", line 4, in <module>
	    import mod_1
	ImportError: No module named mod_1
	```