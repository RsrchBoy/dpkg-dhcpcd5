TOP?=	..
include ${TOP}/iconfig.mk

PROG=		test
SRCS=		test.c
SRCS+=		test_hmac_md5.c hmac_md5.c ${MD5_SRC}

CFLAGS?=	-O2
CSTD?=		c99
CFLAGS+=	-std=${CSTD}

CPPFLAGS+=	-I../crypt

.PATH:		../crypt

VPATH=		. ../crypt

OBJS+=		${SRCS:.c=.o}

.c.o:
	${CC} ${CFLAGS} ${CPPFLAGS} -c $< -o $@

crypt/md5.o:
	mkdir -p crypt
	( cd crypt && ln -s ../../crypt/md5.o . ||: )

all: ${PROG}

clean:
	rm -f ${OBJS} ${PROG} ${PROG}.core ${CLEANFILES}

.depend: ${SRCS} ${COMPAT_SRCS}
	${CC} ${CPPFLAGS} -MM ${SRCS} ${COMPAT_SRCS} > .depend

depend: .depend

${PROG}: ${DEPEND} ${OBJS}
	cp ../crypt/*.o .
	${CC} ${LDFLAGS} -o $@ ${OBJS} ${LDADD}
