
libksba/cert-basic

Install instructions:

	sudo apt-get install libgpg-error-dev
	tar -xjf libksba-1.3.5.tar.bz2
	cd libksba-1.3.5/
	./configure --disable-shared CFLAGS="-g -O2 -Wall -Wcast-align -Wshadow -Wstrict-prototypes -Wpointer-arith -Wno-pointer-sign -fvisibility=hidden -no-pie"
	make all

Running:
	
	afl-fuzz-saveinputs -i seed_dir -o out_dir -e 1440 -Q -- ./libksba-1.3.5/tests/cert-basic @@
