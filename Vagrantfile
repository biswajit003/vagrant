# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/7"
  class Username
        def to_s
            print "Enter your Telia Credentials .\n"
            print "Username: " 
            STDIN.gets.chomp
        end
    end
    
    class Password
        def to_s
            begin
            system 'stty -echo'
            print "Password: "
            pass = URI.escape(STDIN.gets.chomp)
            ensure
            system 'stty echo'
            end
            pass
        end
	end
  #config.vm.network :forwarded_port, guest: 80, host: 80, auto_correct:true
  #config.vm.network :forwarded_port, guest: 443, host: 443, auto_correct:true
  #config.vm.network :forwarded_port, guest: 8443, host: 8443, auto_correct:true
  #config.vm.network :forwarded_port, guest: 8080, host: 8080, auto_correct:true

  #config.vm.synced_folder "eclipse_workspace/", "/vagrant"
    
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "8192"
  
   
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", env: {"USERNAME" => Username.new, "PASSWORD" => Password.new}, inline: <<-SHELL

  #   apt-get update
  #   apt-get install -y apache2
  #cat /dev/null >test
  #toch file1
  #config.vm.provision :shell, path: "preinstall.sh"
  #config.vm.provision :shell, path: "install.sh"
  #config.vm.provision :shell, path: "configure.sh"
  
  #sudo service rem start

  sudo su
  sudo yum -y install wget
  sudo yum install -y unzip
  sudo yum install nano -y
  sudo yum install curl -y
  sudo yum -y install screen
  sudo yum install -y glibc.i686
  sudo yum -y install zip
  #sudo yum install https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.rpm
  sudo yum -y update
  cd /opt
  mkdir product
  cd product
  mkdir opencloud
  cd ~
  #cp -R /vagrant/* /opt/product/opencloud
  cd /opt/product/opencloud
  sudo usermod -a -G vboxsf vagrant
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/apache-ivy-2.4.0-bin.zip
  unzip apache-ivy-2.4.0-bin.zip 
  cd ~
  mkdir .ant
  cd .ant
  mkdir lib
  cd lib
  cp /opt/product/opencloud/apache-ivy-2.4.0/ivy-2.4.0.jar .
  cd ../..
  chmod -R 755 .ant 
  cd /opt/product/opencloud
  sudo mkdir jdk1.8.0_241
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/packerVSvmbcPOC/jdk-8u241-linux-x64.tar.gz
  sudo tar xzvf jdk-8u241-linux-x64.tar.gz -C /opt/product/opencloud/jdk1.8.0_241 --strip-components=1
  update-alternatives --install /usr/bin/java java /opt/product/opencloud/jdk1.8.0_241/bin/java 2
  alternatives --install /usr/bin/jar jar /opt/product/opencloud/jdk1.8.0_241/bin/jar 2
  alternatives --install /usr/bin/javac javac /opt/product/opencloud/jdk1.8.0_241/bin/javac 2
  alternatives --set jar /opt/product/opencloud/jdk1.8.0_241/bin/jar
  alternatives --set javac /opt/product/opencloud/jdk1.8.0_241/bin/javac
  
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/packerVSvmbcPOC/apache-ant-1.10.1.tar
  sudo tar xvf apache-ant-1*tar  --strip-components=1
  sudo ln -s /opt/product/opencloud/apache-ant-1.10.1 /usr/local/ant
  
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/sentinel-express-sdk-2.9.0.2.zip
  unzip sentinel-express-sdk-2.9.0.2.zip
  echo "JAVA_HOME=/opt/product/opencloud/jdk1.8.0_241">>~/.bashrc
  echo "JRE_HOME=/opt/product/opencloud/jdk1.8.0_241/jre">>~/.bashrc
  echo "ANT_HOME=/usr/local/ant">>~/.bashrc
  echo "ANT_LIB=/root/.ant/lib">>~/.bashrc
  echo "export JAVA_HOME">>~/.bashrc
  echo "export JRE_HOME">>~/.bashrc
  echo "export ANT_HOME">>~/.bashrc
  echo "export ANT_LIB">>~/.bashrc
  echo "export PATH=$PATH:/opt/product/opencloud/jdk1.8.0_241/bin:JRE_HOME=/opt/product/opencloud/jdk1.8.0_241/jre/bin:/usr/local/ant/bin:/root/.ant/lib:/opt/product/opencloud/sentinel-express-sdk">>~/.bashrc
  source ~/.bashrc
  
  cd /opt/product/opencloud
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/local-repo.zip
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/packerVSvmbcPOC/LIC-1243-Evaluation-License-TechM.tar
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/sdk.local.properties
  wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/ivy.properties
  sudo tar xvf LIC-1243-Evaluation-License-TechM.tar
  cd /opt/product/opencloud/sentinel-express-sdk
  unzip ../local-repo.zip
  cp ../ivy.properties .
  cp ../sdk.local.properties .
  ant init-sdk
  cd /opt/product/opencloud/sentinel-express-sdk/rhino-sdk
  
  ant install-rhino
    
  cd /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK
  rm -rf rhino-sdk.license
  cp /opt/product/opencloud/LIC-1243-Evaluation-License-TechM.license .
  mv LIC-1243-Evaluation-License-TechM.license rhino-sdk.license
  cd /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/client/etc
  rm -rf  client.properties
  touch client.properties
  echo "# RMI properties, file names are relative to client home directory
