# 目标 : 依赖
# 目标文件 : 依赖文件
test : main.o funb.o func.o		# 【 $^, 所有依赖文件 】
	gcc -o test $^

%.o : %.c						# 【 %, 通配符】【 $@, 目标 】【 $<, 第一个依赖文件 】
	gcc -c -o $@ $<