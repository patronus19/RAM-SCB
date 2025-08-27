SHELL =/bin/sh

include ../Makefile.def
include ../Makefile.conf
include Makefile.DEPEND

OBJECTS = \
	IM_wrapper.o

SEARCH_EXTRA = -I${COUPLERDIR} -I${LIBRARYDIR} -I../src
INCL_EXTRA   = -I${COUPLERDIR} -I${LIBRARYDIR} -I../src

LIBEXT   = ${LIBDIR}/libEXT.a
LIBGLOW  = ${LIBDIR}/libGLOW.a

DEPEND:
	@perl ${SCRIPTDIR}/depend.pl ${SEARCH} ${OBJECTS}

MY_LIB = ${LIBDIR}/libIM.a

LIB: DEPEND
	make ${MY_LIB}
	@echo
	@echo ${MY_LIB} has been brought up to date.
	@echo

RAM_LIB = ../src/libRAM_SCB.a

${MY_LIB}: ${RAM_LIB} ${OBJECTS} ${MAKEFILE_COMP_SELECT}
	echo "making ${MY_LIB} in srcInterface"
	echo 'create ${MY_LIB}' > mergelibs.mri
	echo 'addlib ${RAM_LIB}' >> mergelibs.mri
	echo 'addlib ${LIBEXT}' >> mergelibs.mri
	echo 'addlib ${LIBGLOW}' >> mergelibs.mri
	echo 'addmod ${OBJECTS}' >> mergelibs.mri
	echo 'save' >> mergelibs.mri
	echo 'end' >> mergelibs.mri
	ar -M < mergelibs.mri

clean:
	rm -f *.o

distclean: clean
	rm -f Makefile.DEPEND
