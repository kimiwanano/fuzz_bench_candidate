**libksba-1.3.5**		
* Bug type:    			
  
* CVE ID:     			
   
* Download && Compile:   			
apt-get install libgpg-error-dev			
tar -xjf libksba-1.3.5.tar.bz2			
cd libksba-1.3.5/		
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static   		 
make all		
* Reproduce:     		
afl-fuzz -m none -t 500 -b 50 -i afl-fuzz/in/ -o afl-fuzz/out/ ./libksba-1.3.5/tests/cert-basic @@  			
