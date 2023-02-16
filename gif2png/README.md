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
afl-fuzz -m none -i afl-fuzz/in/ -o afl-fuzz/out/ ./gif2png @@    
