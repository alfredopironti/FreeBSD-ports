PORTNAME=	mail
PORTVERSION=	3.2.1
DISTVERSIONPREFIX=	v
CATEGORIES=	mail

MAINTAINER=	brnrd@FreeBSD.org
COMMENT=	Mail app for Nextcloud
WWW=		https://apps.nextcloud.com/apps/mail

LICENSE_FILE=	${WRKSRC}/COPYING

NEXTCLOUD_RUN_DEPENDS=	26

USES=		cpe gettext nextcloud php:flavors
USE_PHP=	imap

CPE_VENDOR=	nextcloud

.include <bsd.port.mk>
