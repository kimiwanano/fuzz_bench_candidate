**mjs-1.20.1**
* Bug type: stack-overflow    
* CVE ID:    
[CVE-2020-36366](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-36366)    
* Download && Compile:     
git clone https://github.com/cesanta/mjs   
cd mjs  
git checkout 2827bd00b59bdc176a010b22fc4acde9b580d6c2               
afl-clang-fast mjs.c -DMJS_MAIN -o mjs.out -ldl
* Reproduce:     
afl-fuzz -m none -b 47 -i afl-fuzz/in/ -o afl-fuzz/out/ ./mjs.out @@    

![image](https://user-images.githubusercontent.com/76025773/201923702-ba0bdea8-949a-4d2c-ba41-90802e4ac9e5.png)
