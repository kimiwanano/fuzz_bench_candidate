**openjpeg-2.3.0**
* Bug type: uncontrolled-memory-allocation    
* CVE ID:    
[CVE-2019-6988](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6988)      
[CVE-2017-12982](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-12982)         
* Download && Compile:        
wget https://github.com/uclouvain/openjpeg/archive/refs/tags/v2.3.0.tar.gz    
mv v2.3.0.tar.gz openjpeg-2.3.0.tar.gz      
tar -xvf openjpeg-2.3.0.tar.gz  
cd openjpeg-2.3.0    
mkdir build    
cd build/    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake .. -DCMAKE_BUILD_TYPE=Release    
make all    
* Reproduce:    
afl-fuzz -m none -b 41 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/bin/opj_decompress -i @@ -o ./tmp.png    

![image](https://user-images.githubusercontent.com/76025773/201916946-5d7d9c84-bd36-4e41-9a65-1ec4c633c22e.png)
