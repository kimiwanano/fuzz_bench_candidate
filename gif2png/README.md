**gif2png-2.5.13**
* Bug type:    
memory leak    
* CVE ID:     
[CVE-2019-17371](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17371)    
* Download && Compile:    
wget http://www.catb.org/~esr/gif2png/gif2png-2.5.13.tar.gz    
cd gif2png-2.5.13    
apt-get install -y libpng-dev    
CC=afl-clang-fast CXX=afl-clang-fast++ make all
* Reproduce:    
afl-fuzz -m none -t 5000 -b 45 -i afl-fuzz/in/ -o afl-fuzz/out/ ./gif2png @@    

![gif2png-24h测试界面](https://user-images.githubusercontent.com/76025773/221186971-d34e999f-9810-4742-a183-da7c387b887f.png)
![gif2png-24h测试结果](https://user-images.githubusercontent.com/76025773/221186981-b4cb238b-8bc5-43b3-8605-330e64e828ee.png)

* Coverage
