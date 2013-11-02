# $Id: Makefile.in,v 1.4 2006/08/19 09:12:14 dtucker Exp $

sysconfdir=/etc/ssh
piddir=/var/run
srcdir=../../../openbsd-compat/regress
top_srcdir=../../..

VPATH=../../../openbsd-compat/regress
CC=gcc
LD=gcc
CFLAGS=-g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wformat-security -Wno-pointer-sign -Wno-unused-result -fno-strict-aliasing -D_FORTIFY_SOURCE=2 -fno-builtin-memset -fstack-protector-all -D_FORTIFY_SOURCE=2 -g -O2 -fPIE -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security -DLOGIN_PROGRAM=\"/bin/login\" -DLOGIN_NO_ENDOPT -DSSH_EXTRAVERSION=\"Debian-4\" 
CPPFLAGS=-I. -I.. -I$(srcdir) -I$(srcdir)/..     -DHAVE_CONFIG_H
EXEEXT=
LIBCOMPAT=../libopenbsd-compat.a
LIBS=-lcrypto -ldl -lutil -lz -lnsl  -lcrypt -lresolv -Wl,-z,relro -lgssapi_krb5 -lkrb5 -lk5crypto -lcom_err
LDFLAGS= -fstack-protector-all -Wl,--as-needed -fPIE -pie -Wl,-z,relro -Wl,-z,now $(LIBCOMPAT)

TESTPROGS=closefromtest$(EXEEXT) snprintftest$(EXEEXT) strduptest$(EXEEXT) \
	strtonumtest$(EXEEXT)

all:	t-exec ${OTHERTESTS}

%$(EXEEXT):	%.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) -o $@ $< $(LIBCOMPAT) $(LIBS)

t-exec:	$(TESTPROGS)
	@echo running compat regress tests
	@for TEST in ""$?; do \
		echo "run test $${TEST}" ... 1>&2; \
		./$${TEST}$(EXEEXT) || exit $$? ; \
	done
	@echo finished compat regress tests

clean:
	rm -f *.o *.a core $(TESTPROGS) valid.out

distclean: clean
	rm -f Makefile *~
