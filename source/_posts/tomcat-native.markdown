

#Notas sobre la instalacion de apr

tar -xvf tomcat-native.tar.gz 
cd tomcat-native-1.1.20-src/jni/native/
yum install apr-devel
./configure --prefix=/usr/local/stow/tomcat-native-1.1 --with-apr=/usr/bin/apr-1-config 
make
make install
stow tomcat-native-1.1


## Referencias

http://cybergav.in/tag/tomcat-native-library-on-rhel-6/
http://www.jroller.com/agileanswers/entry/configuring_apr_for_tomcat
