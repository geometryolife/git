# The default target of this Makefile is...
all::

# Import tree-wide shared Makefile behavior and libraries
include ../../shared.mak

include ../../config.mak.uname
-include ../../config.mak.autogen
-include ../../config.mak

TARGETS = scalar$(X) scalar.o
GITLIBS = ../../common-main.o ../../libgit.a ../../xdiff/lib.a

all: scalar$(X) ../../bin-wrappers/scalar

$(GITLIBS):
	$(QUIET_SUBDIR0)../.. $(QUIET_SUBDIR1) $(subst ../../,,$@)

$(TARGETS): $(GITLIBS) scalar.c
	$(QUIET_SUBDIR0)../.. $(QUIET_SUBDIR1) $(patsubst %,contrib/scalar/%,$@)

clean:
	$(RM) $(TARGETS) ../../bin-wrappers/scalar

../../bin-wrappers/scalar: ../../wrap-for-bin.sh Makefile
	@mkdir -p ../../bin-wrappers
	$(QUIET_GEN)sed -e '1s|#!.*/sh|#!$(SHELL_PATH_SQ)|' \
	     -e 's|@@BUILD_DIR@@|$(shell cd ../.. && pwd)|' \
	     -e 's|@@PROG@@|contrib/scalar/scalar$(X)|' < $< > $@ && \
	chmod +x $@

test: all
	$(MAKE) -C t

.PHONY: $(GITLIBS) all clean test FORCE
