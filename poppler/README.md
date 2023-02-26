**poppler-0.75.0**
* Bug type: 
Buffer overflow
* CVE ID:     
[CVE-2020-27778](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27778)    
* Download && Compile:    
wget https://poppler.freedesktop.org/poppler-0.75.0.tar.xz    
tar -xvf poppler-0.75.0.tar.xz    
cd poppler-0.75.0    
mkdir build    
cd build/    
apt-get install -y pkg-config    
apt-get install -y libfontconfig1-dev    
apt-get install libtiff-dev    
apt-get install libjpeg-dev    
apt-get install libopenjp2-7-dev    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake ..     
make all
* Reproduce:    
afl-fuzz -m none -t 5000 -b 45 -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/utils/pdftohtml @@    

![pdftohtml-24h测试界面](https://user-images.githubusercontent.com/76025773/221403381-fd4070b4-3c45-4145-b2de-f2d95677b2fd.png)
![pdftohtml-24h测试结果](https://user-images.githubusercontent.com/76025773/221403385-794aed0e-cb74-4fe6-b835-6a9bd2d8a2f9.png)

* Coverage                            
cd coverage-analysis                              
tar -xvf poppler-0.75.0.tar.xz                                
cd poppler-0.75.0                                 
// 修改CMakeFile                          
![e092d2387e7dda2b84146ebc13946a2](https://user-images.githubusercontent.com/76025773/221413064-8d3f7acd-a978-4833-8720-d6574c5dee27.png)
mkdir build                                   
cd build/                           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" cmake ..                            
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                                     
/afl-cov/afl-cov -d ../../../poppler-0.75.0/build/afl-fuzz/out/ --coverage-cmd "./utils/pdftohtml @@ -f AFL_FILE" -c /fuzz_bench/coverage-analysis/poppler-0.75.0/ --enable-branch-coverage

* Speed             
afl-plot fuzz_out graph_fuzz_out                      
![exec_speed](https://user-images.githubusercontent.com/76025773/221403472-b9e2d152-f742-48aa-9bd2-59b3e631dfc0.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221403473-b4482041-a096-4b42-a3a2-bff5e808ec63.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221403476-0e1605bb-60ec-4eb2-b90d-a0723c82b6ab.png)
