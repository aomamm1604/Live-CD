
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

#●ไปที่หน้า Console ของ UCK
   - ทำการติดตั้ง JAVA 

      #apt-get update
      #add-apt-repository ppa:webupd8team/java
      #apt-get update
      #apt-get install oracle-java8-installer
      #update-alternatives --config java
      #apt-get install oracle-java8-set-default
      #update-alternatives --config java
   
   - Check JAVA
      # java -version ; javac -version

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

    nano /usr/share/applications/eclipse.desktop
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

   
   
