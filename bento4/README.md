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
afl-fuzz -m none -t 500 -b 52 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/mp42hls @@    

<img width="450" alt="ab014d0d72b1733893f4c1bab7356d0" src="https://user-images.githubusercontent.com/76025773/201921777-0d13232c-c4cb-4579-a4cc-71be7f0fc095.png">
