# ###########################################################
# from fedora repos
LDC=ldc2

test1: test1.x libtest1.so
	LD_LIBRARY_PATH=. ./test1.x

test2: test2.x libtest2a.so libtest2b.so
	LD_LIBRARY_PATH=. ./test2.x
clean:
	rm -f *.o
	rm -f *.so
	rm -f *.x

LIBS= -lphobos-ldc -ldruntime-ldc -lrt -lpthread -ldl -lm -lpython2.7

%.o: %.d
	echo "building $@"
	$(LDC) -relocation-model=pic -c $^ -of $@

lib%.so: %.o
	echo "building $@"
	gcc -nostartfiles -shared $(LIBS) $^ -o $@ 

test1.x: test1.c libtest1.so
	echo "building $@"
	LD_LIBRARY_PATH=. gcc $< -L. -ltest1 -o $@
test2.x: test2.c libtest2a.so libtest2b.so
	echo "building $@"
	LD_LIBRARY_PATH=. gcc $< -L. -ltest2a -ltest2b -o $@

# ###########################################################