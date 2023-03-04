# 目标 : 依赖
# 目标文件 : 依赖文件
test : main.o funb.o func.o		# 【 $^, 所有依赖文件 】
	gcc -o test $^

%.o : %.c						# 【 %, 通配符】【 $@, 目标 】【 $<, 第一个依赖文件 】
	gcc -c -o $@ $<

clean :
	rm *.o

.PHONY : clean	# 使 clean 变为假想目标，这样即使目录里面有为clean的且up to date的目标文件，make clean 依然能执行
# make的语法为 make [目标] 。若无目标，默认第一个目标