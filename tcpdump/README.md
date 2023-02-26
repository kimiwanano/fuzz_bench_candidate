**tcpdump-4.9.2**
* Bug type:    
heap-overflow, infinite loop    
* CVE ID:        
https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=tcpdump    
* Download && Compile:    
apt-get install libpcap-dev    
wget https://www.tcpdump.org/release/tcpdump-4.9.2.tar.gz    
tar -xzf tcpdump-4.9.2.tar.gz    
cd tcpdump-4.9.2     
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all   
* Reproduce:       
afl-fuzz -m none -t 5000 -b 43 -i afl-fuzz/in/ -o afl-fuzz/out/ ./tcpdump -nr @@                

![tcpdump-24h测试界面](https://user-images.githubusercontent.com/76025773/221402638-8b152efd-6e68-4703-bb96-575c95ee53d8.png)
![tcpdump-24h测试结果](https://user-images.githubusercontent.com/76025773/221402639-979a66d8-aa94-406d-acf1-82318759cac1.png)

* Coverage                  
cd coverage-analysis                            
mkdir tcpdump-analysis                                                    
cd tcpdump-analysis                           
tar -xvf tcpdump-4.9.2.tar.gz                               
cd tcpdump-4.9.2            
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static                                                                     
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                                                                      
/afl-cov/afl-cov -d ../../tcpdump-4.9.2/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/tcpdump-analysis/tcpdump-4.9.2/ -e "./tcpdump -nr @@ -f AFL_FILE"                             
![b2b2c7ee6d42a88aa9a595ff62b3a25](https://user-images.githubusercontent.com/76025773/221412454-42db4e2c-e197-45bf-a2bb-1fb0d6acaeca.png)

* Speed       
afl-plot fuzz_out graph_fuzz_out                  
![exec_speed](https://user-images.githubusercontent.com/76025773/221402673-c037322e-5a7a-44ec-b74e-9befc5911746.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221402675-2119dfcb-6827-4968-84be-ab531f6925a5.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221402679-9f7e488f-f961-47df-863e-4da7ea4039aa.png)
