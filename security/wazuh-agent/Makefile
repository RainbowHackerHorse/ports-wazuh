# $FreeBSD$

PORTNAME=       wazuh
PORTVERSION=    2.1.0
DISTVERSIONPREFIX=      v
PORTREVISION?=  0
CATEGORIES=     security
USE_GITHUB=     yes
GH_ACCOUNT=     wazuh
GH_TAGNAME=	v2.1.0
PKGNAMESUFFIX=  -agent

MAINTAINER=     jonathan@wazuh.com
COMMENT?=       Security tool to monitor and check logs and intrusions

CFLAGS+=        -ferror-limit=0

USES=           gmake readline
USE_OPENSSL=    yes

.if defined(MAINTAINER_MODE)
UID_FILES+=     ../../UIDs
GID_FILES+=     ../../GIDs
.endif
USERS=          ossec ossecm ossecr
GROUPS=         ossec

.if !defined(CLIENT_ONLY)
OPTIONS_DEFINE= MYSQL PGSQL

USES+=          shebangfix
SHEBANG_LANG=   expect
expect_OLD_CMD= "/usr/bin/env expect"
expect_CMD=     ${LOCALBASE}/bin/expect
.endif

OPTIONS_DEFINE+=        DOCS

SUB_LIST=       PORTNAME=${PORTNAME}
SUB_FILES=      pkg-message
PLIST_SUB=      PORTNAME=${PORTNAME}
DOCSFILES=      BUGS CONFIG CONTRIBUTORS INSTALL LICENSE
PORTDOCS=       ${DOCSFILES}

#WRKSRC_SUBDIR=	src
USE_GMAKE= 	yes
PLIST=		${.CURDIR}/pkg-plist

.include <bsd.port.pre.mk>

do-build:
	cd ${WRKSRC}/src && ${GMAKE} TARGET=agent PREFIX=/opt/
do-install:
	@${CP} ${WRKSRC}/etc/ossec-agent.conf* ${STAGEDIR}${PREFIX}/${PORTNAME}/etc/ossec.conf.sample	
.include <bsd.port.mk>

