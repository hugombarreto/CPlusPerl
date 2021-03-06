# Makefile source, C+Perl
#
# Copyright (c) 2013 Hugo de Freitas Siqueira Sadok Menna Barreto <sadok.com.br>
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.


CXX=g++
LD=g++
AR=ar rvs
CXXFLAGS=$(shell perl -MExtUtils::Embed -e ccopts) -Dusethreads -Duseithreads -Wall -Wno-write-strings #-g
LDFLAGS=$(shell perl -MExtUtils::Embed -e ldopts) -Dusethreads -Duseithreads #-g

UNAME := $(shell uname)

RM=rm -vf

LIB=CPlusPerl.a
SRCS=PerlInterpreterManager.cpp PerlObject.cpp PerlStack.cpp PerlInterface.cpp PerlException.cpp
OBJS=$(subst .cpp,.o,$(SRCS))

TESTS=test1.cpp
TESTS_OBJS=$(subst .cpp,.o,$(TESTS))
TEST_EXEC= test1

.cpp.o:
	$(CXX) $(CXXFLAGS) -c $<

ifeq ($(UNAME), Linux)
all: $(LIB) .depend

.depend: $(SRCS)
	$(RM) ./.depend
	$(CXX) $(CXXFLAGS) -MM $^ >> ./.depend

-include .depend
else
all: $(LIB)
endif

$(LIB): $(OBJS)
	$(AR) $@ $(OBJS)

test: $(LIB) $(TESTS_OBJS)
	$(LD) -o $(TEST_EXEC) $(TESTS_OBJS) $(LIB) $(LDFLAGS)

clean:
	$(RM) $(LIB) $(OBJS) $(TESTS_OBJS) $(TEST_EXEC) .depend
