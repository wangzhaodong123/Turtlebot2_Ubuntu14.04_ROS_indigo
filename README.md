# Turtlebot2_Ubuntu14.04_ROS_indigo
实验室的机器人Turtlebot2的软件环境安装记录。

一，清单（大白菜，easybcd，uiso可能需要更新）
	
	DaBaiCai_STA_bd.exe：大白菜系统安装工具，可用于win7的安装（http://www.dabaicaipe.cn/）

	EasyBCD_2.2.exe：Easybcd，用于win7和linux引导向的建立（https://www.softpedia.com/get/System/OS-Enhancements/EasyBCD.shtml）

	ubuntu-14.04.5-desktop-amd64.iso：ubuntu14.04，64位系统（https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/）

	uiso9_cn.exe：安装双系统时，制作启动盘的软件（https://cn.ultraiso.net/xiazai.html）

	Win7_x86c_6.3.GHO：win7镜像文件（这个你自己来吧）

	kinect驱动(openni、NITE、Sensor)：Kinect的驱动，注意在32位的Ubuntu14.04是不能用的（链接：https://pan.baidu.com/s/1znOatsnRhRFeqwQr2sHL0Q 密码：5o1q）
二，安装说明
	
	（1）win7安装（DaBaiCai_STA_bd.exe + Win7_x86c_6.3.GHO + U盘）

		【1】准备除了要安装win7的另外一台电脑，并安装DaBaiCai_STA_bd；
		【2】将Win7_x86c_6.3.GHO复制到需要安装win7的电脑上，记住位置；
		【3】在装有DaBaiCai_STA_bd的电脑上插上U盘（会格式化U盘，注意备份），打开DaBaiCai_STA_bd，软件会自动识别U盘，点击开始制作；
		【4】将制作好的U盘插到需要安装win7的电脑上，开机，同时连续按F12，并选择从U盘启动；
		【5】进入大白菜界面后，选择WIN8 PE标准版并进入；打开大白菜PE装机工具，映像文件路径选择【2】的镜像路径，分区选择C盘，开始制作；
		【6】重启电脑，拔掉U盘，系统会自动安装驱动并等待重启；
		【7】安装完成；
		
	（2）Ubuntu14.04双系统安装说明（EasyBCD_2.2.exe + ubuntu-14.04.5-desktop-amd64.iso + uiso9_cn.exe + U盘）
	
		（安装Windows10,Ubuntu双系统14.04LTS记录：https://www.cnblogs.com/arcsinw/p/5303615.html）
		（Ubuntu安装时怎样分区：https://www.cnblogs.com/zhchoutai/p/8721763.html）
		（ubuntu系统安装时的分区方案：https://blog.csdn.net/young951023/article/details/79382854）
		【1】准备除了要安装双系统的的另外一台电脑，并安装EasyBCD_2.2.exe和uiso9_cn.exe；
		【2】在装有uiso9_cn的电脑上插入U盘，打开uiso9_cn，文件->打开，选择需要装的ubuntu-14.04.5-desktop-amd64.iso，启动->写入硬盘镜像，硬盘驱动器选择插入的U盘，点击写入；
		【3】打开需要安装双系统的电脑，进入win7，计算机->管理->磁盘管理，选择准备放置ubuntu的盘（已备份，不要和win7放在一个盘），右击->压缩卷，根据自己需要输入需要压缩的大小，关机；
		【4】将制作好的U盘插入需要安装双系统的电脑，开机，同时连续按F12，并选择从U盘启动；
		【5】启动之后选择，install ubuntu，选择自己想要的语言（最好英语），网络可以不连接，一路继续直到安装类型时，选择最下方的“其他选项”（目的是为了自己创建分区），继续；
		【6】找到并双击【3】所开辟的空间freespace，创建四个基本分区：
			1,swap：和计算机内存相当，用于：swapspace
			2,/：	一般15-20G，用于Ext4，挂载点：/
			3,/boot：300M，用于Ext4，挂载点：/boot
			4,/home：可以尽量大一些，或者剩余的都用作/home，50G，用于Ext4，挂载点：/home
			安装启动引导，选择刚才分的/boot的分区，继续；
		【7】接下来的根据自己需要继续就可以了，包括语言，地区，主机名和密码，等安装完成之后，关机；
		【8】添加linux启动项。打开计算机，此时应该会进入win7系统，打开EasyBCD，添加新条目，操作系统选择Linux/BCD，驱动器选择刚才的/boot分区，点击添加，此时在编辑引导菜单便会有win7和linux的两个引导向；
		【9】如此，重启，便会出现win7和linux的选择界面。
			
	（3）双系统下卸载ubuntu
	
		（Windows、Ubuntu双系统正确卸载Ubuntu系统：https://blog.csdn.net/yeqiang19910412/article/details/79121581）
		当linux的安装启动引导选择的不是/boot时，如果直接删除linux分区会导致win7也无法进入了；
		所以一是要注意在安装的时候，安装启动引导选择/boot，二是根据博客，先修复再删除；
	
	（4）ROS
	
		（Ubuntu14.04安装ROS Indigo：https://blog.csdn.net/myarrow/article/details/53046625）
		【1】安装
			sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
			sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net --recv-key 0xB01FA116
			sudo apt-get update
			sudo apt-get install ros-indigo-desktop-full
		【2】初始化
			sudo rosdep init
			sudo rosdep update
		【3】配置环境变量
			echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
			source ~/.bashrc
				
	（5）Turtlebot2软件包（http://wiki.ros.org/turtlebot/Tutorials/indigo/Turtlebot%20Installation）

	（6）Kinect驱动安装：kinect驱动(openni、NITE、Sensor)文件夹有详细说明
	
		Kinect的ROS包：
			【1】安装
				sudo apt-get install  ros-indigo-freenect-*
				rospack profile
				echo "export TURTLEBOT_3D_SENSOR=kinect" >> .bashrc
			【2】启动并查看深度图和rgb图
				roslaunch turtlebot_bringup minimal.launch
				roslaunch freenect_launch freenect-registered-xyzrgb.launch
				rosrun image_view image_view image:=/camera/rgb/image_color
				rosrun image_view image_view image:=/camera/depth_registered/image_raw
	
	（7）在安装或者编译时会出现缺少依赖项的错误，以下是常见的（以后尽量补充）：
		
		【1】OpenGl （OpenGl env setup ubuntu14.04：https://github.com/cheyiliu/All-in-One/wiki/OpenGl-env-setup---ubuntu14.04）
			sudo apt-get install build-essential
			sudo apt-get install libgl1-mesa-dev
			sudo apt-get install libglu1-mesa-dev
			sudo apt-get install libglut-dev  or  sudo apt-get install freeglut3-dev
