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
* Reproduce:   
afl-fuzz -m none -b 40 -i afl-fuzz/in/ -o afl-fuzz/out/ ./src/flex @@    

![image](https://user-images.githubusercontent.com/76025773/201915136-120a433a-3d40-4fea-9ccc-ebe7d16560fa.png)
