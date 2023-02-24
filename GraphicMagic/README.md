**GraphicsMagick-1.3.26**
* Bug type:    
use-after-free    
* CVE ID:     
[CVE-2017-11403](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-11403)    
* Download && Compile:   
wget https://sourceforge.net/projects/graphicsmagick/files/graphicsmagick-history/1.3/GraphicsMagick-1.3.26.tar.gz     
tar -xvf GraphicsMagick-1.3.26.tar.gz    
cd GraphicsMagick-1.3.26    
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all
* Reproduce:     
afl-fuzz -m none -t 5000 -b 40 -i afl-fuzz/in/ -o afl-fuzz/out/ ./utilities/gm convert @@ /dev/null    
