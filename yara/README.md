**yara-3.5.0**
* Bug type: stack-overflow
* CVE ID:    
[CVE-2017-9438](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-9438)    
[CVE-2017-9304](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-9304)    
* Download && Compile    
wget https://github.com/VirusTotal/yara/archive/refs/tags/v3.5.0.tar.gz    
mv v3.5.0.tar.gz yara-3.5.0.tar.gz    
tar -xvf yara-3.5.0.tar.gz     
cd yara-3.5.0    
apt-get install autoconf automake libtool       
./bootstrap.sh     
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all    
* Reproduce:    
afl-fuzz -m none -t 5000 -b 40 -i afl-fuzz/in/ -o afl-fuzz/out/ ./yara @@ strings    

![yara-24h测试界面](https://user-images.githubusercontent.com/76025773/221400746-3e9af6e5-0311-49b9-819d-c28cc253d42c.png)
![yara-24h测试结果](https://user-images.githubusercontent.com/76025773/221400749-ec1c073b-c615-4899-9ba5-287177639ef4.png)

* Coverage              
cd coverage-analysis
mkdir yara-analysis
cd yara-analysis
tar -xvf yara-3.5.0.tar.gz                          
cd yara-3.5.0            
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./bootstrap.sh                              
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static                                             
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                                                           
/afl-cov/afl-cov -d ../../yara-3.5.0/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/yara-analysis/yara-3.5.0/ -e "./yara @@ strings  -f AFL_FILE"                      

![f32331d6fcf5bef383728679b6bab3a](https://user-images.githubusercontent.com/76025773/221402088-24eacb20-75d3-45a9-b7fa-2948d9a326f6.png)

* Speed     
afl-plot fuzz_out graph_fuzz_out        
![exec_speed](https://user-images.githubusercontent.com/76025773/221400735-e6414017-8dca-4867-abcd-bfa16734dc19.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221400737-b31d2c3b-a007-462b-9534-069038db157b.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221400740-9f960cdb-d2e2-4c39-8b58-9969605f1344.png)
