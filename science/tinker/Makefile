PORTNAME=	tinker
DISTVERSION=	8.10.5
CATEGORIES=	science
MASTER_SITES=	https://dasher.wustl.edu/tinker/downloads/

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	General purpose molecular modelling package
WWW=		https://dasher.wustl.edu/tinker/

LICENSE=	TINKER
LICENSE_NAME=	TINKER license agreement
LICENSE_FILE=	${WRKSRC}/doc/license.pdf
LICENSE_PERMS=	auto-accept # internal academic purposes only, no commercial use

LIB_DEPENDS=	libfftw3.so:math/fftw3

USES=		fortran gmake

WRKSRC=		${WRKDIR}/${PORTNAME}
BUILD_WRKSRC=	${WRKSRC}/source
INSTALL_WRKSRC=	${WRKSRC}/source

MAKE_ENV=	HAVE_G2C=yes
MAKE_ARGS=	RANLIB=ranlib BINDIR=${STAGEDIR}${PREFIX}/bin LIBS="${LOCALBASE}/lib/libfftw3.a ${LOCALBASE}/lib/libfftw3_threads.a"
MAKEFILE=	${WRKSRC}/make/Makefile
EXTRACT_AFTER_ARGS=--exclude fftw --exclude windows --exclude macosx

SUB_FILES=	pkg-message

BINARY_ALIAS=	gfortran=gfortran${GCC_DEFAULT}

OPTIONS_DEFINE=	OPTIMIZED_FFLAGS DOCS EXAMPLES

OPTIONS_DEFINE_amd64=	SSE
OPTIONS_DEFINE_i386=	SSE
OPTIONS_DEFAULT_amd64=	SSE
OPTIONS_DEFAULT_i386=	SSE

SSE_MAKE_ARGS=	PORT_SIMD_FLAGS="-msse -msse2 -mfpmath=sse"

OPTIMIZED_FFLAGS_DESC=	compilation optimizations

PORTDOCS=	*
PORTEXAMPLES=	*

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MOPTIMIZED_FFLAGS}
FFLAGS+=	-O3 -ffast-math -finline-functions -fomit-frame-pointer -funroll-loops -fexpensive-optimizations
.if (${ARCH} == "i386")
FFLAGS+=	-mfancy-math-387 -malign-double
.endif # i386
.endif

post-extract:
	@${RM} ${BUILD_WRKSRC}/*.c
	@${RM} ${WRKSRC}/other/eopbend.orig
	# remove bundled linux libraries
	@${RM} ${WRKSRC}/lib/linux/*

post-patch:
	@${REINPLACE_CMD} -i '' 's|\.\./bin/|${STAGEDIR}${PREFIX}/bin/|' ${BUILD_WRKSRC}/../bench/bench*.run

post-install:
	@${MKDIR} ${STAGEDIR}${DATADIR}
	@${MKDIR} ${STAGEDIR}${DATADIR}/params
	cd ${WRKSRC}/params && ${INSTALL_DATA} * ${STAGEDIR}${DATADIR}/params
	@${MKDIR} ${STAGEDIR}${DATADIR}/test
	cd ${WRKSRC}/test && ${INSTALL_DATA} * ${STAGEDIR}${DATADIR}/test

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC}/doc && ${INSTALL_DATA} 0README *.pdf ${STAGEDIR}${DOCSDIR}

post-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	cd ${WRKSRC}/example && ${INSTALL_DATA} \
		0README *.make *.dyn *.int *.frac *.key *.seq *.pdb *.xyz \
		${STAGEDIR}${EXAMPLESDIR}

benchmarks: stage
.for n in 1 2 3 4 5 6 7 8 9
	@cd ${BUILD_WRKSRC}/../bench && ./bench${n}.run
.endfor

.include <bsd.port.mk>