rhino.remote.host=127.0.0.1
rhino.remote.port=1199
rhino.remote.username=admin
rhino.remote.password=password

# Uncomment to provide a comma separated list of hosts for client failover support.
# rhino.remote.serverlist=hosta:1199,hostb:1199

javax.net.ssl.trustStore=rhino-client.keystore
javax.net.ssl.trustStorePassword=changeit
javax.net.ssl.keyStore=rhino-client.keystore
javax.net.ssl.keyStorePassword=changeit

# Port offset for snapshot operations
rhino.snapshot.baseport=22000


# Build properties
build.sysclasspath=first
failonerror=false
debug=yes
opt=no">>/opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/client/etc/client.properties

cd /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/

sed -i '/-Xms/s/.*/-Xms4096m/' /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/jvm_args
sed -i '/-Xmx/s/.*/-Xmx4096m/' /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/jvm_args
sed -i '/# select the server VM/{n;s/.*/-Dtransaction.default_timeout=300000/}' /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/jvm_args
cd /opt/product/opencloud/
wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/packerVSvmbcPOC/apache-tomcat-8.5.40.tar
tar xvf apache-tomcat-8*tar  --strip-components=1
wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net:443/artifactory/tcas-generic-local/rhino/apache-tomcat.zip
unzip apache-tomcat.zip
cp -rn /opt/product/opencloud/apache-tomcat/* /opt/product/opencloud/apache-tomcat-8.5.40/
cd /opt/product/opencloud/apache-tomcat-8.5.40/
cat /dev/null >/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem

#To switch off bash's history expansion
set +H
echo "#!/bin/bash">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "# description: Tomcat Start Stop Restart">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "# processname: tomcat">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "# chkconfig: 234 20 80">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "JAVA_HOME=/opt/product/opencloud/jdk1.8.0_241">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "export JAVA_HOME">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "PATH="$'\x24'"JAVA_HOME/bin:"$'\x24'"PATH">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "export PATH">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "CATALINA_HOME=/opt/product/opencloud/apache-tomcat-8.5.40/">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo " ">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "case "$'\x24'"1 in">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "start)">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "sh "$'\x24'"CATALINA_HOME/bin/startup.sh">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo ";;">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "stop)">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "sh "$'\x24'"CATALINA_HOME/bin/shutdown.sh">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo ";;">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "restart)">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "sh "$'\x24'"CATALINA_HOME/bin/shutdown.sh">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "sh "$'\x24'"CATALINA_HOME/bin/startup.sh">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo ";;">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "esac">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
echo "exit 0">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
cd /opt/product/opencloud/apache-tomcat-8.5.40/
chmod +x bin/*.sh bin/rem
sudo ln -s /opt/product/opencloud/apache-tomcat-8.5.40/bin/rem /etc/init.d/
sudo chkconfig rem on

source ~/.bashrc
cd /opt/product/opencloud
wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/rhino-element-manager-2.6.2.1.zip
wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/rhino/sentinel-express-element-manager-2.9.0.2.em.jar
wget --user=$USERNAME --password=$PASSWORD https://diva.teliacompany.net/artifactory/tcas-generic-local/packerVSvmbcPOC/sis-em-2.6.1.0.em.jar.tar
unzip rhino-element-manager-2.6.2.1.zip -d /opt/product/opencloud/
sudo tar xvf sis-em-2.6.1.0.em.jar.tar --strip-components=1
cd /opt/product/opencloud/apache-tomcat-8.5.40/
cp ../rhino-element-manager-2.6.2.1/rem-rmi.jar bin/
mkdir -p rem_home/plugins
cp /opt/product/opencloud/sentinel-express-element-manager-2.9.0.2.em.jar /opt/product/opencloud/apache-tomcat-8.5.40/rem_home/plugins/
cp /opt/product/opencloud/sis-em-2.6.1.0.em.jar /opt/product/opencloud/apache-tomcat-8.5.40/rem_home/plugins/
cp /opt/product/opencloud/rhino-element-manager-2.6.2.1/admin/resources/rem.war /opt/product/opencloud/apache-tomcat-8.5.40/webapps/
mkdir rem-tmp
cd rem-tmp
unzip ../webapps/rem.war WEB-INF/classes/log4j2.properties
mv -f ../log4j2.properties WEB-INF/classes/log4j2.properties
zip ../webapps/rem.war WEB-INF/classes/log4j2.properties
cd ..
rm -rf rem-tmp
chmod -R 777 /opt/product/opencloud/sentinel-express-sdk

#To start a screen command in dettached mode
#screen -d -m RhinoSDK/start-rhino.sh

 SHELL
 config.vm.synced_folder "D:/vagrant_eclipse_workspace", "/opt/product/opencloud/sentinel-express-sdk"
  end

