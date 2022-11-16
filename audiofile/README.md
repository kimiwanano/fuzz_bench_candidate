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
afl-fuzz -i afl-fuzz/in/ -o afl-fuzz/out/ ./sfcommands/sfconvert @@ out.mp3 format aiff    
