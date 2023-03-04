# 目标 : 依赖
# 目标文件 : 依赖文件
test : main.o funb.o
	gcc -o test main.o funb.o

main.o : main.c
	gcc -c -o main.o main.c

funb.o : funb.c
	gcc -c -o funb.o funb.c