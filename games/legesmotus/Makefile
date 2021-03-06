# Created by: Dmitry Marakasov <amdmi3@FreeBSD.org>
# $FreeBSD$

PORTNAME=	legesmotus
PORTVERSION=	0.4.0
PORTREVISION=	6
CATEGORIES=	games
MASTER_SITES=	SF

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Team-based, networked, 2D shooter set in zero-gravity

LICENSE=	GPLv2 GPLv3
LICENSE_COMB=	dual

NOT_FOR_ARCHS=		aarch64 armv6 armv7
NOT_FOR_ARCHS_REASON=	fails to build: Disallowed architecture for this platform

HAS_CONFIGURE=	yes
CONFIGURE_ARGS=	--prefix="${PREFIX}" \
		--mandir="${PREFIX}/man" \
		--datadir="${DATADIR}"
USES=		gmake
MAKE_ENV=	XDIR=${LOCALBASE}

PORTDATA=	*

OPTIONS_MULTI=	COMPONENTS
OPTIONS_MULTI_COMPONENTS=CLIENT SERVER METASERVER SERVERSCANNER
OPTIONS_DEFAULT=CLIENT SERVER
OPTIONS_SUB=	yes

CLIENT_DESC=		Build client
SERVER_DESC=		Build server
METASERVER_DESC=	Build metaserver
SERVERSCANNER_DESC=	Build server scanner

CLIENT_CONFIGURE_OFF=	--disable-client
CLIENT_USE=		SDL=sdl,image,ttf,mixer GL=gl
CLIENT_DESKTOP_ENTRIES= "Leges Motus" \
			"" \
			"${DATADIR}/sprites/blue_head32.png" \
			"legesmotus" \
			"Game;ActionGame;" \
			""
SERVER_CONFIGURE_OFF=		--disable-server
METASERVER_CONFIGURE_ON=	--enable-metaserver
SERVERSCANNER_CONFIGURE_ON=	--enable-serverscanner

.include <bsd.port.mk>
