# FireflyWorkSpace
该项目主要是对于FireFlyRK3288这个开发板的所有功能开发的一种设计，将所有的开发过程全部都记录了。

## 下载源码
百度云盘下载：
https://pan.baidu.com/share/init?surl=LC-YfxayV2707WX1ZZzOmA 密码为1234

## docker构建编译环境

打开2.docker，然后在WCL输入：

> docker build -t sdkcompiler .

如图所示：
![](/1.Docs/images/docker.png)

随后需要将源码文件绑定：

>docker run --privileged --mount type=bind,source=G:\dockerspace\,target=/home/firefly/proj --name="ubuntu18" -h firefly -it sdkcompiler

我这里是指向于G盘中dockerspace目录下volume映射到/home/firefly/proj下

此时你将进入docker

如下图所示：

![](/1.Docs/images/docker2.png)

> md5sum rk3288_linux_release_v2.5.0a_20230510_split_dir/*firefly_split*

```
f3b9309c574e04491a9e9f3e7a5c5540  rk3288_linux_release_v2.5.0a_20230510_split_dir/rk3288_linux_release_v2.5.0a_20230510_firefly_split.file0
fb0cd76f518405441bbc2ad2334ee6b9  rk3288_linux_release_v2.5.0a_20230510_split_dir/rk3288_linux_release_v2.5.0a_20230510_firefly_split.file1
cb26fddb36d49ff6b79f2fc934a731c1  rk3288_linux_release_v2.5.0a_20230510_split_dir/rk3288_linux_release_v2.5.0a_20230510_firefly_split.file2
43aa8447d4ef303ce41274c6ea7b00a2  rk3288_linux_release_v2.5.0a_20230510_split_dir/rk3288_linux_release_v2.5.0a_20230510_firefly_split.file3
c6c1ed77033af3d26be24974dda1b2aa  rk3288_linux_release_v2.5.0a_20230510_split_dir/rk3288_linux_release_v2.5.0a_20230510_firefly_split.file4
```

然后进行解压缩：

> cat rk3288_linux_release_v2.5.0a_20230510_split_dir/*firefly_split* | tar -xzv

![](/1.Docs/images/docker3.png)

>  cd rk3288_linux_release_v2.5.0a_20230510

>  .repo/repo/repo sync -l

![](/1.Docs/images/docker4.png)

> sudo apt install tree

> tree -L 1

![](/1.Docs/images/docker5.png)

这里我使用buildroot版本

> ./build.sh firefly-rk3288-buildroot.mk

全部自动编译并打包：

> ./build.sh

## 分区表
parameter 分区表：device/rockchip/rk3288/parameter-buildroot.txt
package-file 文件用于打包固件时确定需要的分区镜像和镜像路径，同时它需要与 parameter.txt 文件保持一致
具体看tools/linux/Linux_Pack_Firmware/rockdev/rk3288-ubuntu-package-file


# 参考

https://wiki.t-firefly.com/zh_CN/Firefly-RK3288/linux_compile.html