**mjs-1.20.1**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2020-36366](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-36366)    
* Download && Compile:     
afl-clang-fast mjs.c -DMJS_MAIN -o mjs.out -ldl
* Reproduce:     
afl-fuzz -m none -b 47 -i afl-fuzz/in/ -o afl-fuzz/out/ ./mjs.out @@
