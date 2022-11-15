**nasm-2.14.03rc1**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2019-6291](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6291)    
[CVE-2019-6290](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6290)    
[CVE-2018-1000886](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-1000886)     
* Download && Compile:    
wget https://www.nasm.us/pub/nasm/snapshots/20180612/nasm-2.14rc1-20180612.tar.gz    
tar -xvf nasm-2.14rc1-20180612.tar.gz     
cd nasm-2.14rc1-20180612    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-shared    
make all
* Reproduce:    
afl-fuzz -m none -b 44 -i afl-fuzz/in/ -o afl-fuzz/out/ ./nasm -f bin @@ -o ./tmp

![image](https://user-images.githubusercontent.com/76025773/201922459-8e13c1bf-4ead-4b06-bc15-43f4066eff11.png)
