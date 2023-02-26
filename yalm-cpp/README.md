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
make all
* Reproduce:     
afl-fuzz -m none -t 5000 -b 42 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/util/parse @@     

![parse-24h测试界面](https://user-images.githubusercontent.com/76025773/221402973-13a30e9c-00fc-496a-99f5-635f1d5e3785.png)
![parse-24h测试结果](https://user-images.githubusercontent.com/76025773/221402975-f4714a93-b6b7-43ae-8f6d-e720c4090e30.png)

* Coverage          
cd coverage-analysis
git clone https://github.com/jbeder/yaml-cpp                        
cd yaml-cpp/    
git checkout 562aefc114938e388457e6a531ed7b54d9dc1b62                                   
// 修改CMakeFile                                  
![3cb127d65a339898ce6b5e492f52b17](https://user-images.githubusercontent.com/76025773/221403008-f5313219-9f84-4989-a06e-bcbbe37291c7.png)                           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" cmake ..
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all
/afl-cov/afl-cov -d ../../../yaml-cpp/afl-fuzz/out/ --coverage-cmd "./util/parse @@ -f AFL_FILE" -c /fuzz_bench/coverage-analysis/yaml-cpp/ --enable-branch-coverage         
![b779e81e094ee9cac34a1e84d03cdbd](https://user-images.githubusercontent.com/76025773/221412564-99473853-2234-4d06-a1b0-392940a20bae.png)


* Speed           
afl-plot fuzz_out graph_fuzz_out              
![exec_speed](https://user-images.githubusercontent.com/76025773/221402993-715a4802-a626-40dc-9d56-3f74706347a6.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221402994-c389f9ce-06e2-42e6-8f8e-fa9fa3a48b0e.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221402995-9a90bcfb-8f4d-4822-a2a6-280ae770be00.png)
