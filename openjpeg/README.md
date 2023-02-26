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
afl-fuzz -m none -t 5000 -b 41 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/bin/opj_decompress -i @@ -o ./tmp.png    


![opj_decompress-24h测试界面](https://user-images.githubusercontent.com/76025773/221413541-279c4924-6795-4b93-a86f-4a9fded34fd6.png)
![opj_decompress-24h测试结果](https://user-images.githubusercontent.com/76025773/221413546-06747e33-ff2a-4796-b62d-d681c8c6cfaf.png)    

* Coverage                              
cd coverage-analysis                              
tar -xvf openjpeg-2.3.0.tar.gz                                    
cd openjpeg-2.3.0                         
// 修改CMakeFile                          

mkdir build                       
cd build/                           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" cmake .. -DCMAKE_BUILD_TYPE=Release                    
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                     

* Speed     
afl-plot fuzz_out graph_fuzz_out                      
![exec_speed](https://user-images.githubusercontent.com/76025773/221413738-ea3f5fe5-427c-48d6-8c63-1ce7edc1ecdd.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221413739-7b054b2d-13b6-40bd-8ba9-6ad2ca22722e.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221413743-7b1ef233-3ca3-463b-9a69-8bb36c5db42e.png)
