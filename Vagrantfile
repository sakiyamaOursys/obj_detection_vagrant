VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos65"
  config.vm.network :forwarded_port, guest:22, host:2001, id:"ssh"
  config.vm.network :forwarded_port, guest:80, host:8080, id:"http"
  config.vm.network :private_network, ip:"192.168.33.10"
  config.vm.synced_folder ".", "/vagrant", mount_options: ['dmode=777','fmode=755']
  config.vm.provision "shell", inline: <<-EOT
  
        # timezone
        cp -p /usr/share/zoneinfo/Japan /etc/localtime

        # iptables off
        /sbin/iptables -F
        /sbin/service iptables stop
        /sbin/chkconfig iptables off

        # Apache
        sudo yum -y install httpd
        sudo /sbin/service httpd restart
        sudo /sbin/chkconfig httpd on

        # php
        sudo yum -y install php

         #nano
        sudo yum -y install nano

		#unzip
        sudo yum -y install unzip

		#gnu gcc
		#sudo yum -y install gmp-devel mpfr-devel  libmpc-devel
		#sudo curl -O ftp://ftp.gnu.org/gnu/gcc/gcc-4.9.2/gcc-4.9.2.tar.gz; tar zxf gcc-4.9.2.tar.gz
		#cd gcc-4.9.2
		#sudo ./contrib/download_prerequisites
		#sudo mkdir build
		#cd build
		#sudo ../configure --enable-languages=c,c++ --disable-multilib
		#long long time.....
		#sudo make
		#sudo make install
		
		#cmake 2.8
		sudo yum -y install cmake
		
		#opencv-2.4.9
		#sudo wget -O OpenCV-2.4.9.zip http://fossies.org/linux/misc/opencv-2.4.9.zip
		#sudo unzip OpenCV-2.4.9
		#cd opencv-2.4.9
		#sudo mkdir build
		#cd build
		#sudo cmake ..
		#sudo make -j2
		#sudo make install
				
		#path
		#sudo sh -c "echo '/usr/local/lib' >> /etc/ld.so.conf"		
		#sudo sh -c "echo '/usr/local/bin' >> /etc/ld.so.conf"			
		#sudo ldconfig
		
		#git
		sudo yum install -y git
		
		#change dir
		cd /vagrant/prgm/php/
		
		#git source
		git clone https://github.com/sakiyamaOursys/object_detection_server.git
		cd object_detection_server
		sudo chmod 777 build_cppfile.sh
		sudo ./build_cppfile.sh
		sudo cp /usr/local/share/OpenCV/haarcascades/haarcascade_frontalface_default.xml haarcascades/haarcascade_frontalface_default.xml 

  EOT
end