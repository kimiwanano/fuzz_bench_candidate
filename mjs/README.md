**mjs-1.20.1**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2020-36366](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-36366)    
* Download && Compile:     
afl-clang-fast mjs.c -DMJS_MAIN -o mjs.out -ldl
* Reproduce:     
afl-fuzz -m none -b 47 -i afl-fuzz/in/ -o afl-fuzz/out/ ./mjs.out @@    

![image](https://user-images.githubusercontent.com/76025773/201923702-ba0bdea8-949a-4d2c-ba41-90802e4ac9e5.png)
