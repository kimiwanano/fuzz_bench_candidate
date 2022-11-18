**nm-2.31**    
* Bug type:    
stack-overflow    
* CVE ID:   
[CVE-2018-12641](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-12641)    
[CVE-2018-17985](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-17985)    
[CVE-2018-18484](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18484)    
[CVE-2018-18700](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18700)   
[CVE-2018-18701](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18701)   
[CVE-2019-9070](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9070)     
[CVE-2019-9071](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-9071)    
* Download:     
wget https://ftp.gnu.org/gnu/binutils/binutils-2.31.1.tar.gz   
tar -xvf binutils-2.31.1.tar.gz   
cd binutils-2.31.1    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all     
* Reproduce:     
afl-fuzz -m none -i afl-fuzz-cxxfilt/in/ -o afl-fuzz-cxxfilt/out/ ./binutils/cxxfilt -n      
