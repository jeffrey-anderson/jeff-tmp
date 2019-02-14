```
# Switch to root
sudo -i

# After entering your password copy / paste the commands below one line at a time or in blocks:

groupadd developers

mkdir software
cd software

# Java

curl -L -b "oraclelicense=a" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz -O
tar xvzf jdk-8u201-linux-x64.tar.gz

mv jdk1.8.0_201 /opt
cd /opt
ln -s jdk1.8.0_201 java8
chown -R root.root jdk1.8.0_201

cat <<EOF > /etc/profile.d/java.sh
JAVA_HOME=/opt/java8
PATH=$JAVA_HOME/bin:\$PATH
export JAVA_HOME PATH
EOF
cd ~/software


# Docker

amazon-linux-extras install docker -y
systemctl enable docker
systemctl start docker

# IntelliJ

wget https://download-cf.jetbrains.com/idea/ideaIC-2018.3.3.tar.gz
tar xvzf ideaIC-2018.3.3.tar.gz
mv idea-IC-183.5153.38 /opt/idea
chmod -R g+w /opt/idea
chown -R root.developers /opt/idea

cat <<EOF > /usr/share/applications/jetbrains-idea-ce.desktop
[Desktop Entry]
Version=1.0
Type=Application
Name=IntelliJ IDEA Community Edition
Icon=/opt/idea/bin/idea.svg
Exec="/opt/idea/bin/idea.sh" %f
Comment=Capable and Ergonomic IDE for JVM
Categories=IDE;Development
Terminal=false
StartupWMClass=jetbrains-idea-ce
EOF


# DBeaver

wget https://dbeaver.io/files/dbeaver-ce-latest-linux.gtk.x86_64.tar.gz
tar xvzf dbeaver-ce-latest-linux.gtk.x86_64.tar.gz
mv dbeaver /opt/dbeaver
chmod -R g+w /opt/dbeaver
chown -R root.developers /opt/dbeaver

cat <<EOF > /usr/share/applications/dbeaver.desktop
[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Name=DBeaver Community
GenericName=UniversaL Database Manager
Comment=Universal Database Manager and SQL Client.
Path=/opt/dbeaver/
Exec=/opt/dbeaver/dbeaver
Icon=/opt/dbeaver/dbeaver.png
Categories=IDE;Development
WM_CLASS=DBeaver
StartupWMClass=DBeaver
StartupNotify=true
Keywords=Database;SQL;IDE;JDBC;ODBC;MySQL;PostgreSQL
MimeType=application/sql
EOF

# Postman

wget https://dl.pstmn.io/download/latest/linux64
tar xvzf linux64

mv Postman /opt
chmod -R g+w /opt/Postman
chown -R root.developers /opt/Postman

cat <<EOF > /usr/share/applications/postman-ade.desktop
[Desktop Entry]
Version=1.0
Type=Application
Name=Postman ADE
Icon=/opt/Postman/app/resources/app/assets/icon.png
Exec="/opt/Postman/app/Postman" %f
Comment=Postman Simplifies API Development
Categories=IDE;Development
Terminal=false
EOF

# Maven
wget https://www.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
tar xvzf apache-maven-3.6.0-bin.tar.gz

mv apache-maven-3.6.0 /opt
cd /opt
ln -s apache-maven-3.6.0 maven

cat <<EOF > /etc/profile.d/maven.sh
export PATH=/opt/maven/bin:\$PATH
EOF

cd ~/software

# Gradle

wget https://services.gradle.org/distributions/gradle-5.1.1-bin.zip
unzip gradle-5.1.1-bin.zip
mv gradle-5.1.1 /opt
cd /opt
ln -s gradle-5.1.1 gradle

cat <<EOF > /etc/profile.d/gradle.sh
export PATH=/opt/gradle/bin:\$PATH
EOF

cd ~/software

# Atom Editor

wget https://atom-installer.github.com/v1.34.0/atom.x86_64.rpm
yum install atom.x86_64.rpm -y


### ================
###
### AFTER THE IMAGE IS DEPLOYED:
###
### Students will have to run this the first time they connect:
sudo usermod -aG docker,developers $USER
###
### Then logout and back in or reboot the system
### System -> Logout --OR--
sudo init 6
```
