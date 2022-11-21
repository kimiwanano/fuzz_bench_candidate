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
