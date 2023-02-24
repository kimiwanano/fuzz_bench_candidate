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
make all           
* Reproduce:      
afl-fuzz -m none -t 5000 -b 46 -i afl-fuzz/in/ -o afl-fuzz/out/ ./BUILD/src/appl/jasper --input @@ --output test.bmp --output-format bmp

![jasper-24h测试界面](https://user-images.githubusercontent.com/76025773/221199253-a699ad54-dea0-47b0-b4a5-9a0cb224304c.png)
![jasper-24h测试结果](https://user-images.githubusercontent.com/76025773/221199257-e273c72b-24d6-4283-b5d4-99e74ef16a06.png)
