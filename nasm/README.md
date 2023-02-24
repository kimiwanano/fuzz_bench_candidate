**nasm-2.14.03rc1**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2019-6291](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6291)    
[CVE-2019-6290](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-6290)    
[CVE-2018-1000886](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-1000886)     
* Download && Compile:    
wget https://www.nasm.us/pub/nasm/snapshots/20180612/nasm-2.14rc1-20180612.tar.gz    
tar -xvf nasm-2.14rc1-20180612.tar.gz     
cd nasm-2.14rc1-20180612    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all
* Reproduce:    
afl-fuzz -m none -t 5000 -b 49 -i afl-fuzz/in/ -o afl-fuzz/out/ ./nasm -f bin @@ -o ./tmp

![nasm-24h测试界面](https://user-images.githubusercontent.com/76025773/221198385-11132fdc-f41f-44e5-9f58-467bd7493ed4.png)
![nasm-24h测试结果](https://user-images.githubusercontent.com/76025773/221198414-117969c3-bbfd-4bc8-befc-5f116a25cece.png)


* Coverage
cd coverage-analysis mkdir sfconvert-analysis
cd nasm-analysis
tar -xvf nasm-2.14rc1-20180612.tar.gz           
cd nasm-2.14rc1-20180612    
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all
/afl-cov/afl-cov -d ../../nasm-2.14rc1-20180612/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/nasm-analysis/nasm-2.14rc1-20180612/ -e "./nasm -f bin @@ -o ./tmp -f AFL_FILE"

* Speed       
afl-plot fuzz_out graph_fuzz_out        
![exec_speed](https://user-images.githubusercontent.com/76025773/221198314-449e95bd-0c9b-4387-8f67-3ad23da88086.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221198321-d57ad46f-35f5-404e-88b1-ed28c2ba622c.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221198335-ea5a950c-ed61-46ef-9ea5-1f42c69f6a3e.png)
