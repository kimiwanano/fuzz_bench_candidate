**poppler-0.75.0**
* Bug type: 
Buffer overflow
* CVE ID:     
[CVE-2020-27778](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-27778)    
* Download && Compile:    
wget https://poppler.freedesktop.org/poppler-0.75.0.tar.xz    
tar -xvf poppler-0.75.0.tar.xz    
cd poppler-0.75.0    
mkdir build    
cd build/    
apt-get install -y pkg-config    
apt-get install -y libfontconfig1-dev    
apt-get install libtiff-dev    
apt-get install libjpeg-dev    
apt-get install libopenjp2-7-dev    
CC=afl-clang-fast CXX=afl-clang-fast++ cmake ..     
make all
* Reproduce:    
afl-fuzz -m none -i afl-fuzz/in/ -o afl-fuzz/out/ ./build/utils/pdftohtml @@    
