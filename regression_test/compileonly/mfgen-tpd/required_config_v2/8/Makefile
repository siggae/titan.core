##############################################################################
# Copyright (c) 2000-2016 Ericsson Telecom AB
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
#
# Contributors:
#   Szabo, Bence Janos
#
##############################################################################
TOPDIR := ../../../..
include $(TOPDIR)/Makefile.regression

ifdef LCOV
COVERAGE_FLAG := -C
endif

# ${MAKEPROG} has the same content as the built-in ${MAKE},
# except the special handling of ${MAKE} does not apply.
# If we used ${MAKE} in the rules below, 'make -n' would succeed once,
# then fail on every subsequent invocation until a 'make clean' is done. 

# Hierarchy 
#            a--->e------------->
#            |    |             |
#            |    |             |
#            b<---|---<         |
#            |    |   |         |f:1
#            c    |   |f:1=>b:1 |
#            |    |   |         |
#            d>--->   <---------f
# d refers both b and e
#Result will be: a:Default, b:1, c:Default, d:Default, e:Default, f:1
MAKEPROG := ${MAKE}

all: CheckTpd 

BuildTpd:
	$(TTCN3_DIR)/bin/ttcn3_makefilegen -f $(MFGEN_FLAGS) $(COVERAGE_FLAG) \
	-t a.tpd -g

CheckTpd: BuildTpd
	if [ ! -f "./binDefault/Makefile" ] || [ ! -L "./binDefault/aDefault.ttcn" ] || [ -L "./binDefault/a1.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -L "./binDefault/b1.ttcn" ] || [ -L "./binDefault/bDefault.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -L "./binDefault/cDefault.ttcn" ] || [ -L "./binDefault/c1.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -L "./binDefault/dDefault.ttcn" ] || [ -L "./binDefault/d1.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -L "./binDefault/eDefault.ttcn" ] || [ -L "./binDefault/e1.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi
	if [ ! -L "./binDefault/f1.ttcn" ] || [ -L "./binDefault/fDefault.ttcn" ]; \
	then echo "Makefilegen required config test 8 failed: Overall verdict: fail" && exit 1; fi

clean:
	-rm -rf binDefault

distclean: clean
	-rm -f *.out

.PHONY: all clean distclean BuildTpd CheckTpd

