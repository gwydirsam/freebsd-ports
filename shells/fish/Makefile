# Created by: Kai Wang <kaiw27@gmail.com>
# $FreeBSD$

PORTNAME=	fish
PORTVERSION=	2.6.0
CATEGORIES=	shells
MASTER_SITES=	http://fishshell.com/files/${PORTVERSION}/

MAINTAINER=	asomers@FreeBSD.org
COMMENT=	User friendly command line shell

LICENSE=	GPLv2

LIB_DEPENDS+=	libpcre2-32.so:devel/pcre2

USES=		autoreconf cpe gmake libtool ncurses pkgconfig pathfix python:3.4+ \
		localbase compiler:c++11-lang shebangfix
SHEBANG_FILES=	share/tools/*.py share/tools/web_config/webconfig.py

CONFLICTS_INSTALL=	comms/mlan3

GNU_CONFIGURE=	yes

CPE_VENDOR=	fishshell

LDFLAGS+=	-L${LOCALBASE}/lib -pthread
MANDIRS=	${DATADIR}/man/man1

OPTIONS_DEFINE=	DOCS NLS
OPTIONS_SUB=	yes

NLS_USES=		gettext
NLS_CONFIGURE_ENV=	ac_cv_func_gettext=yes
NLS_CONFIGURE_OFF=	--without-gettext

post-patch:
	@${REINPLACE_CMD} -e \
		'/^all:/s|user_doc|| ; \
		 s| "$$(HAVE_GETTEXT)" = 1| x$$(HAVE_GETTEXT) = x1| ; \
		 s| $$(HAVE_GETTEXT) = 1| x$$(HAVE_GETTEXT) = x1| ; \
		 s|$$(DESTDIR)$$(bindir)/fish|$$(bindir)/fish|g' \
		 ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e \
		's|-rdynamic|-Wl,--export-dynamic| ; \
		 /pthread_create/d ; \
		 s|ncurses curses|curses| ; \
		 s|ncurses.h||' ${WRKSRC}/configure.ac

post-install:
.for i in fish fish_indent fish_key_reader
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${i}
.endfor

.include <bsd.port.mk>
