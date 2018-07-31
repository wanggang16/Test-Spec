# Test-Spec
字节服务器及部件引入测试规范，含整机，CPU，硬盘，网卡，内存等  
文档版本:   0.1  
日期:   6/25/2018

## 测试前准备   
### 外观检查  
机框是否有碰撞/变形 ； 散热器，挡风罩是否有遗漏；VGA/USB/RJ45接口连接器是否正常。确认无问题后，进行下一步配置确认。

### 确认设备硬件配置正确    
#### 测试机信息  
测试机型：  
ODM厂商：  
>CPU  
厂家*型号*数量  
>内存  
厂家*容量*数量  
>硬盘   
厂家*型号*容量*数量  
>OCP 网卡  
厂家*型号*数量  
>其他PCIE 外插卡  
Slot1:  
Slot2:  
Slot3:  
…..  
类型*规格*数量  

## 系统功能测试  
### BIOS SEPUP确认  
#### 测试目的  
1.确认系统的BIOS/BMC的版本
2.确认CPU/内存/硬盘/PCIE外插卡 型号*数量
3.查看网卡的MAC是否可读
#### 测试方法   
开机，进入BIOS SETUP界面，记录BIOS/BMC当前版本，确认CPU/内存/硬盘/PCIE外插卡 型号*数量 与配置相符，所有硬件设备都有读取到。
确认/记录 网卡的MAC ADDR  
确认BIOS设置Legacy  

### PXE系统引导  
#### 测试目的  
确认系统PXE功能，并安装OS  
#### 测试方法   
1. PXE功能是否默认为enable;  
2. 系统从PXE服务器启动，安装OS  
3. OS 版本：  
Linux n22-145-017 4.9.0-6-amd64 #1 SMP Debian 4.9.88-1+deb9u1 (2018-05-07) x86_64 GNU/Linux  


### 接口/开关检查   
#### 测试目的  
拔插 线缆 或 按开关，设备使用任然正常
#### 测试方法   
VGA
USB
RJ45/SFP…网口
串口
UID 按键
Power Button 按键
AC电源线
硬盘

拔插10次，接口功能仍然正常使用，BMC 能准确记录AC电源线，硬盘的拔插log

###  清除Log， 
#### 测试目的 
清理BMC 和 系统 Log，确认BIOS /OS /BMC 时间相同  
#### 测试方法   
清理软件Log，准备启动稳定性测试


### Cycle 测试     
#### 测试目的  
测试整机系统在AC/DC/Reboot多次过程中是否有异常
#### 测试方法   
Reboot :100次
AC cycle:100次
DC Cycle:100次 

### 整机功能压力测试 
#### 测试目的  
确认CPU/内存/硬盘/PCIE外插卡 在系统压力下工作正常  
#### 测试方法   
使用 Burnin Test 脚本，根据系统实际配置进行设定，压力测试一星期。
查看Burnin 无Error， BMC 日志无故障记录，系统message 日志无error.   

### CPU测试  
#### 测试目的  
确认CPU在整机的稳定性/兼容性
#### 测试方法   
SPEC CPU 


### 内存测试  
#### 测试目的  
确认新内存在整机的稳定性/兼容性
#### 测试方法   
STREAM


### SATA硬盘  
#### 测试目的  
确认新内存在整机的稳定性/兼容性
#### 测试方法   
FIO

脚本链接：  
https://sysrepo.byted.org/system/ServerEva/tree/master/FLASH/fioconfig


### 网卡  
#### 测试目的  
确认新内存在整机的稳定性/兼容性  
#### 测试方法   

ftp://ftp.netperf.org/netperf/netperf-2.5.0.tar.gz

检查节点NIC LED颜色和状态是否与规格一致
带宽确认：
选两台服务器测试带宽，然后观察输出。     命令如下：     服务器A：ib_write_bw -D 60      服务器B：ib_write_bw -D 60 <服务器 A IP>
延时性能确认
选两台服务器测试延迟，然后观察输出。     命令如下：     服务器A：ib_write_lat -a      服务器B：ib_write_lat -a <服务器 A IP>
NCSI功能验证
（大小包传输）














