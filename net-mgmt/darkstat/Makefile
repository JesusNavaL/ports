# Created by: Anders Nordby <anders@FreeBSD.org>
# $FreeBSD$

PORTNAME=	darkstat
PORTVERSION=	3.0.719
CATEGORIES=	net-mgmt
MASTER_SITES=	https://unix4lyfe.org/darkstat/

MAINTAINER=	emikulic@gmail.com
COMMENT=	Network statistics gatherer and reporter

USE_HARDENING=	safestack

USE_RC_SUBR=	darkstat

USES=		tar:bzip2
GNU_CONFIGURE=	yes

PORTDOCS=	AUTHORS INSTALL README
PLIST_FILES=	sbin/darkstat man/man8/darkstat.8.gz

OPTIONS_DEFINE=	DOCS

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
