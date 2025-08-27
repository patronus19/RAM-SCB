#^CFG GLOW makefile
SHELL = /bin/sh

include ../Makefile.def
include ../Makefile.conf
include Makefile.DEPEND

RAMFLAGS = -fallow-argument-mismatch -fallow-invalid-boz

MODULES = \
	bands.o\
	cglow.o\
	conduct.o\
	egrid.o\
	ephoto.o\
	etrans.o\
	exsect.o\
	fieldm.o\
	gchem.o\
	geo2mag.o\
	ModGlowBasic.o\
	glow.o\
	iri90.o\
	maxt.o\
	mzgrid.o\
	nrlmsise00.o\
	pegrid.o\
	qback.o\
	qproton.o\
	rcolum.o\
	recipes2.o\
	rout.o\
	snoem.o\
	snoemint.o\
	solzen.o\
	ssflux.o

DEPEND:
	@perl ${SCRIPTDIR}/depend.pl ${MODULES}

MY_LIB = ${LIBDIR}/libGLOW.a

LIB:	DEPEND
	${MAKE} ${MY_LIB}
	@echo
	@echo ${MY_LIB} has been brought up to date.
	@echo

${MY_LIB}: ${MODULES}
	rm -f ${MY_LIB}
	${AR} ${MY_LIB} ${MODULES}


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

distclean: clean
	rm -f Makefile.DEPEND
	rm -rf *.o *.mod

clean:
	rm -f *~ core *.o *.mod fort.* a.out *.exe *.a *.so *.protex
