The vagrant file is used to configure virtual machine.

Following are the specifications :

#######################

Installation Details :

	JAVA
	ANT
	RhinoSDK
	Sentinel
	Apache Tomcat
######################

=>To allow CMD to prompt username and password in command line we use the following 


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


=>To run screen command in dettach mode we can use the following command

	screen -d -m RhinoSDK/start-rhino.sh
	
	 * With the use of above command we can run a script inside a screen without entering it

=>To replace a line we can use the following command
	
	sed -i '/-Xmx/s/.*/-Xmx4096m/' /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/jvm_args
	
=>To replace a line after a particular line we can use the following command

	sed -i '/# select the server VM/{n;s/.*/-Dtransaction.default_timeout=300000/}' /opt/product/opencloud/sentinel-express-sdk/rhino-sdk/RhinoSDK/config/jvm_args
	
=>To bypass symbol like $ we can use the following command

	echo "PATH="$'\x24'"JAVA_HOME/bin:"$'\x24'"PATH">>/opt/product/opencloud/apache-tomcat-8.5.40/bin/rem
