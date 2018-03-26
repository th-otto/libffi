CC = gcc
CFLAGS = -O2 -Wall
HOST=$(shell ../../config.guess)
prefix = ../../$(HOST)
includedir = $(prefix)/include
CPPFLAGS = -I$(includedir)
CPPFLAGS += $(CPUFLAGS)
LIBFFI = ../../$(HOST)/.libs/libffi.a

all: check-call check-callback

test-call: test-call.c testcases.c $(LIBFFI)
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -o test-call test-call.c $(LIBFFI)

test-callback: test-callback.c testcases.c $(LIBFFI)
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -o test-callback test-callback.c $(LIBFFI)

check-call: test-call
	./test-call > test-call.out
	LC_ALL=C uniq -u < test-call.out > failed-call
	test '!' -s failed-call

check-callback: test-callback
	./test-callback > test-callback.out
	LC_ALL=C uniq -u < test-callback.out > failed-callback
	test '!' -s failed-callback

clean:
	rm -f test-call test-callback test-call.out test-callback.out failed-call failed-callback
