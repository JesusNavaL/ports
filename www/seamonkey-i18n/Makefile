# Created by: Andrew Pantyukhin <infofarmer@FreeBSD.org>
# $FreeBSD$

PORTNAME=	seamonkey-i18n
PORTVERSION=	2.49.2
CATEGORIES=	www mail news editors irc
MASTER_SITES=	MOZILLA/${PORTNAME:S|-i18n||}/releases/${DISTVERSION}/langpack \
		MOZILLA/${PORTNAME:S|-i18n||}/candidates/${DISTVERSION}-candidates/build1/linux-i686/xpi \
		LOCAL/jbeich/${DIST_SUBDIR}
PKGNAMEPREFIX=
DISTFILES=	${SEAMONKEY_I18N_:S/$/.langpack.xpi/:S/^/seamonkey-${PORTVERSION}./}
DIST_SUBDIR=	xpi/${DISTNAME}

MAINTAINER=	gecko@FreeBSD.org
COMMENT=	Localized interface for SeaMonkey

USES=		zip gecko:seamonkey
USE_XPI=	seamonkey linux-seamonkey

NO_ARCH=	yes
USE_SUBMAKE=	yes

WDIR=	langpack-*@seamonkey.mozilla.org

XPI_DISTNAMES=	${SEAMONKEY_I18N_}

PLIST?=		${WRKDIR}/plist
PLISTF?=	${WRKDIR}/plist_files

.include "${.CURDIR}/Makefile.option"
.include <bsd.port.pre.mk>

.ifndef WITHOUT_SWITCHER
RUN_DEPENDS+=	xpi-quick-locale-switcher>=0:www/xpi-quick-locale-switcher
.endif

.include "${.CURDIR}/Makefile.lang"

SEAMONKEY_I18N_?=	${SEAMONKEY_I18N}

.for dist in ${XPI_DISTNAMES}
XPI_ID_${dist}=		langpack-${dist}@seamonkey.mozilla.org
.endfor

pre-everything::
	@${ECHO_CMD}
	@${ECHO_CMD} "Please define SEAMONKEY_I18N_ALL to install all languages."
	@${ECHO_CMD}

do-extract:
	@${MKDIR} ${WRKSRC}
	@for lang in ${SEAMONKEY_I18N_}; do \
		if ! (${EXTRACT_CMD} ${EXTRACT_BEFORE_ARGS} ${_DISTDIR}/seamonkey-${PORTVERSION}.$$lang.langpack.xpi -d ${WRKSRC}/langpack-$$lang@seamonkey.mozilla.org);\
		then \
			exit 1; \
		fi; \
		cd ${WRKSRC}/langpack-$$lang@seamonkey.mozilla.org/; \
		${FIND} -H -s * ! -type d | \
		${SED} -e "s|^|lib/xpi/langpack-$$lang@seamonkey.mozilla.org/|" >> ${PLISTF}; \
	done
	${CAT} ${PLISTF} | ${SORT} >> ${PLIST}

do-install:
	@${MKDIR} ${STAGEDIR}${XPI_LIBDIR} ${XPI_LINKFARMS:S,^,${STAGEDIR},}
	cd ${WRKSRC}; ${PAX} -rw . ${STAGEDIR}${XPI_LIBDIR}
	${CHMOD} -R a+rX,go-w ${STAGEDIR}${XPI_LIBDIR}/${WDIR}/
	@for sldir in ${XPI_LINKFARMS}; do \
		${ECHO_CMD} "@dir $${sldir}" ${_A}; \
	done
	@${ECHO_CMD} '@exec for _dir in ${XPI_LINKFARMS} ; { \
		${LN} -sf ${XPI_LIBDIR}/${WDIR} $$_dir/ ${_Q}; }' ${_A}
	@${ECHO_CMD} '@unexec for _dir in ${XPI_LINKFARMS}; { ${RM} $$_dir/${WDIR} ; }' ${_A}

post-patch:
	${FIND} ${WRKSRC} -name install.rdf -print0 | \
		${XARGS} -0L1 ${REINPLACE_CMD} -i '' -e '/<?xml/,$$!d'

list-langs:
	@fetch -qo- "https://ftp.mozilla.org/pub/mozilla.org/${PORTNAME:S|-i18n||}/releases/${PORTVERSION}/langpack"|\
		${PERL} -ne 'if(/.*href="${DISTNAME:S|-i18n||}.([a-zA-Z-]+).langpack.xpi.*/){print "$$1\n"}' |\
		${AWK} 'BEGIN{ORS=" "}{print $$1}END{printf "\nNumber of languages: %d\n",NR}'

.include "${.CURDIR}/../xpi-adblock/Makefile.xpi"

.include <bsd.port.post.mk>
