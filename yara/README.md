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
./bootstrap.sh     
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all    
* Reproduce:    
afl-fuzz -m none -b 42 -i afl-fuzz/in/ -o afl-fuzz/out/ ./yara @@ strings    

![image](https://user-images.githubusercontent.com/76025773/201911925-6e9b564e-d09d-49b8-9086-e24ef4b0f7ff.png)
