**yaml-cpp-0.6.2**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2019-6292](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6292)     
[CVE-2019-6285](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6285)     
[CVE-2018-20573](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20573)     
[CVE-2018-20574](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20574)     
* Download && Compile:    
git clone https://github.com/jbeder/yaml-cpp    
cd yaml-cpp/    
git checkout 562aefc114938e388457e6a531ed7b54d9dc1b62    
mkdir build      
cd build/    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake ..    
make     
make all
* Reproduce:     
afl-fuzz -m none -b 48 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/util/parse @@   
