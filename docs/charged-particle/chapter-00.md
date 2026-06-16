# 前言

![](images/39a203b7775f2d96805992bd66b997a6c871c6816e7f0cbee6c3d8c968c931e0.jpg)

## CST Studio Suite 2025

## 带电粒子仿真

![](images/b67a147709b8bcda03e73a96ca11965d481430d2509ea5dd33f6dc5dd99a0914.jpg)

<details>
<summary>图中文字</summary>

3D
V+R
i'i
</details>

## 3DEXPERIENCE?

工作流程与

求解器概述

版本 2025.0 - 2024/8/21

## 版权

© 1998-2024 Dassault Systemes Deutschland GmbH。CST Studio Suite 是 Dassault Systèmes 的产品。

保留所有权利。

本文档中的信息如有更改，恕不另行通知。本文档所述软件依据许可协议或保密协议提供。该软件只能按照这些协议的条款使用。

未经 Dassault Systèmes 书面许可，除购买者个人使用目的外，不得以任何形式或通过任何电子或机械方式复制、存储于检索系统或传输本文档的任何部分，包括影印和录制。

## 商标

CST、CST 标志、Cable Studio、CST BOARDCHECK、CST EM STUDIO、CST EMC STUDIO、CST MICROWAVE STUDIO、CST PARTICLE STUDIO、CST Studio Suite、EM Studio、EMC Studio、Microstripes、Microwave Studio、MPHYSICS、MWS、Particle Studio、PCB Studio、PERFECT BOUNDARY APPROXIMATION (PBA)、Studio Suite、IdEM、Spark3D、Fest3D、Antenna Magus、Opera、3DEXPERIENCE、3DS 标志、Compass 图标、IFWE、3DEXCITE、3DVIA、BIOVIA、CATIA、CENTRIC PLM、DELMIA、ENOVIA、GEOVIA、MEDIDATA、NETVIBES、OUTSCALE、SIMULIA 和 SOLIDWORKS 均为 Dassault Systèmes 的商业商标或注册商标。Dassault Systèmes 是一家依据法国法律成立的欧洲公司（Societas Europaea），并在凡尔赛贸易和公司注册处以编号 322 306 440 注册；上述商标也可能属于其在美国和/或其他国家的子公司。所有其他商标均归其各自所有者所有。使用 Dassault Systèmes 或其子公司的任何商标均须获得其明确书面批准。

DS 产品和服务名称可能是 Dassault Systèmes 或其子公司的商标或服务标志。

3DS.com/SIMULIA

## 目录

第 1 章 - 引言 . . 6

欢迎 . 6

如何快速入门 .. 6

用于粒子动力学仿真的 CST Studio Suite . 6

谁使用 CST Studio Suite 进行粒子动力学仿真？..

粒子动力学仿真的主要功能 ..

概述 .. 7

结构建模..

粒子跟踪仿真器.. 8

静电 Particle-in-Cell 仿真器.. 8

Particle-in-Cell 仿真器 .. 9

尾场仿真器.. 10

本征模仿真器 . 11

静电仿真器 . 1 2

静磁仿真器 . 12

可视化与二次结果计算 . . 13

结果导出 .. 13

自动化... . 13

关于本手册 . . 13

文档约定 . 14

您的反馈 . 14

第 2 章 - 仿真工作流程... . 15

仿真工作流程：粒子跟踪 . . 15

结构 . 15

创建新项目.. . 16

打开跟踪 QuickStart 指南.. . 18

定义单位 . 18

定义背景材料 . 19

结构建模 . 19

定义电势和磁体.. 25

可视化并细化网格 . . 27

定义粒子源 .. 29

定义边界条件 . . 32

开始仿真 . 34

分析结果 .. 36

模型参数化... 3 9

结构自动优化 . 4 5

附加信息：粒子跟踪求解器的更多设置 ... . 47

附加信息：在静磁计算中将 PEC 作为普通材料处理.. . 48

附加信息：在跟踪求解器中使用四面体网格 .. .. 49

小结 .... 52

## 仿真工作流程：电磁 Particle-in-Cell... . 53

结构 . 53

创建新项目.. 54

打开 PIC QuickStart 指南... 55

定义单位 . 5 6

定义背景材料 . 56

结构建模 . 56

定义粒子源 . . 62

仿真设置.. 6 6

细化网格.. . 68

定义粒子监视器.. . 69

开始仿真 . . 70

分析仿真结果 . . 70

小结 . . 73

## 仿真工作流程：尾场 ... . 75

结构 . . 75

创建新项目.. 75

打开尾场 QuickStart 指南. 77

定义单位 . . 78

定义背景材料 . . 78

结构建模 . . 78

定义粒子束源. . 82

定义边界和对称条件... . 83

可视化网格.. . 84

定义 2D 时域场监视器... . 86

开始仿真 . . 87

分析仿真结果 . 88

附加信息：尾场后处理.. . 90

小结 . 92

第 3 章 - 求解器概述 .. . 93

粒子跟踪求解器 . . 93

Particle-in-Cell 求解器 ... . 94

静电 Particle-in-Cell 求解器 ... . 94

尾场求解器 . . 95

附加功能 . 96

粒子与材料的相互作用 96

蒙特卡洛碰撞.. . 97

粒子合并. 98

耦合仿真 . 98

考虑电磁场 . 98

粒子接口 . . 100

粒子表面损耗导出.. . 101

加速功能 . . 102

第 4 章 - 查找更多信息... . 104

QuickStart 指南... . 104

在线文档.. . 104

教程和示例.. . 105

技术支持 .. . 105

宏语言文档 . . 105

变更历史. . 105
