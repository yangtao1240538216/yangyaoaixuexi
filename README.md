# my2048
## 针对2022.4.6的更新“weak AI in memory”:  
### 更新概述
本次“weak AI in memory”版本在原版游戏上添加了AI自动解题功能，本程序的AI功能较弱，大约能保证60%的概率算到2048，总分在30000左右
### 使用方法
打开网页后，按F12打开控制台，点击“AI auto run”按钮，出现弹窗“测试AI算法是否开始执行”，点击确认后，AI程序正式执行，  
控制台中会依次打印每一步的二维数组board和score，大约打印2、3千条记录之后，游戏结束，出现“游戏结束”弹窗，  
点击确认，游戏界面呈现AI自动解题的终止状态，控制台的board数组可以查看每一步的具体状态。
### 设计思想
本次更新名为“weak AI in memory”，即“内存中的弱人工智能”，本次AI算法思想为：  
> 1.在当前board情况下，依次选择4个方向中的一个  
> 
> 2.在可移动的前提下，将board在内存中的初始副本(initialVirtualBoard)按照指定的方向移动一次  
> 
> 3.将移动一个方向之后的initialVirtualBoard再备份成virtualBoard，用于随机移动测试  
> 
> 4.执行randomGamePlay()函数，该函数每次随机选择一个方向，将virtualBoard按该方向移动，计算得分，重复执行“随机移动-计算得分”操作，直至本次randomGamePlay()游戏结束  
> 
> 5.重复randomGamePlay()1000次(次数可以修改，一般而言，次数越多，最终实现2048的成功率越高，但听说有边界效应递减，目前尚未进行大规模测试)  
> 
> 6.在四个方向都分别执行相同若干次randomGamePlay()函数后，获取四个方向的总得分，选择其中分数最高的方向，作为board下一步的真实移动方向  
> 
> 7.重复1~6，直至board游戏结束
	
### 缺陷
当前版本的AI自动解题有以下缺陷：  
1、解题成功率不够高，各方向1000次模拟仅60~70%成功率  
2、代码冗余度高，代码复用性差  
3、算法的数学依据比较模糊，不够智能，评判依据过于暴力、粗糙  
4、没有运用到机器学习的思想  
5、AI自动解题时，游戏界面没有对应的动画更新（AI游戏解题没有设置时延，CPU处于全速运转，前端页面无法与之匹配，只能在游戏结束后显示最终画面）  
6、AI自动解题没有设置交互功能，一旦开始，就无法人为干预，既不能暂停，也不能在中途用按键修改
