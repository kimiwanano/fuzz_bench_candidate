**exiv2-0.26**
* Bug type: uncontrolled-memory-allocation    
* CVE ID:    
[CVE-2018-4868](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-4868)
* Download && Compile:   
apt-get install libexpat1-dev    
wget https://github.com/Exiv2/exiv2/releases/download/v0.26/exiv2-0.26-trunk.tar.gz    
tar -xvf exiv2-0.26-trunk.tar.gz     
cd exiv2-trunk/    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all
* Reproduce:      
afl-fuzz -m none -b 46 -i afl-fuzz/in/ -o afl-fuzz/out/ ./bin/exiv2 -pX @@   
