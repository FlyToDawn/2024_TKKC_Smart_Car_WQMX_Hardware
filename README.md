# 2024年智能车竞赛嘉庚学院完全模型的硬件方案

## 文件需要导入立创EDA专业版！！！

#### 介绍
2024年嘉庚学院智能车完全模型组硬件方案开源，采用立创EDA进行设计。

#### 方案设计概述

本方案根据2024年第十九届全国大学生智能车竞赛完全模型相关要求进行设计，通过四次大迭代与数次小迭代设计，使得方案更加稳定。整体设计思路参考往年完全模型组的技术报告、赛曙公司开源的智控板设计方案与逐飞科技的方案综合评价后进行设计。考虑到整车重心问题，需要设计左右相近的两块电路板并将其连接起来。

##### 所需的模块分析

整车需要12V供电，有一个555电机驱动，一个数字舵机负责车辆转向，需要预留编码器接口PH2.0 4pin，采用逐飞科技TC264D核心板作为下位机主控，上位机为百度公司Edgeboard赛事专用板卡，上下位机通过串口进行通信。车辆的两块电路板连接接口需要预留。

##### 整车模块选型

电池采用3S锂电池，额定电压11.1V，满电12.6V，电源稳压部分采用德州仪器公司TPS5450DDAR，为整车提供了5V电源和舵机电源。对于3.3V电源，采用了AMS1117型LDO稳压芯片。电机驱动部分采用DRV8701电机控制芯片和TPH1R403NL型MOS管进行设计。

#### 现行版本的不足与需要改进之处

##### 1.Edgeboard供电

Edgeboard的供电部分虽说有1000uF大电容作为切换时瞬时供电的电容，但并没有电源的滤波电容，而且在第一次切换的时候可能会导致切换失败，不知道原因，需要未来后人们的智慧来改进了。

##### 2.电池电压检测

现行的方案并没有电池电压的检测部分，这就导致在比赛和调试过程中可能会导致电池过放，进而导致财产损失（电池坏了），后续可以在电池电源附件加一个可以用于电池电压检测的接口

##### 3.电池接口

现行的方案有XT60和T型插头两种方案，但是在只使用XT60的情况下，可能会有几率短路T插接口，进而导致电池短路引发爆炸等危险。（虽说可以给T插加一个保护盖）此外，现行板子的尺寸长边超出嘉立创免费打样要求的100mm要求，会导致打板成本较高。

##### 4.器件布局

现行的方案在DC-DC电路部分的电路布局可能不是最佳布局方案，可能需要后人进行相关的改进

##### 5.没有电池防反接措施

现行的方案上没有设计电池反接保护措施

##### 6.舵机防倒灌设计

舵机的信号没有倒灌设计

##### 7.没有预留键盘控制和屏幕外设接口

现行的方案没有预留车上的键盘和屏幕，调参数可能较为困难

##### 8.没有IMU的预留接口

目前没有预留出IMU所需要的接口
