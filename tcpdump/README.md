**tcpdump-4.9.2**
* Bug type:    
heap-overflow, infinite loop    
* CVE ID: 
https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=tcpdump    
* Download && Compile:    
apt-get install libpcap-dev    
wget https://www.tcpdump.org/release/tcpdump-4.9.2.tar.gz    
tar -xzf tcpdump-4.9.2.tar.gz    
cd tcpdump-4.9.2     
CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --disable-shared --enable-static    
make all   
* Reproduce:       
afl-fuzz -m none -i afl-fuzz/in/ -o afl-fuzz/out/ ./tcpdump -nr @@    
