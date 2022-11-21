**cxxfilt-2.31**
* Bug type:     
stack-overflow       
* CVE ID:      
[CVE-2018-9138](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-9138)           
[CVE-2018-9996](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-9996)         
[CVE-2018-17985](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-17985)         
[CVE-2018-18484](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18484)       
[CVE-2018-18700](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18700)          
* Download:               
wget https://ftp.gnu.org/gnu/binutils/binutils-2.31.1.tar.gz           
tar -xvf binutils-2.31.1.tar.gz            
cd binutils-2.31.1              
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static            
make all       
* Reproduce:      
afl-fuzz -m none -t 500 -b 54 -i afl-fuzz-cxxfilt/in/ -o afl-fuzz-cxxfilt/out/ ./binutils/cxxfilt -n    

![image](https://user-images.githubusercontent.com/76025773/203093252-0eb74754-e586-49cc-8f52-e43a8e8bec83.png)
