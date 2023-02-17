**libksba-1.3.5**		
* Bug type:    			
  
* CVE ID:     			
   
* Download && Compile:   
apt-get install libgpg-error-dev   
或
wget ftp://ftp.gnupg.org/gcrypt/libgpg-error/libgpg-error-1.27.tar.gz   
tar zxvf libgpg-error-1.27.tar.gz   
cd libgpg-error-1.27   
./configure --prefix=/usr --libdir=/usr/lib64   
make   
make install   
tar -xjf libksba-1.3.5.tar.bz2   
cd libksba-1.3.5/   
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static   
make all   
* Reproduce:   
afl-fuzz -m none -t 500 -b 50 -i afl-fuzz/in/ -o afl-fuzz/out/ ./libksba-1.3.5/tests/cert-basic @@   
