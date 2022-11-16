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
* Reproduce:      
afl-fuzz -m none -b 45 -i afl-fuzz/in/ -o afl-fuzz/out/ ./BUILD/src/appl/jasper --input @@ --output test.bmp --output-format bmp

![image](https://user-images.githubusercontent.com/76025773/202127288-5b60f806-5000-40fb-8875-5f469330f78a.png)
