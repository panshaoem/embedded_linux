编译程序
用 x86 的 ubuntu自带的gcc可编译hello.c文件，命令如下
    gcc -o test_x86 hello.c
这样就能生成可执行程序 test_x86, 用以下命令获得文件详情
    file test
        test_x86: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), 
        dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, 
        for GNU/Linux 3.2.0, BuildID[sha1]=1bfbab34b20cf562f5aaa47dae0292fd927a426b, not stripped
文件并不能直接被arm架构的树莓派3B+直接运行，因此需要使用交叉编译工具链
到github下载并解压树莓派用的交叉编译工具链  tools-master.zip
在文件夹内随便找了个gcc尝试编译 hello.c, 例如以下指令，发现不能在树莓派上执行
    ~/tools-master/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc-4.9.3 -o test_arm_4.9.3 hello.c
树莓派上运行test_arm_4.9.3时，总会报以下错误
    bash: ./test_arm_4.9.3: No such file or directory

解决方案如下
    1) 获取 test_arm_4.9.3 详情
    file test_arm_4.9.3
        test_arm_4.9.3: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), 
        dynamically linked, interpreter /lib/ld-linux-armhf.so.3, 
        for GNU/Linux 2.6.32, not stripped
    2) 到当前树莓派获取任意可执行文件详情
            /usr/bin/find: ELF 64-bit LSB shared object, ARM aarch64, version 1 (SYSV), 
            dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, 
            BuildID[sha1]=63e1f8b169ecea05b70ce3e49dd2a466a1f5ad0c, for GNU/Linux 3.7.0, stripped
    3) 发现树莓哦当前架构是 ARM aarch64，因此无法执行 test_arm_4.9.3
    4) 在下载 tools-master.zip 的 git 仓库的 README 发现以下指令可直接安装，树莓派的交叉编译工具链
        sudo apt-get install gcc-aarch64-linux-gnu
    5) 编译
        aarch64-linux-gnu-gcc -o test_aarch64 hello.c
