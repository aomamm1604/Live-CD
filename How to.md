
#How to do Ubuntu Live CD

#● ทำการติดตั้ง Ubuntu 14.04 LTS บนเครื่อง HOST
   โดย version ที่เราใช้ลงต้องเป็น version เดียวกับที่เราจะทำตัว Live CD (ตัวอย่างเช่น จะทำ Ubuntu live cd version 14.04 LTS เครื่อง Host ก็ต้องลงเป็น Ubuntu 14.04 LTS ด้วยเช่นกัน)
   
#● Install UCK (Ubuntu Customization Kit)
   โดยการ ติดตั้งสามารถ ติดตั้งผ่าน Ubuntu’s Software Center โดยการพิมพ์ uck or Ubuntu Customization Kit ไปยังช่องค้นหา
   หรือจะทำการติดตั้งผ่าน terminal โดยใช้
   
      #apt-get install uck
  
#●ทำการ start UCK 

#เลือก Run Console Application
เพื่อทำการcustomize ตัว ISO File หลังจากที่เราเข้าหน้า consloe มาแล้ว เราจะอยู่ในสิทธิ์ root โดย folder root ในที่นี้จะถูก
ลบทิ้งหลังจากเราทำการ build iso

โดยเราสามารถเข้าไปดู directory ต่างๆได้ที่

      #cd home/ชื่อuser/tmp/remaster-root/

หากเราต้องการเพิ่มไฟล์ หรือ อยากจะสร้าง folder ที่ใส่ package สำหรับให้ user ต่างๆได้ใช้ เราสามารถนำไฟล์เหล่านั้นไปไว้ที่

      #cd /etc/skel


ไฟล์ต่างๆ จะถูกสร้างให้แต่ล่ะ user ที่ถูก generate ขึ้นมาใหม่โดยอัติโนมัติ

ในตัวอย่างนี้ เราจะทำการติดตั้งโปรแกรม codeblocks, eclipse และ โปรแกรม pc2 สำหรับ user

#●ไปที่หน้า Console ของ UCK ทำการติดตั้ง JAVA

         #apt-get update
         #add-apt-repository ppa:webupd8team/java
         #apt-get update
         #apt-get install -y oracle-java8-installer
         #update-alternatives --config java
         #apt-get install oracle-java8-set-default
         #update-alternatives --config java
         #java -version ; javac -version
   
#●ไปที่หน้า terminal ของ เครื่อง 
   Host ทำการ copy file ที่เราต้องการไปไว้ที่ /etc/skel ซึ่งไฟล์เหล่านี้จะปรากฎอยู่ที่ home directory ของแต่ล่ะ user  
   
      #cp yourfile /home/muict/tmp/remaster-root/etc/skel
      #cp eclipse-cpp-mars-1-linux-gtk-x86_64.tar.gz /home/muict/tmp/remaster-root/opt

หลังจาก copy file ต่างๆที่เราต้องการแล้วให้ทำการกลับมาที่ uck console
   
#● Go back to UCK Consloe

   ลองทำการตรวจสอบไฟล์ต่างๆที่เรา copy มาด้วยการ ls ดูที่ directory  เหล่านั้น
   
      #ls /opt
      #ls /etc/skel/

#● Install gcc g++ vim gedit

    #apt-get install -y vim gedit build-essential
    #gcc --version ; g++ --version
   
#● Install eclipse

    #cd /opt
    #ls
    #tar -xvf eclipse-cpp-mars-1-linux-gtk-x86_64.tar.gz 
    #rm -rf eclipse-cpp-mars-1-linux-gtk-x86_64.tar.gz 

   create icon on desktop

    #nano /usr/share/applications/eclipse.desktop
       [Desktop Entry]
         Name=Eclipse
         Type=Application
         Exec=/opt/eclipse/eclipse
         Terminal=false
         Icon=/opt/eclipse/icon.xpm
         Comment=Integrated Development Environment
         NoDisplay=false
         Categories=Development;IDE;
         Name[en]=eclipse

   
#● ไปที่ /ect/skel ทำการ create Desktop directory

      #cd /etc/skel
      #mkdir Desktop

#● ติดตั้ง desktop icon

      #chmod +x /usr/share/applications/eclipse.desktop
      #desktop-file-install /usr/share/applications/eclipse.desktop
      #ln -s /opt/eclipse/eclipse /usr/local/bin/
      #cp /usr/share/applications/eclipse.desktop /etc/skel/Desktop/
      #cd Desktop
      #chmod 755 eclipse.desktop 
      #eclipse

#● ลบ folder example หน้า Desktop ทิ้ง

      #cd /etc/skel
      #rm -rf examples.desktop 
   
#● สร้าง shell script สำหรับ run pc2team ใน /etc/skel

      #vi test.sh
         #! /bin/sh
         cd /home/ubuntu/pc2/bin/
         ./pc2team
  
      #chmod +x test.sh
   
   
#● สร้าง desktop icon สำหรับ folder pc2

      #nano /usr/share/applications/pc2team.desktop
         [Desktop Entry]
         Name=PC2TEAM
         Type=Application
         Exec=sh /home/ubuntu/test.sh
         Terminal=false
         Icon=/usr/share/icons/HighContrast/scalable/categories/applications-system.svg
         Comment=ACM
         NoDisplay=false
         Categories=Application;
         Name[en]=pc2team

      #chmod +x /usr/share/applications/pc2team.desktop
      #desktop-file-install /usr/share/applications/pc2team.desktop
      #cp /usr/share/applications/pc2team.desktop /etc/skel/Desktop/
      #cd /etc/skel/Desktop
      #chmod 755 pc2team.desktop
      


#● ทำการ ลบ package ที่เราไม่ต้องการทิ้ง

      #apt-get remove Ubiquity
   
      #gsettings set com.canonical.Unity.Lenses disabled-scopes "['more_suggestions-amazon.scope',    'more_suggestions-u1ms.scope', 'more_suggestions-populartracks.scope', 'music-musicstore.scope', 'more_suggestions-ebay.scope', 'more_suggestions-ubuntushop.scope', 'more_suggestions-skimlinks.scope']"
      #gsettings set com.canonical.Unity.Lenses remote-content-search none
      #rm -rf /usr/share/applications/ubuntu-amazon-default.desktop
      #apt-get -y remove --purge libreoffice*
      #apt-get clean
      #apt-get autoremove
      #apt-get remove fonts-opensymbol libreoffice libreoffice-\* openoffice.org-dtd-officedocument1.0 python\*-uno uno-libs3-\* ure ure-dbg
      #aptitude search '~i' | grep libreoffice
      #apt-get remove libreoffice-core
      #apt-get purge thunderbird*
      #apt-get purge firefox
      #rm -rf ~/.mozilla
      #rm -rf /usr/lib/firefox
      #rm -rf /usr/lib/firefox-addons/
      #apt-get remove --purge unity-lens-shopping

#●Add univers repository

      #sudo -e /etc/apt/sources.list
      #add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe"
      #add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe restricted multiverse"
      #add-apt-repository "deb http://archive.canonical.com/ubuntu $(lsb_release -sc) partner"

#● Install Codeblocks

      #apt-get update
      #add-apt-repository ppa:pasgui/ppa
      #apt-get update
      #apt-get install codeblocks

#● commnet พวก repo ที่เราเพิ่ง add เพิ่มไป

      #nano /etc/apt/sources.list
      #apt-get update

#● เสร็จ

      #exit

#● ทำการเลือก continue building รอจนเสร็จ

ไฟล์ iso จะอยู่ที่ /tmp/remaster-new/
