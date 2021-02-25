# action-WSL2-Linux-Kernel

[![Auto build kernel for wsl2](https://github.com/liwenjie119/action-WSL2-Linux-Kernel/workflows/Auto%20build%20kernel%20for%20wsl2/badge.svg)](https://github.com/liwenjie119/action-WSL2-Linux-Kernel/actions)

## 说明

此仓库为自动编译WSL2内核，源码来自 [xieyubo/WSL2-Linux-Kernel](https://github.com/xieyubo/WSL2-Linux-Kernel) 综合 [ActiveIce/WSL2-Linux-Kernel](https://github.com/ActiveIce/WSL2-Linux-Kernel)

每周自动更新编译

## 系统要求

Windows 10 版本 2004 (OS 内部版本 20145) 或更高版本
``` PowerShell
winver.exe
```

启用 “适用于 Linux 的 Windows 子系统” “虚拟机平台” (需要重启)
``` PowerShell
wsl.exe --install
```

## 下载

下载系统镜像、引导程序、内核至同一文件夹

[Ubuntu 20.10 (Groovy)](https://cloud-images.ubuntu.com/groovy/current/groovy-server-cloudimg-amd64-wsl.rootfs.tar.gz)

[Ubuntu Loader](https://raw.githubusercontent.com/liwenjie119/action-WSL2-Linux-Kernel/master/ubuntu.exe)

[WSL2-Linux-Kernel](https://raw.githubusercontent.com/liwenjie119/action-WSL2-Linux-Kernel/master/kernel)


将 `focal-server-cloudimg-amd64-wsl.rootfs.tar.gz` 重命名为 `install.tar.gz`

## 配置
在用户文件夹的根目录 `C:\Users\<yourUserName>` 新建文件 `.wslconfig`

在 `.wslconfig` 文件中按格式填入内核路径、分配CPU核心数、分配内存数量

``` PowerShell
[wsl2]
kernel=E:\\Ubuntu\\kernel
processors=4
memory=4GB
swap=1GB
swapFile=E:\\Ubuntu\\swap.vhdx
#localhostForwarding=true
```

## 安装和使用
双击 `Ubuntu.exe`

首次使用按提示设置用户名和密码即可


#### 清理 VHDX 磁盘
VHDX 磁盘文件不会随着 Ubuntu 系统内文件的删除而变小，若磁盘文件太大，可以手动缩小

启用 “Windows Powershell 的 Hyper-V 模块” (需要重启)
``` PowerShell
dism.exe /online /enable-feature /featurename:Microsoft-Hyper-V-Management-PowerShell /all /norestart
```
清理命令 ( `-Path` 后面参数是 VHDX 文件的路径)
``` PowerShell
wsl.exe --shutdown
Optimize-VHD -Path E:\Ubuntu\ext4.vhdx -Mode Full
```
