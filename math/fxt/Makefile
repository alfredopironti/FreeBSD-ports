PORTNAME=	fxt
PORTVERSION=	2023.05.07
CATEGORIES=	math
MASTER_SITES=	https://www.jjj.de/fxt/

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Llibrary of low-level algorithms
WWW=		https://www.jjj.de/fxt/

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/COPYING.txt

USES=		compiler:c++11-lang gmake

MAKE_ENV=	FXT_INSTALL="${INSTALL_DATA}"
MAKEFILE=	makefile
WRKSRC=		${WRKDIR}/fxt

OPTIONS_DEFINE=	EXAMPLES

post-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	cd ${WRKSRC}/demo && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
