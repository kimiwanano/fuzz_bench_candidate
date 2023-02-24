**jasper-2.0.14**
* Bug type: uncontrolled-memory-allocation, memory leak    
* CVE ID:
[CVE-2016-8886](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-7581)    
* Download && Compile:    
wget http://www.ece.uvic.ca/~frodo/jasper/software/jasper-2.0.14.tar.gz    
tar -xvf jasper-2.0.14.tar.gz     
cd jasper-2.0.14    
mkdir BUILD    
cd BUILD/    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake -G "Unix Makefiles" ..       
make all           
* Reproduce:      
afl-fuzz -m none -t 5000 -b 46 -i afl-fuzz/in/ -o afl-fuzz/out/ ./BUILD/src/appl/jasper --input @@ --output test.bmp --output-format bmp

![jasper-24h测试界面](https://user-images.githubusercontent.com/76025773/221199253-a699ad54-dea0-47b0-b4a5-9a0cb224304c.png)
![jasper-24h测试结果](https://user-images.githubusercontent.com/76025773/221199257-e273c72b-24d6-4283-b5d4-99e74ef16a06.png)

* Coverage          
cd coverage-analysis
mkdir jasper-analysis
cd jasper-analysis
tar -xvf jasper-2.0.14.tar.gz     
cd jasper-2.0.14    
// 修改CMakeFile                                            
![e2ab42b4f4f5ba983720766a373b6b3](https://user-images.githubusercontent.com/76025773/221227795-963f75e5-f941-463c-940f-b6d5d519f13c.png)
mkdir BUILD    
cd BUILD/    
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" cmake  -G "Unix Makefiles" ..                                                                    
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                                         
/afl-cov/afl-cov -d ../../jasper-2.0.14/afl-fuzz/out/ --coverage-cmd "./src/appl/jasper --input @@ --output test.bmp --output-format bmp -f AFL_FILE" -c /fuzz_bench/coverage-analysis/jasper-analysis/jasper-2.0.14/ --enable-branch-coverage                                            
![b3d3651dfbe216a42abcb45fd43d3a4](https://user-images.githubusercontent.com/76025773/221227440-ac5f99ce-f0eb-4468-b9b2-e36625cb4f36.png)

* Speed         
afl-plot fuzz_out graph_fuzz_out              
![exec_speed](https://user-images.githubusercontent.com/76025773/221224654-c141aecd-b348-4bd8-8282-7bd2294644fb.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221224664-fe809146-dc64-4359-8531-bcfdd9397b84.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221224675-842e174c-9320-4128-8335-2f7bd6c43f8d.png)
