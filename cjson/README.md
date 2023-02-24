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

![cjson-24h测试界面](https://user-images.githubusercontent.com/76025773/221084498-f9fe8e4a-7b7f-4205-bd7f-4286ec18e4f4.png)
![cjson-24h测试结果](https://user-images.githubusercontent.com/76025773/221084487-5448411c-8211-4790-a618-7359af043de5.png)

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

![66b2324142d648787d339987fc52ca9](https://user-images.githubusercontent.com/76025773/221088650-fa73e840-aa00-4746-95b8-dd63da51fffb.png)

* Speed           
afl-plot fuzz_out graph_fuzz_out              

![exec_speed](https://user-images.githubusercontent.com/76025773/221187967-7e90c2d2-d338-4b47-b223-2d93881f4e46.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221187978-47950ca2-9a69-43e3-b605-b12c0a6798df.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221187989-53091cb9-d6cc-4627-b304-a12929691c0c.png)


