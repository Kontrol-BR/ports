# $FreeBSD$

PORTNAME=	unanimity
DISTVERSION=	g20180307
PORTREVISION=	1
CATEGORIES=	biology

MAINTAINER=	jwb@FreeBSD.org
COMMENT=	Pacific Biosciences consensus library and applications

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_aarch64=		fails to compile: mmintrin.h:47:5: use of undeclared identifier '__builtin_ia32_emms'; did you mean '__builtin_isless'?

# Sensitive to dependency versions, use latest commit for everything
BUILD_DEPENDS=	pbseqan==g20171002:biology/pbseqan \
		pbbam==g20180416:biology/pbbam \
		pbcopper==g20180413:biology/pbcopper
LIB_DEPENDS=	libhts.so:biology/htslib \
		libboost_regex.so:devel/boost-libs

USES=		cmake pkgconfig python
USE_GITHUB=	yes
GH_ACCOUNT=	PacificBiosciences
GH_TAGNAME=	6f11a13e1472b8c00337ba8c5e94bf83bdab31d6

CMAKE_ARGS+=	-DHTSLIB_INCLUDE_DIRS:STRING=${LOCALBASE}/include/htslib \
		-DHTSLIB_LIBRARIES:STRING="-L${LOCALBASE}/lib -lhts" \
		-DPacBioBAM_INCLUDE_DIRS:STRING=${LOCALBASE}/include/pbbam \
		-DPacBioBAM_LIBRARIES:STRING="-L${LOCALBASE}/lib -lpbbam" \
		-DSEQAN_INCLUDE_DIRS:STRING=${LOCALBASE}/include/PacBio \
		-Dpbcopper_INCLUDE_DIRS=${LOCALBASE}/include \
		-Dpbcopper_LIBRARIES="-L${LOCALBASE}/lib -lpbcopper"
CFLAGS_i386=	-msse2 -Wno-c++11-narrowing

PLIST_FILES=	bin/arrow bin/ccs bin/gcpp lib/libcc2.a lib/libunanimity.a

post-install:
	${INSTALL_DATA} ${WRKSRC}/src/libcc2.a ${WRKSRC}/src/libunanimity.a \
		${STAGEDIR}${PREFIX}/lib

.include <bsd.port.mk>
