
Caution: Remove wings from your drone before start

1) Download Ubuntu desktop from 

    http://old-releases.ubuntu.com/releases/16.04.3/ 
2) Causion don’t use latest Ubuntu as it may not supported by aero drone
3) Create bootable disk, I used rufus
    ![](https://github.com/BhaskarTrivedi/Intel-Aero-Drone/blob/master/Img/BootablePD.jpg)
 
4) Make sure your drone is connected to power cable, battery is not enough for installation.
    visit https://github.com/BhaskarTrivedi/Intel-Aero-Drone/tree/master/MinimumThingYouShouldHaveToWorkOnIntelAeroDrone to see complete setup
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
13) Install ssh
    a.	sudo apt-get update
    b.	sudo apt-get upgrade
    c.	sudo apt-get install openssh-server
14) Intel aero reprository
        a.	echo 'deb https://download.01.org/aero/deb xenial main' | sudo tee /etc/apt/sources.list.d/intel-aero.list
        b.	wget -qO - https://download.01.org/aero/deb/intel-aero-deb.key | sudo apt-key add -
        c.	sudo apt-get update
        d.	sudo apt-get upgrade
        e.	sudo apt-get -y install gstreamer-1.0 libgstreamer-plugins-base1.0-dev libgstrtspserver-1.0-dev gstreamer1.0-vaapi gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-libav ffmpeg v4l-utils python-pip
        f.	sudo pip install pymavlink
        g.	sudo apt-get -y install aero-system
        h.	sudo reboot
 15) Intel Aero Maintenance tools
        a.	sudo mkdir /etc/mavlink-router/config.d
        b.  create file
            sudo gedit /etc/mavlink-router/config.d/qgc.conf 
        c. Make entry to above file
            •	[UdpEndpoint wifi]
            •	Mode = Normal
            •	Address = Your laptop Ip address
        d. Flash BIOS
            •	sudo aero-bios-update
            •	sudo reboot
            •	using latest Bios from intel site
            •	Download latest bios from 
                    https://downloadcenter.intel.com/download/27399/Intel-Aero-Platform-for-UAVs-Installation-Files
            •	rpm2cpio aero-bios-01.00.16-r1.corei7_64.rpm | cpio -idmv
            •	sudo mv BIOSUPDATE.fv /boot
            •	sudo reboot
        e. FPGA
            •	sudo jam -aprogram /etc/fpga/ aero-compute-board.jam
        f. Flight Controller
            •	cd /etc/aerofc/px4/
            •	sudo aerofc-update.sh nuttx-aerofc-v1-default.px4
                Trouble shoot
                    •	If getting attempting reboot error thr to install recorevry FPGA from /etc/fpga
        g. Intel RealSense SDK
            •	sudo apt-get -y install git libusb-1.0-0-dev pkg-config libgtk-3-dev libglfw3-dev cmake
            •	git clone -b legacy --single-branch https://github.com/IntelRealSense/librealsense.git
            •	cd librealsense
            •	mkdir build && cd build
            •	cmake ../ -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true
            •	make
            •	sudo make install
            •	Install ROS using ROS installation guide given at intel aero drone


        
            
