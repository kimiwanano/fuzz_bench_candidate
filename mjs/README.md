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
afl-fuzz -m none -t 5000 -b 48 -i afl-fuzz/in/ -o afl-fuzz/out/ ./mjs.out @@    

![mjs-24h测试界面](https://user-images.githubusercontent.com/76025773/221210373-137d75d7-6ae7-4970-a230-ce890e0cb737.png)
![mjs-24小时测试结果](https://user-images.githubusercontent.com/76025773/221210393-c88e12be-84ce-4921-9aa4-723f61a7350c.png)

* Coverage      
cd coverage-analysis          
mkdir mjs-analysis              
cd mjs-analysis           
git clone https://github.com/cesanta/mjs          
cd mjs          
git checkout 2827bd00b59bdc176a010b22fc4acde9b580d6c2           
gcc -fprofile-arcs -ftest-coverage mjs.c -DMJS_MAIN -o mjs.out -ldl         
/afl-cov/afl-cov -d ../../mjs/fuzz_out/ --enable-branch-coverage -c /fuzz_bench/coverage-analysis/mjs/ -e "./mjs.out @@ -f AFL_FILE"        
![c53417997b1ce3fd0e669374db84e49](https://user-images.githubusercontent.com/76025773/221210310-ec643f9f-043d-477a-ab45-6326c5bc26fe.png)

* Speed         
afl-plot fuzz_out graph_fuzz_out            
![exec_speed](https://user-images.githubusercontent.com/76025773/221210596-2841d30b-990f-410b-b12e-5a4571940b2c.png)
![high_freq](https://user-images.githubusercontent.com/76025773/221210608-d35d2ae1-65e6-42ed-9de3-a357bc3e8d42.png)
![low_freq](https://user-images.githubusercontent.com/76025773/221210626-edf254b4-d38e-48bd-872e-11f31a905ecf.png)
