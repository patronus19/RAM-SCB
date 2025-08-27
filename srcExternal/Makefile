SHELL =/bin/sh

include ../Makefile.def
include ../Makefile.conf
include Makefile.DEPEND

RAMFLAGS = -fallow-argument-mismatch -fallow-invalid-boz

OBJECTS = \
	planeweim.o       \
	gaussian_filter.o \
        Geopack-2008_dp.o \
        T89.o             \
        T96.o             \
        T02.o             \
        TS04.o            \
        TS07.o            \
        w2k_r8.o          \
        w05.o             \
        fct-source.o      \
        irisub.o          \
        iritec.o          \
        iriflip.o         \
        iridreg.o         \
        irifun.o          \
        nrlmsise00_sub.o  \
        igrf.o

SEARCH_EXTRA = -I${LIBDIR} -I../src
INCL_EXTRA   = -I${LIBDIR} -I../src

DEPEND:
	@perl ${SCRIPTDIR}/depend.pl ${SEARCH} ${OBJECTS}

MY_LIB = ${LIBDIR}/libEXT.a

LIB: DEPEND
	make ${MY_LIB}
	@echo
	@echo ${MY_LIB} has been brought up to date.
	@echo

${MY_LIB}: ${OBJECTS} ${MAKEFILE_COMP_SELECT}
	${AR} ${MY_LIB} ${OBJECTS}
	
.f90.o:
	${COMPILE.f90} ${Cflag3} ${RAMFLAGS} $<

.F90.o:
	${COMPILE.f90} -DsysLinux -DcompGFORTRAN ${Cflag3} $<

.f.o:
	${COMPILE.f77} ${Cflag3} ${RAMFLAGS} -ffixed-line-length-132 $<

.for.o:
	${COMPILE.f77} ${Cflag3} ${RAMFLAGS} -ffixed-line-length-132 $<

.ftn.o:
	${COMPILE.f77} ${Cflag3} ${RAMFLAGS} -ffixed-line-length-132 $<
	

clean:
	rm -f *.o

distclean: clean
	rm -f Makefile.DEPEND
