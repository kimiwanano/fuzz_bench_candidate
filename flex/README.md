**Flex 2.6.4**   
* Bug type: stack-overflow   
* CVE ID:    
[CVE-2019-6293](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6293)   
* Download && Compile:   
apt-get install -y m4    
wget https://github.com/westes/flex/files/981163/flex-2.6.4.tar.gz    
tar -xvf flex-2.6.4.tar.gz    
cd flex-2.6.4    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static  
make all
* Reproduce:   
afl-fuzz -m none -t 5000 -b 44 -i afl-fuzz/in/ -o afl-fuzz/out/ ./src/flex @@       

![flex-24h测试界面](https://user-images.githubusercontent.com/76025773/221085998-6d7bcf88-c9e1-48b3-9713-c8f1559e73cb.png)
![flex-24h测试结果](https://user-images.githubusercontent.com/76025773/221085992-576c8456-713b-4cae-8d76-b220c39b3097.png)

* Coverage      
cd coverage-analysis              
mkdir flex-analysis          
cd flex-analysis       
tar -xvf flex-2.6.4.tar.gz              
cd flex-2.6.4            
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static                    
/afl-cov/afl-cov -d ../flex-2.6.4/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/flex-analysis    /flex-2.6.4/ -e "cat AFL_FILE | ./src/flex"   

![33db084dd8138ae1203cde7a7672039](https://user-images.githubusercontent.com/76025773/221188359-a8996294-3a8f-4266-ba19-e814ad475ec6.png)



* Speed       
afl-plot fuzz_out graph_fuzz_out          

![exec_speed](https://user-images.githubusercontent.com/76025773/221188190-84bbd96f-f33c-4a2e-b00f-9baa58016cf3.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221188197-39a22d85-dbbd-4b94-bb69-8636f15935b3.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221188207-9256c19f-0c4a-4f62-a245-66b5efee8634.png)
