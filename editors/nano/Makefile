# Created by: Philippe Lefebvre <nemesis@balistik.net>
# $FreeBSD$

PORTNAME=	nano
PORTVERSION=	2.9.4
CATEGORIES=	editors
MASTER_SITES=	http://www.nano-editor.org/dist/v${PORTVERSION:R}/ GNU

MAINTAINER=	danilo@FreeBSD.org
COMMENT=	Nano's ANOther editor, an enhanced free Pico clone

LICENSE=	GPLv3

CONFLICTS=	nano-devel-2*

USES=		charsetfix ncurses
GNU_CONFIGURE=	yes

USE_HARDENING=	safestack

CONFIGURE_ARGS=	--docdir=${DOCSDIR} --enable-utf8
MAKE_ARGS+=	install_htmlmanDATA=install-htmlmanDATA
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

OPTIONS_DEFINE=	DOCS EXAMPLES NLS
OPTIONS_SUB=	yes

DOCS_USES=	groff

NLS_USES=		gettext
NLS_CONFIGURE_ENABLE=	nls

INFO=		nano

PORTSCOUT=	limitw:1,even

post-configure:
	${REINPLACE_CMD} -e 's/update_revision//g' ${WRKSRC}/src/Makefile

post-build:
	cd ${WRKSRC}/doc; ${REINPLACE_CMD} \
		-e 's:SYSCONFDIR:${PREFIX}/etc:g' \
		-e 's:EXAMPLESDIR:${EXAMPLESDIR}:g' \
		nano.1 rnano.1 nanorc.5 ${WRKSRC}/doc/${INFO:=.info}

post-install:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/doc/sample.nanorc ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
