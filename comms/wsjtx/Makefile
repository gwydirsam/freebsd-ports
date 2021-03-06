# $FreeBSD$

PORTNAME=	wsjtx
PORTVERSION=	1.8.0
CATEGORIES=	comms hamradio
MASTER_SITES=	SF/wsjt/${PORTNAME}-${PORTVERSION}${DISTVERSIONSUFFIX}
DISTNAME=	${PORTNAME}-${PORTVERSION}
EXTRACT_SUFX=	.tgz
MAINTAINER=	hamradio@FreeBSD.org
COMMENT=	Weak signal ham radio communication package

LICENSE=	GPLv3

BUILD_DEPENDS=	asciidoctor:textproc/rubygem-asciidoctor \
		a2x:textproc/asciidoc \
		${LOCALBASE}/share/xsl/docbook:textproc/docbook-xsl
LIB_DEPENDS=	libfftw3.so:math/fftw3 \
		libfftw3f.so:math/fftw3-float \
		libhamlib.so:comms/hamlib \
		libxslt.so:textproc/libxslt \
		libomp.so.0:devel/openmp

MAKE_JOBS_UNSAFE=	yes
USE_GL=		yes
USE_QT5=	gui buildtools qmake_build widgets multimedia concurrent printsupport serialport
USES=		cmake compiler:c++11-lib dos2unix fortran pkgconfig tar:tgz
CMAKE_ARGS+=	-DPORT_BUILDING::STRING="ON" \
		-DCMAKE_PREFIX_PATH+=${LOCALBASE}/wsjtx/lib \
		-DLOCALBASE::STRING="${LOCALBASE}"
WRKSRC=		${WRKDIR}/${PORTNAME}

#
# This nonsense is because wsjtx is shipped with a copy of hamlib
# as well as wsjtx
#
do-extract:
	${TAR} xf ${DISTDIR}/${PORTNAME}-${PORTVERSION}${EXTRACT_SUFX} -C${WRKDIR}
	${TAR} xf ${WRKDIR}/${PORTNAME}-${PORTVERSION}/src/wsjtx.tgz -C${WRKDIR}

BROKEN_i386=    does not build on i386 due to openmp

.include <bsd.port.mk>
