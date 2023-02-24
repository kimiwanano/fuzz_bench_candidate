**libksba-1.3.5**		
* Bug type:    			
  
* CVE ID:     			
   
* Download && Compile:   
apt-get install libgpg-error-dev   
或
【wget ftp://ftp.gnupg.org/gcrypt/libgpg-error/libgpg-error-1.27.tar.gz   
tar zxvf libgpg-error-1.27.tar.gz   
cd libgpg-error-1.27   
./configure --prefix=/usr --libdir=/usr/lib64   
make   
make install】   
tar -xjf libksba-1.3.5.tar.bz2   
cd libksba-1.3.5/   
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static   
make all   
* Reproduce:   
afl-fuzz -m none -t 5000 -b 47 -i afl-fuzz/in/ -o afl-fuzz/out/ ./libksba-1.3.5/tests/cert-basic @@   


![cert-basic-24h测试界面](https://user-images.githubusercontent.com/76025773/221219569-fb63e1a5-f24d-4559-9308-cc4dca1751e4.png)
![cert-basic-24h测试结果](https://user-images.githubusercontent.com/76025773/221219577-966045f4-e682-4ed6-9413-b8b74c4e3216.png)

* Coverage      
cd coverage-analysis          
mkdir cert-basic-analysis           
cd cert-basic-analysis            
tar -xjf libksba-1.3.5.tar.bz2            
cd libksba-1.3.5/                   
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static             
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all    
/afl-cov/afl-cov -d ../../libksba-1.3.5/fuzz_out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/libksba-1.3.5/ -e "./tests/cert-basic @@ -f AFL_FILE"           
![cert-basic-24h覆盖情况](https://user-images.githubusercontent.com/76025773/221220180-7d93484c-eca7-4947-ab79-968601989e21.png)

* Speed         
afl-plot fuzz_out graph_fuzz_out          
![exec_speed](https://user-images.githubusercontent.com/76025773/221220272-cd7b7b64-58bd-44b8-bfb7-7d23b6cb7d5d.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221220280-35c30dc2-f2f5-45b6-bdef-109c290f0e73.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221220287-8519b13a-505e-40ab-bb6e-8c91d89ba21e.png)

