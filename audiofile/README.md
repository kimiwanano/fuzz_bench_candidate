**audiofile-0.2.7**     
* Bug type:     
heap-overflow    
* CVE ID:     
[CVE-2017-6834](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6834)     
[CVE-2017-6832](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6832)      
[CVE-2017-6831](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6831)    
* Download:     
wget https://src.fedoraproject.org/repo/pkgs/audiofile/audiofile-0.2.7.tar.gz/a39be317a7b1971b408805dc5e371862/audiofile-0.2.7.tar.gz    
tar -xvf audiofile-0.2.7.tar.gz     
cd audiofile-0.2.7     
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all    
* Reproduce:     
afl-fuzz -m none -t 500 -b 51 -i afl-fuzz/in/ -o afl-fuzz/out/ ./sfcommands/sfconvert @@ out.mp3 format aiff    

![image](https://user-images.githubusercontent.com/76025773/203090553-bf80f352-c069-4652-b71a-1222454c1696.png)

* Coverage      
cd coverage-analysis
mkdir sfconvert-analysis          
cd sfconvert-analysis       
tar -xvf flex-2.6.4.tar.gz              
cd flex-2.6.4                     
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" ./configure --disable-shared --enable-static                  
cd sfcommands               
make clean
CC=gcc CXX=g++ CFLAGS="-fprofile-arcs -ftest-coverage" make all
/afl-cov/afl-cov -d ../sfconvert/afl-fuzz/out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/sfconvert-analysis/audiofile-0.2.7/ -e "./sfconvert out.mp3 format aiff -f AFL_FILE"     

![ce9510a9fa795200b05922c48d7b733](https://user-images.githubusercontent.com/76025773/221092059-0d9598d9-f3a7-4fa7-aaef-6c145833826b.png)
