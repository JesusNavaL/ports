# $FreeBSD$

PORTNAME=	gb
PORTVERSION=	0.4.4
DISTVERSIONPREFIX=	v
CATEGORIES=	devel

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Project based build tool for Go

LICENSE=	MIT

USES=		go
USE_GITHUB=	yes
GH_ACCOUNT=	constabulary
GH_TUPLE=	pkg:errors:645ef00:errors/../src/github.com/pkg/errors

PLIST_FILES=	bin/gb bin/gb-vendor

PORTDOCS=	README.md

GO_PKGNAME=	github.com/${GH_ACCOUNT}/${GH_PROJECT}
GO_TARGET=	./...

do-install:
	${INSTALL_PROGRAM} ${GO_WRKDIR_BIN}/* ${STAGEDIR}/${LOCALBASE}/bin
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	( cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/ ; )

.include <bsd.port.mk>
