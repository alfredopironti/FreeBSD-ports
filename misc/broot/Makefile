PORTNAME=	broot
DISTVERSIONPREFIX=	v
DISTVERSION=	1.22.1
PORTREVISION=	1
CATEGORIES=	misc

MAINTAINER=	lcook@FreeBSD.org
COMMENT=	Quick and easy new way to see and navigate directory trees
WWW=		https://dystroy.org/broot/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libgit2.so:devel/libgit2 \
		libonig.so:devel/oniguruma
RUN_DEPENDS=	git:devel/git

USES=		cargo
USE_GITHUB=	yes
GH_ACCOUNT=	canop

SUB_FILES=	pkg-message
PLIST_FILES=	bin/${PORTNAME} \
		man/man1/${PORTNAME}.1.gz
PORTDOCS=	CHANGELOG.md README.md documentation.md features.md

OPTIONS_DEFINE=		CLIPBOARD DOCS
OPTIONS_DEFAULT=	CLIPBOARD

CLIPBOARD_DESC=	Enable terminal X11 clipboard support

CLIPBOARD_USES=		python:3.6+,build xorg
CLIPBOARD_USE=		XORG=xcb
CLIPBOARD_BINARY_ALIAS=	python3=${PYTHON_CMD}
CLIPBOARD_VARS=		CARGO_FEATURES+=clipboard

_BUILD_VERSION=	${DISTVERSION}
_BUILD_DATE=	$$(date +'%Y/%m/%d')

pre-build:
	@${MV} ${WRKSRC}/man/page \
		${WRKSRC}/man/${PORTNAME}.1
	@${REINPLACE_CMD} -e 's|#version|${_BUILD_VERSION}|g' \
		-e "s|#date|${_BUILD_DATE}|g" \
		${WRKSRC}/man/${PORTNAME}.1

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}
	${INSTALL_MAN} ${WRKSRC}/man/${PORTNAME}.1 \
		${STAGEDIR}${MAN1PREFIX}/man/man1

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} \
		${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
