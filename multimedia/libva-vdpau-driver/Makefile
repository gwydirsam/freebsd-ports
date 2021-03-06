# $FreeBSD$

PORTNAME=	libva-vdpau-driver
PORTVERSION=	0.7.4
PORTREVISION=	7
CATEGORIES=	multimedia
MASTER_SITES=	http://www.freedesktop.org/software/vaapi/releases/${PORTNAME}/

MAINTAINER=	madpilot@FreeBSD.org
COMMENT=	VDPAU-based backend for VAAPI

LICENSE=	GPLv2 GPLv3
LICENSE_COMB=	dual

LIB_DEPENDS=	libvdpau.so:multimedia/libvdpau
BUILD_DEPENDS=	${LOCALBASE}/libdata/pkgconfig/libva.pc:multimedia/libva \
		${LOCALBASE}/include/linux/videodev2.h:multimedia/v4l_compat

LICENSE_FILE_GPLv2=	${WRKSRC}/COPYING
USES=		libtool gmake localbase pkgconfig tar:bzip2
USE_GL=		gl

GNU_CONFIGURE=	yes

PLIST_FILES=	lib/va/nvidia_drv_video.so lib/va/s3g_drv_video.so lib/va/vdpau_drv_video.so

OPTIONS_DEFINE=	DEBUG
DEBUG_CONFIGURE_ENABLE=	debug

.include <bsd.port.pre.mk>

.if defined(STRIP) && ${STRIP} != ""
INSTALL_TARGET=	install-strip
.endif

post-patch:	.SILENT
	${REINPLACE_CMD} -e '/LIBS/{ s/-ldl//; s/-lrt//; }' \
		-e 's|driverdir|& --define-variable prefix=${PREFIX}|' \
		-e '/\^vdpau_version/s|$$CC -E|& ${CPPFLAGS}|' \
		 ${WRKSRC}/configure

.include <bsd.port.post.mk>
