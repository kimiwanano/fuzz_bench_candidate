**cjson-1.7.7**
* Bug type: 
out-of-bounds access
* CVE ID:     
[CVE-2019-11834](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11834) 
[CVE-2019-11835](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-11834)
* Download && Compile:    
wget https://github.com/DaveGamble/cJSON/archive/refs/tags/v1.7.7.tar.gz    
mv v1.7.7.tar.gz cjson-1.7.7.tar.gz    
tar -xvf cjson-1.7.7.tar.gz      
cd cJSON-1.7.7/    
CC=afl-clang-fast CXX=afl-clang-fast++ make all                 
cd fuzzing/    
CC=afl-clang-fast CXX=afl-clang-fast++ make all              
* Reproduce:     
afl-fuzz -m none -b 53 -t 500 -i afl-fuzz/in/ -o afl-fuzz/out/ -x ./fuzzing/json.dict ./fuzzing/cjson @@                           
