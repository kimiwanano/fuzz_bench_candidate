**bento4-1.5.1**
* Bug type: uncontrolled-memory-allocation, memory leak    
* CVE ID:    
[CVE-2018-20186](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20186)     
[CVE-2018-20659](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-20659)    
[CVE-2019-7698](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-7698)    
[CVE-2019-6966](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6966)    
* Download && Compile:    
cd bento4-1.5.1/    
mkdir build    
cd build/    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake -DCMAKE_BUILD_TYPE=Release ..    
make all
* Reproduce:    
afl-fuzz -m none -b 43 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/mp42hls @@
