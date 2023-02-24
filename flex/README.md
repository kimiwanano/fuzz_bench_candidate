**Flex 2.6.4**   
* Bug type: stack-overflow   
* CVE ID:    
[CVE-2019-6293](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6293)   
* Download && Compile:   
apt-get install -y m4    
wget https://github.com/westes/flex/files/981163/flex-2.6.4.tar.gz    
tar -xvf flex-2.6.4.tar.gz    
cd flex-2.6.4    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static  
make all
* Reproduce:   
afl-fuzz -m none -t 5000 -b 44 -i afl-fuzz/in/ -o afl-fuzz/out/ ./src/flex @@       

![flex-24h测试界面](https://user-images.githubusercontent.com/76025773/221085998-6d7bcf88-c9e1-48b3-9713-c8f1559e73cb.png)
![flex-24h测试结果](https://user-images.githubusercontent.com/76025773/221085992-576c8456-713b-4cae-8d76-b220c39b3097.png)

* Coverage      
