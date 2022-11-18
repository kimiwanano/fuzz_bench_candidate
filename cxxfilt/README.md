**cxxfilt-2.31**
* Bug type:     
stack-overflow       
* CVE ID:      
[CVE-2018-9138](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-9138)           
[CVE-2018-9996](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-9996)         
[CVE-2018-17985](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-17985)         
[CVE-2018-18484](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18484)       
[CVE-2018-18700](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-18700)          
* Download:

* Reproduce:      
afl-fuzz -m none -i afl-fuzz-cxxfilt/in/ -o afl-fuzz-cxxfilt/out/ ./binutils/cxxfilt -n    
