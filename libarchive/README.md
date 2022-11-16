**libarchive-3.1.0**     
* Bug type:     
infinite loop, NULL pointer dereference     
* CVE ID:     
[CVE-2015-8930](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-8930)     
[CVE-2015-8916](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-8916)     
[CVE-2015-8917](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-8917)     
* Download && Compile:   
wget https://www.libarchive.org/downloads/libarchive-3.1.0.tar.gz   
tar -xvf libarchive-3.1.0.tar.gz     
cd libarchive-3.1.0    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static     
make all     
* Reproduce:      
afl-fuzz -m none -i afl-fuzz/in/ -o afl-fuzz/out/ ./bsdtar -O -xf @@     
