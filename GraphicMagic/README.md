**GraphicsMagick-1.3.26**
* Bug type:    
use-after-free    
* CVE ID:     
[CVE-2017-11403](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-11403)    
* Download && Compile:   
wget https://sourceforge.net/projects/graphicsmagick/files/graphicsmagick-history/1.3/GraphicsMagick-1.3.26.tar.gz     
tar -xvf GraphicsMagick-1.3.26.tar.gz    
cd GraphicsMagick-1.3.26    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all
* Reproduce:     
afl-fuzz -m none -t 5000 -b 50 -i afl-fuzz/in/ -o afl-fuzz/out/ ./utilities/gm convert @@ /dev/null               

![gm-24h测试界面](https://user-images.githubusercontent.com/76025773/221345604-1a6ec27d-8c0e-40ac-bb78-a4c70e4afc38.png)
![gm-24h测试结果](https://user-images.githubusercontent.com/76025773/221345639-b999b6c4-8853-4eff-be4b-4762589c75ba.png)          

* Coverage          
cd coverage-analysis                    
mkdir gm-analysis                            
cd gm-analysis                                
tar -xvf GraphicsMagick-1.3.26.tar.gz                                                      
cd GraphicsMagick-1.3.26                                          
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static                                           
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all                                     
/afl-cov/afl-cov -d ../../GraphicsMagick-1.3.26/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/gm-analysis/GraphicsMagick-1.3.26/ -e "./utilities/gm convert @@ /dev/null -f AFL_FILE"                   
![18b0e3090e6247949d20fa872db4d8f](https://user-images.githubusercontent.com/76025773/221351078-fa667e4f-fced-47c6-907f-6911074d007b.png)


* Speed           
afl-plot fuzz_out graph_fuzz_out                          
![exec_speed](https://user-images.githubusercontent.com/76025773/221346181-b722fd14-8ded-4bd4-b81f-3e780d46b853.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221346186-c8445036-5b2b-4b9e-bc28-73998769afb1.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221346188-0164e05d-4e45-4488-a57f-f375d3317839.png)
