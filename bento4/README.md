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
afl-fuzz -m none -t 5000 -b 42 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/mp42hls @@    

![mp42hls-24h测试界面](https://user-images.githubusercontent.com/76025773/221110896-0829ceea-9c56-463d-996e-3542960f0622.png)
![mp42hls-24h测试结果](https://user-images.githubusercontent.com/76025773/221110907-c9ee7ef1-3480-4943-a77c-fde60f9e452a.png)

* Coverage      
cd coverage-analysis
mkdir bento4-analysis          
cd bento4-analysis       
git clone https://github.com/axiomatic-systems/Bento4           
git checkout 590312125c833bc496faf815c583cfd053509d2c             
cd Bento4
// 修改CMakeFile        
![ba546438493fb91e9a3fd3e45a80eee](https://user-images.githubusercontent.com/76025773/221110604-e7a22ea1-e4a3-4790-a7f8-1d8c203c5a30.png)               
mkdir build         
cd build        
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage"  cmake -DCMAKE_BUILD_TYPE=Release ..                      
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all              
/afl-cov/afl-cov -d ../bento4/afl-fuzz/out/  --coverage-cmd "./mp42hls @@ -f AFL_FILE" -c /fuzz_bench/coverage-analysis/bento4-analysis/Bento4/ --enable-branch-coverage              
![0f97e3a64f00d80bff7e58d7eeb0d42](https://user-images.githubusercontent.com/76025773/221111126-8d769089-1096-4ec8-bb79-e75a216f4a80.png)

*Speed            
afl-plot fuzz_out graph_fuzz_out               
![exec_speed](https://user-images.githubusercontent.com/76025773/221187635-f9717d04-43e6-422e-bc27-789fee238c33.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221187647-9d536ef2-b6fa-49bc-9345-1e5deec60ec2.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221187660-363f7a19-92aa-412e-8f32-0a64961ed516.png)
