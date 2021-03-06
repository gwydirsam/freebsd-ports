# $FreeBSD$

PORTNAME=	vault
PORTVERSION=	0.8.3
DISTVERSIONPREFIX=	v
CATEGORIES=	security

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Tool for securely accessing secrets

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	go>=1.9:lang/go

USE_GITHUB=	yes
GH_ACCOUNT=	hashicorp
GH_SUBDIR=	src/github.com/${GH_ACCOUNT}/${PORTNAME}
COMMIT_ID=	6b29fb2b7f70ed538ee2b3c057335d706b6d4e36

USE_RC_SUBR=	vault

USERS=		vault
GROUPS=		vault

PLIST_FILES=	bin/${PORTNAME}

do-build:
	@cd ${WRKSRC}; \
		${SETENV} ${BUILD_ENV} CGO_ENABLED=0 GOPATH=${WRKSRC} \
		go build \
		-ldflags "\
		-X github.com/hashicorp/vault/version.Version=${PORTVERSION} \
		-X github.com/hashicorp/vault/version.VersionPrerelease= \
		-X github.com/hashicorp/vault/version.VersionMetadata= \
		-X github.com/hashicorp/vault/version.GitCommit='${COMMIT_ID}'" \
		-o bin/${PORTNAME}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}

.include <bsd.port.mk>
