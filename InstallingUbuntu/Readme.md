
Caution: Remove wings from your drone before start

1) Download Ubuntu desktop from 

    http://old-releases.ubuntu.com/releases/16.04.3/ 
2) Causion don’t use latest Ubuntu as it may not supported by aero drone
3) Create bootable disk, I used rufus
    ![](https://github.com/BhaskarTrivedi/Intel-Aero-Drone/blob/master/Img/BootablePD.jpg)
 
4) Make sure your drone is connected to power cable, battery is not enough for installation.
    visit https://github.com/BhaskarTrivedi/Intel-Aero-Drone/tree/master/MinimumThingYouShouldHaveToWorkOnIntelAeroDrone 
5) Start your drone by pressing power button setup
6) Press ESC to enter BIOS
7) Select boot manager 
    ![](https://github.com/BhaskarTrivedi/Intel-Aero-Drone/blob/master/Img/IMG_20190201_142118538_BURST000_COVER_TOP.jpg)
8) Select USB Device
    ![](https://github.com/BhaskarTrivedi/Intel-Aero-Drone/blob/master/Img/IMG_20190201_142133333.jpg)
9) Select install ubuntu
    ![](https://github.com/BhaskarTrivedi/Intel-Aero-Drone/blob/master/Img/IMG_20190201_142219576.jpg)
10) While installing ubuntu I ignored third party flash and MP3 and other media, to save space
11) I selected clean installation 
12) Enter username and password
13) Install ssh<br/>

        a.	sudo apt-get update<br/>
        b.	sudo apt-get upgrade<br/>
        c.	sudo apt-get install openssh-server<br/>
        
14) Intel aero reprository<br/>

        a.	echo 'deb https://download.01.org/aero/deb xenial main' | sudo tee /etc/apt/sources.list.d/intel-aero.list<br/>
        b.	wget -qO - https://download.01.org/aero/deb/intel-aero-deb.key | sudo apt-key add -<br/>
        c.	sudo apt-get update<br/>
        d.	sudo apt-get upgrade<br/>
        e.	sudo apt-get -y install gstreamer-1.0 libgstreamer-plugins-base1.0-dev libgstrtspserver-1.0-dev gstreamer1.0-vaapi gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-libav ffmpeg v4l-utils python-pip<br/>
        f.	sudo pip install pymavlink<br/>
        g.	sudo apt-get -y install aero-system<br/>
        h.	sudo reboot<br/>
        
 15) Intel Aero Maintenance tools<br/>
 
    a.	sudo mkdir /etc/mavlink-router/config.d<br/>
    b.  create file<br/>
        sudo gedit /etc/mavlink-router/config.d/qgc.conf <br/>
    c. Make entry to above file<br/>
    
        •	[UdpEndpoint wifi]<br/>
        •	Mode = Normal<br/>
        •	Address = Your laptop Ip address<br/>
        
    d. Flash BIOS<br/>
    
        •	sudo aero-bios-update<br/>
        •	sudo reboot<br/>
        •	using latest Bios from intel site<br/>
        •	Download latest bios from <br/>
                    https://downloadcenter.intel.com/download/27399/Intel-Aero-Platform-for-UAVs-Installation-Files<br/>
        •	rpm2cpio aero-bios-01.00.16-r1.corei7_64.rpm | cpio -idmv<br/>
        •	sudo mv BIOSUPDATE.fv /boot<br/>
        •	sudo reboot<br/>
        
     e. FPGA<br/>
        
        •	sudo jam -aprogram /etc/fpga/ aero-compute-board.jam<br/>
            
     f. Flight Controller
        
        •	cd /etc/aerofc/px4/<br/>
        •	sudo aerofc-update.sh nuttx-aerofc-v1-default.px4<br/>
            Trouble shoot<br/>
            •	If getting attempting reboot error thr to install recorevry FPGA from /etc/fpga<br/>
                    
     g. Intel RealSense SDK<br/>
        
        •	sudo apt-get -y install git libusb-1.0-0-dev pkg-config libgtk-3-dev libglfw3-dev cmake<br/>
        •	git clone -b legacy --single-branch https://github.com/IntelRealSense/librealsense.git<br/>
        •	cd librealsense<br/>
        •	mkdir build && cd build<br/>
        •	cmake ../ -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true<br/>
        •	make<br/>
        •	sudo make install<br/>
        •	Install ROS using ROS installation guide given at intel aero drone<br/>


        
            
