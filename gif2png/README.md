**gif2png-2.5.13**
* Bug type:    
memory leak    
* CVE ID:     
[CVE-2019-17371](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17371)    
* Download && Compile:    
wget http://www.catb.org/~esr/gif2png/gif2png-2.5.13.tar.gz    
cd gif2png-2.5.13    
apt-get install -y libpng-dev    
CC=afl-clang-fast CXX=afl-clang-fast++ make all
* Reproduce:    
afl-fuzz -m none -t 5000 -b 45 -i afl-fuzz/in/ -o afl-fuzz/out/ ./gif2png @@    

![gif2png-24h测试界面](https://user-images.githubusercontent.com/76025773/221186971-d34e999f-9810-4742-a183-da7c387b887f.png)
![gif2png-24h测试结果](https://user-images.githubusercontent.com/76025773/221186981-b4cb238b-8bc5-43b3-8605-330e64e828ee.png)

* Coverage
cd coverage-analysis        
mkdir gif2png-analysis
cd gif2png-analysis
tar -xvf gif2png-2.5.13.tar.gz    
cd gif2png     
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all           
/afl-cov/afl-cov -d ../../gif2png-2.5.13/fuzz_out/ --coverage-cmd "./gif2png @@ -f AFL_FILE" -c /fuzz_bench/coverage-analysis/gif2png-2.5.13/ --enable-branch-coverage

![608c808eb43851159ec8863ae2b6495](https://user-images.githubusercontent.com/76025773/221189195-2214e716-6da9-49d8-a39d-fb7ec48ebcc9.png)       

* Speed       
afl-plot fuzz_out graph_fuzz_out          

![exec_speed](https://user-images.githubusercontent.com/76025773/221189390-ebad8530-51c6-4ade-bd5d-57fa6e861878.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221189401-36e518c0-452d-4058-a3db-1151011f8f9a.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221189407-d0d73ed5-3538-4bb6-865a-026d15d66b34.png)
