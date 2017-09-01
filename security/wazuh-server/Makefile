# $FreeBSD$

PORTNAME=	wazuh
DISTVERSION=	2.0.1
CATEGORIES=	security
DSTVERSIONPREFIX=	v
PKGNAMESUFFIX= -server

MAINTAINER=	rainbow@newcontext.com
COMMENT=	Wazuh fork of the ossec HIDS

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=


USES= gmake
USES= gcc
USES= readline
USE_OPENSSL= yes

USERS=          ossec ossecm ossecr
GROUPS=         ossec

USE_GITHUB=	yes
GH_ACCOUNT=	wazuh

IS_INTERACTIVE=	yes

WRKSRC=		${WRKDIR}/wazuh-${DISTVERSION}

.if !defined(CLIENT_ONLY)
OPTIONS_DEFINE=	MYSQL PGSQL

MYSQL_VARS=	WITH_DB=yes
MYSQL_USE=	MYSQL=client
MYSQL_PORTDOCS=	mysql.schema

PGSQL_VARS=	WITH_DB=yes
PGSQL_USES=	pgsql
PGSQL_PORTDOCS=	postgresql.schema
.endif

OPTIONS_DEFINE+=	DOCS

SUB_LIST=	PORTNAME=${PORTNAME}
SUB_FILES=	pkg-message
PLIST_SUB=	PORTNAME=${PORTNAME}
DOCSFILES=	BUGS CONFIG CONTRIBUTORS INSTALL LICENSE
PORTDOCS=	${DOCSFILES}

.include <bsd.port.pre.mk>

CONFLICTS_INSTALL=	ossec-hids-server ossec-hids-local ossec-hids-client

.if defined(CLIENT_ONLY)
SUB_LIST+=	PRECMD=:
PKGNAMESUFFIX=	-agent
CONFLICTS_INSTALL=	wazuh-local wazuh-server
.elif defined(LOCAL_ONLY)
CONFLICTS_INSTALL=	wazuh-agent wazuh-server
PKGNAMESUFFIX=	-local
.else
CONFLICTS_INSTALL=	wazuh-agent wazuh-local
.endif

# Still working on stuff here

.include <bsd.port.mk>