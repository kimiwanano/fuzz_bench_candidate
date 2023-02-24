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
afl-fuzz -m none -b 43 -t 5000 -i afl-fuzz/in/ -o afl-fuzz/out/ -x ./fuzzing/json.dict ./fuzzing/cjson @@  

![cjson-24h测试结果](https://user-images.githubusercontent.com/76025773/221084487-5448411c-8211-4790-a618-7359af043de5.png)
![cjson-24h测试界面](https://user-images.githubusercontent.com/76025773/221084498-f9fe8e4a-7b7f-4205-bd7f-4286ec18e4f4.png)

* Coverage      
cd coverage-analysis
mkdir cjson-analysis          
cd cjson-analysis       
tar -xvf cjson-1.7.7.tar.gz           
cd cJSON-1.7.7/       
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all         
cd fuzzing/           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all         
/afl-cov/afl-cov -d ../cJSON-1.7.7/fuzzing/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/cjson-analysis/cjson-1.7.7/ -e "cat AFL_FILE | ./cjson"          

![4af70950d082973c31a5ff9e73bdae4](https://user-images.githubusercontent.com/76025773/221084060-3030a9d5-ed8e-4f60-a82b-b0ff79ebafba.png)
