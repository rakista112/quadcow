dnl $Id: configure.ac,v 1.62 2004/03/18 10:03:34 bagder Exp $
dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.57)

dnl We don't know the version number "staticly" so we use a dash here
AC_INIT(curl, [-], [curl-bug@haxx.se])

dnl configure script copyright
AC_COPYRIGHT([Copyright (c) 1998 - 2004 Daniel Stenberg, <daniel@haxx.se>
This configure script may be copied, distributed and modified under the 
terms of the curl license; see COPYING for more details])

AC_CONFIG_SRCDIR([lib/urldata.h])
AM_CONFIG_HEADER(lib/config.h src/config.h)
AM_MAINTAINER_MODE

dnl SED is needed by some of the tools
AC_PATH_PROG( SED, sed, , $PATH:/usr/bin:/usr/local/bin)
AC_SUBST(SED)

dnl AR is used by libtool, and try the odd Solaris path too
AC_PATH_PROG( AR, ar, , $PATH:/usr/bin:/usr/local/bin:/usr/ccs/bin)
AC_SUBST(AR)

dnl figure out the libcurl version
VERSION=`$SED -ne 's/^#define LIBCURL_VERSION "\(.*\)"/\1/p' ${srcdir}/include/curl/curl.h`
AM_INIT_AUTOMAKE(curl,$VERSION)
AC_MSG_CHECKING([curl version])
AC_MSG_RESULT($VERSION)

dnl
dnl we extract the numerical version for curl-config only
VERSIONNUM=`$SED -ne 's/^#define LIBCURL_VERSION_NUM 0x\(.*\)/\1/p' ${srcdir}/include/curl/curl.h`
AC_SUBST(VERSIONNUM)

dnl Solaris pkgadd support definitions
PKGADD_PKG="HAXXcurl"
PKGADD_NAME="cURL - a client that groks URLs"
PKGADD_VENDOR="curl.haxx.se"
AC_SUBST(PKGADD_PKG)
AC_SUBST(PKGADD_NAME)
AC_SUBST(PKGADD_VENDOR)


dnl
dnl Detect the canonical host and target build environment
dnl

AC_CANONICAL_HOST
dnl Get system canonical name
AC_DEFINE_UNQUOTED(OS, "${host}", [cpu-machine-OS])

dnl Check for AIX weirdos
AC_AIX

dnl Checks for programs.
AC_PROG_CC

dnl check for how to do large files
AC_SYS_LARGEFILE

dnl check for cygwin stuff
AC_LIBTOOL_WIN32_DLL

dnl libtool setup
AM_PROG_LIBTOOL

AC_MSG_CHECKING([if we need -no-undefined])
case $host in
  *-*-cygwin | *-*-mingw* | *-*-pw32*)
    need_no_undefined=yes
    ;;
  *)
    need_no_undefined=no
    ;;
esac
AC_MSG_RESULT($need_no_undefined)
AM_CONDITIONAL(NO_UNDEFINED, test x$need_no_undefined = xyes)

AC_MSG_CHECKING([if we need -mimpure-text])
case $host in
  *-*-solaris2*)
    if test "$GCC" = "yes"; then
      mimpure="yes"
    fi
    ;;
  *)
    mimpure=no
    ;;
esac
AC_MSG_RESULT($mimpure)
AM_CONDITIONAL(MIMPURE, test x$mimpure = xyes)

dnl The install stuff has already been taken care of by the automake stuff
dnl AC_PROG_INSTALL
AC_PROG_MAKE_SET

dnl ************************************************************
dnl switch off particular protocols
dnl
AC_MSG_CHECKING([whether to support http])
AC_ARG_ENABLE(http,
AC_HELP_STRING([--enable-http],[Enable HTTP support])
AC_HELP_STRING([--disable-http],[Disable HTTP support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_HTTP, 1, [to disable HTTP])
       AC_MSG_WARN([disable HTTP disables FTP over proxy and GOPHER too])
       AC_DEFINE(CURL_DISABLE_GOPHER, 1, [to disable GOPHER])
       AC_SUBST(CURL_DISABLE_HTTP)
       AC_SUBST(CURL_DISABLE_GOPHER)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support ftp])
AC_ARG_ENABLE(ftp,
AC_HELP_STRING([--enable-ftp],[Enable FTP support])
AC_HELP_STRING([--disable-ftp],[Disable FTP support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_FTP, 1, [to disable FTP])
       AC_SUBST(CURL_DISABLE_FTP)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support gopher])
AC_ARG_ENABLE(gopher,
AC_HELP_STRING([--enable-gopher],[Enable GOPHER support])
AC_HELP_STRING([--disable-gopher],[Disable GOPHER support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_GOPHER, 1, [to disable GOPHER])
       AC_SUBST(CURL_DISABLE_GOPHER)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support file])
AC_ARG_ENABLE(file,
AC_HELP_STRING([--enable-file],[Enable FILE support])
AC_HELP_STRING([--disable-file],[Disable FILE support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_FILE, 1, [to disable FILE])
       AC_SUBST(CURL_DISABLE_FILE)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support ldap])
AC_ARG_ENABLE(ldap,
AC_HELP_STRING([--enable-ldap],[Enable LDAP support])
AC_HELP_STRING([--disable-ldap],[Disable LDAP support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_LDAP, 1, [to disable LDAP])
       AC_SUBST(CURL_DISABLE_LDAP)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support dict])
AC_ARG_ENABLE(dict,
AC_HELP_STRING([--enable-dict],[Enable DICT support])
AC_HELP_STRING([--disable-dict],[Disable DICT support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_DICT, 1, [to disable DICT])
       AC_SUBST(CURL_DISABLE_DICT)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)
AC_MSG_CHECKING([whether to support telnet])
AC_ARG_ENABLE(telnet,
AC_HELP_STRING([--enable-telnet],[Enable TELNET support])
AC_HELP_STRING([--disable-telnet],[Disable TELNET support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       AC_DEFINE(CURL_DISABLE_TELNET, 1, [to disable TELNET])
       AC_SUBST(CURL_DISABLE_TELNET)
       ;;
  *)   AC_MSG_RESULT(yes)
       ;;
  esac ],
       AC_MSG_RESULT(yes)
)

dnl **********************************************************************
dnl Check for built-in manual
dnl **********************************************************************

AC_MSG_CHECKING([whether to provide built-in manual])
AC_ARG_ENABLE(manual,
AC_HELP_STRING([--enable-manual],[Enable built-in manual])
AC_HELP_STRING([--disable-manual],[Disable built-in manual]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       ;;
  *)   AC_MSG_RESULT(yes)
       USE_MANUAL="1"
       ;;
  esac ],
       AC_MSG_RESULT(yes)
       USE_MANUAL="1"
)
dnl The actual use of the USE_MANUAL variable is done much later in this
dnl script to allow other actions to disable it as well.


dnl **********************************************************************
dnl Checks for libraries.
dnl **********************************************************************

dnl gethostbyname without lib or in the nsl lib?
AC_CHECK_FUNC(gethostbyname,
              [HAVE_GETHOSTBYNAME="1"
              ],
              [ AC_CHECK_LIB(nsl, gethostbyname,
                             [HAVE_GETHOSTBYNAME="1"
                             LIBS="$LIBS -lnsl"
                             ])
              ])

if test "$HAVE_GETHOSTBYNAME" != "1"
then
  dnl gethostbyname in the socket lib?
  AC_CHECK_LIB(socket, gethostbyname,
               [HAVE_GETHOSTBYNAME="1"
               LIBS="$LIBS -lsocket"
               ])
fi

dnl At least one system has been identified to require BOTH nsl and socket
dnl libs at the same time to link properly.
if test "$HAVE_GETHOSTBYNAME" != "1"
then
  AC_MSG_CHECKING([trying gethostbyname with both nsl and socket libs])
  my_ac_save_LIBS=$LIBS
  LIBS="-lnsl -lsocket $LIBS"
  AC_TRY_LINK( ,
             [gethostbyname();],
             [ dnl found it!
             HAVE_GETHOSTBYNAME="1",
             AC_MSG_RESULT([yes])],
             [ dnl failed!
             AC_MSG_RESULT([no])
             dnl restore LIBS
             LIBS=$my_ac_save_LIBS]
             )
fi

if test "$HAVE_GETHOSTBYNAME" != "1"
then
  dnl This is for Msys/Mingw
  AC_MSG_CHECKING([for gethostbyname in ws2_32])
  my_ac_save_LIBS=$LIBS
  LIBS="-lws2_32 $LIBS"
  AC_TRY_LINK([#include <winsock2.h>],
               [gethostbyname("www.dummysite.com");],
               [ dnl worked!
               AC_MSG_RESULT([yes])
               HAVE_GETHOSTBYNAME="1"],
               [ dnl failed, restore LIBS
               LIBS=$my_ac_save_LIBS
               AC_MSG_RESULT(no)]
             )
fi

if test "$HAVE_GETHOSTBYNAME" = "1"; then
  AC_DEFINE(HAVE_GETHOSTBYNAME, 1, [If you have gethostbyname])
else
  AC_MSG_ERROR([couldn't find libraries for gethostbyname()])
fi

dnl resolve lib?
AC_CHECK_FUNC(strcasecmp, , [ AC_CHECK_LIB(resolve, strcasecmp) ])

if test "$ac_cv_lib_resolve_strcasecmp" = "$ac_cv_func_strcasecmp"; then
  AC_CHECK_LIB(resolve, strcasecmp,
              [LIBS="-lresolve $LIBS"],
               ,
               -lnsl)
fi

dnl socket lib?
AC_CHECK_FUNC(connect, , [ AC_CHECK_LIB(socket, connect) ])

dnl dl lib?
AC_CHECK_FUNC(dlclose, , [ AC_CHECK_LIB(dl, dlopen) ])

AC_MSG_CHECKING([whether to use libgcc])
AC_ARG_ENABLE(libgcc,
AC_HELP_STRING([--enable-libgcc],[use libgcc when linking]),
[ case "$enableval" in
  yes)
        LIBS="$LIBS -lgcc"
       AC_MSG_RESULT(yes)
       ;;
  *)   AC_MSG_RESULT(no)
       ;;
  esac ],
       AC_MSG_RESULT(no)
)

dnl **********************************************************************
dnl Check for the presence of the winmm library.
dnl **********************************************************************

AC_MSG_CHECKING([for timeGetTime in winmm])
my_ac_save_LIBS=$LIBS
LIBS="-lwinmm $LIBS"
AC_TRY_LINK([#include <windef.h>
             #include <mmsystem.h>
             ],
             [timeGetTime();],
             [ dnl worked!
             AC_MSG_RESULT([yes])
             ],
             [ dnl failed, restore LIBS
             LIBS=$my_ac_save_LIBS
             AC_MSG_RESULT(no)]
           )

dnl **********************************************************************
dnl Checks for IPv6
dnl **********************************************************************

AC_MSG_CHECKING([whether to enable ipv6])
AC_ARG_ENABLE(ipv6,
AC_HELP_STRING([--enable-ipv6],[Enable ipv6 (with ipv4) support])
AC_HELP_STRING([--disable-ipv6],[Disable ipv6 support]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       ipv6=no
       ;;
  *)   AC_MSG_RESULT(yes)
       ipv6=yes
       ;;
  esac ],

  AC_TRY_RUN([ /* is AF_INET6 available? */
#include <sys/types.h>
#include <sys/socket.h>
main()
{
 if (socket(AF_INET6, SOCK_STREAM, 0) < 0)
   exit(1);
 else
   exit(0);
}
],
  AC_MSG_RESULT(yes)
  ipv6=yes,
  AC_MSG_RESULT(no)
  ipv6=no,
  AC_MSG_RESULT(no)
  ipv6=no
))

if test "$ipv6" = "yes"; then
  CURL_CHECK_WORKING_GETADDRINFO
fi

dnl **********************************************************************
dnl Check how non-blocking sockets are set
dnl **********************************************************************
AC_ARG_ENABLE(nonblocking,
AC_HELP_STRING([--enable-nonblocking],[Enable detecting how to do it])
AC_HELP_STRING([--disable-nonblocking],[Disable non-blocking socket detection]),
[
  if test "$enableval" = "no" ; then
    AC_MSG_WARN([non-blocking sockets disabled])
    AC_DEFINE(HAVE_DISABLED_NONBLOCKING, 1,
    [to disable NON-BLOCKING connections])
  else
    CURL_CHECK_NONBLOCKING_SOCKET
  fi
],
[
  CURL_CHECK_NONBLOCKING_SOCKET
])

dnl **********************************************************************
dnl Check for the random seed preferences 
dnl **********************************************************************

AC_ARG_WITH(egd-socket,
AC_HELP_STRING([--with-egd-socket=FILE],
               [Entropy Gathering Daemon socket pathname]),
    [ EGD_SOCKET="$withval" ]
)
if test -n "$EGD_SOCKET" ; then
	AC_DEFINE_UNQUOTED(EGD_SOCKET, "$EGD_SOCKET",
        [your Entropy Gathering Daemon socket pathname] )
fi

dnl Check for user-specified random device
AC_ARG_WITH(random,
AC_HELP_STRING([--with-random=FILE],[read randomness from FILE (default=/dev/urandom)]),
    [ RANDOM_FILE="$withval" ],
    [
        dnl Check for random device
        AC_CHECK_FILE("/dev/urandom", [ RANDOM_FILE="/dev/urandom"] )
    ]
)
if test -n "$RANDOM_FILE" ; then
	AC_SUBST(RANDOM_FILE)
	AC_DEFINE_UNQUOTED(RANDOM_FILE, "$RANDOM_FILE",
        [a suitable file to read random data from])
fi

dnl **********************************************************************
dnl Check if the operating system allows programs to write to their own argv[]
dnl **********************************************************************

AC_MSG_CHECKING([if argv can be written to])
AC_CACHE_VAL(curl_cv_writable_argv, [
AC_RUN_IFELSE([[
int main(int argc, char ** argv) {
	argv[0][0] = ' ';
	return (argv[0][0] == ' ')?0:1;
}
	]],
	curl_cv_writable_argv=yes,
	curl_cv_writable_argv=no,
	curl_cv_writable_argv=cross)
])
case $curl_cv_writable_argv in
yes)
	AC_DEFINE(HAVE_WRITABLE_ARGV, 1, [Define this symbol if your OS supports changing the contents of argv])
	AC_MSG_RESULT(yes)
	;;
no)
	AC_MSG_RESULT(no)
	;;
*)
        AC_MSG_RESULT(no)
        AC_MSG_WARN([the previous check could not be made default was used])
	;;
esac

dnl **********************************************************************
dnl Check for the presence of Kerberos4 libraries and headers
dnl **********************************************************************

AC_ARG_WITH(krb4-includes,
AC_HELP_STRING([--with-krb4-includes=DIR],
               [Specify location of kerberos4 headers]),[
 CPPFLAGS="$CPPFLAGS -I$withval"
 KRB4INC="$withval"
 want_krb4=yes
 ])

AC_ARG_WITH(krb4-libs,
AC_HELP_STRING([--with-krb4-libs=DIR],[Specify location of kerberos4 libs]),[
 LDFLAGS="$LDFLAGS -L$withval"
 KRB4LIB="$withval"
 want_krb4=yes
 ])


OPT_KRB4=off
AC_ARG_WITH(krb4,dnl
AC_HELP_STRING([--with-krb4=DIR],[where to look for Kerberos4]),[
  OPT_KRB4="$withval"
  if test X"$OPT_KRB4" != Xyes
  then
    LDFLAGS="$LDFLAGS -L$OPT_KRB4/lib$libsuff"
    KRB4LIB="$OPT_KRB4/lib$libsuff"
    CPPFLAGS="$CPPFLAGS -I$OPT_KRB4/include"
    KRB4INC="$OPT_KRB4/include"
  fi
  want_krb4="yes"
 ])

AC_MSG_CHECKING([if Kerberos4 support is requested])

if test "$want_krb4" = yes
then
  if test "$ipv6" = "yes"; then
    echo krb4 is not compatible with IPv6
    exit 1
  fi
  AC_MSG_RESULT(yes)

  dnl Check for & handle argument to --with-krb4

  AC_MSG_CHECKING(where to look for Kerberos4)
  if test X"$OPT_KRB4" = Xyes
  then
    AC_MSG_RESULT([defaults])
  else
    AC_MSG_RESULT([libs in $KRB4LIB, headers in $KRB4INC])
  fi

  dnl Check for DES library
  AC_CHECK_LIB(des, des_pcbc_encrypt,
  [
    AC_CHECK_HEADERS(des.h)

    dnl resolv lib?
    AC_CHECK_FUNC(res_search, , [AC_CHECK_LIB(resolv, res_search)])

    dnl Check for the Kerberos4 library
    AC_CHECK_LIB(krb, krb_net_read,
    [
      dnl Check for header files
      AC_CHECK_HEADERS(krb.h)

      dnl we found the required libraries, add to LIBS
      LIBS="-lkrb -ldes $LIBS"

      dnl Check for function krb_get_our_ip_for_realm
      dnl this is needed for NAT networks
      AC_CHECK_FUNCS(krb_get_our_ip_for_realm)

      dnl add define KRB4
      AC_DEFINE(HAVE_KRB4, 1,
      [if you have the Kerberos4 libraries (including -ldes)])

      dnl substitute it too!
      KRB4_ENABLED=1
      AC_SUBST(KRB4_ENABLED)

      dnl the krb4 stuff needs a strlcpy()
      AC_CHECK_FUNCS(strlcpy)

    ])
  ])
else
  AC_MSG_RESULT(no)
fi

dnl **********************************************************************
dnl Check for FBopenssl(SPNEGO) libraries
dnl **********************************************************************

AC_ARG_WITH(spnego,
  AC_HELP_STRING([--with-spnego=DIR],
                 [Specify location of SPNEGO library fbopenssl]),
  [ SPNEGO_ROOT="$withval"
    want_spnego="yes" ]
)
AC_MSG_CHECKING([if SPNEGO support is requested])
if test x"$want_spnego" = xyes; then

  if test X"$SPNEGO_ROOT" = Xyes; then
     AC_MSG_ERROR([FBOpenSSL libs and/or directories were not found where specified!])
     AC_MSG_RESULT(no)
  else
     if test -z "$SPNEGO_LIB_DIR"; then
        LDFLAGS="$LDFLAGS -L$SPNEGO_ROOT -lfbopenssl"
     else
        LDFLAGS="$LDFLAGS $SPNEGO_LIB_DIR"
     fi
 
     AC_MSG_RESULT(yes)
     AC_DEFINE(HAVE_SPNEGO, 1, [Define this if you have the SPNEGO library fbopenssl])
  fi
else
  AC_MSG_RESULT(no)
fi

dnl **********************************************************************
dnl Check for GSS-API libraries
dnl **********************************************************************

AC_ARG_WITH(gssapi-includes,
  AC_HELP_STRING([--with-gssapi-includes=DIR],
                 [Specify location of GSSAPI header]),
  [ GSSAPI_INCS="-I$withval" 
    want_gss="yes" ]
)

AC_ARG_WITH(gssapi-libs,
  AC_HELP_STRING([--with-gssapi-libs=DIR],
  		 [Specify location of GSSAPI libs]),
  [ GSSAPI_LIBS="-L$withval -lgssapi"
    want_gss="yes" ]
)

AC_ARG_WITH(gssapi,
  AC_HELP_STRING([--with-gssapi=DIR],
                 [Where to look for GSSAPI]),
  [ GSSAPI_ROOT="$withval"
    want_gss="yes" ]
)

AC_MSG_CHECKING([if GSSAPI support is requested])
if test x"$want_gss" = xyes; then
  if test -z "$GSSAPI_INCS"; then
     if test -f "$GSSAPI_ROOT/bin/krb5-config"; then
        GSSAPI_INCS=`$GSSAPI_ROOT/bin/krb5-config --cflags gssapi`
     else
        GSSAPI_INCS="-I$GSSAPI_ROOT/include"
     fi
  fi
  CPPFLAGS="$CPPFLAGS $GSSAPI_INCS"
  
  if test -z "$GSSAPI_LIB_DIR"; then
     if test -f "$GSSAPI_ROOT/bin/krb5-config"; then
        gss_ldflags=`$GSSAPI_ROOT/bin/krb5-config --libs gssapi`
	LDFLAGS="$LDFLAGS $gss_ldflags"
     else
        LDFLAGS="$LDFLAGS -L$GSSAPI_ROOT/lib$libsuff -lgssapi"
     fi
  else
     LDFLAGS="$LDFLAGS $GSSAPI_LIB_DIR"
  fi

  AC_MSG_RESULT(yes)
  AC_DEFINE(HAVE_GSSAPI, 1, [if you have the gssapi libraries])

  if test -n "$GSSAPI_INCS"; then
    # cut off the preceding -I from the include path
    GSSAPI_INCS=`echo $GSSAPI_INCS | sed -e s/^-I//g`
  fi

  if test -f "$GSSAPI_INCS/gssapi.h"; then
      AC_DEFINE(HAVE_GSSHEIMDAL, 1, [if you have the Heimdal gssapi libraries])
  else
      AC_DEFINE(HAVE_GSSMIT, 1, [if you have the MIT gssapi libraries])
  fi
  
else
  AC_MSG_RESULT(no)
fi
  

dnl Detect the pkg-config tool, as it may have extra info about the
dnl openssl installation we can use. I *believe* this is what we are
dnl expected to do on really recent Redhat Linux hosts.
AC_PATH_PROG( PKGCONFIG, pkg-config, no, $PATH:/usr/bin:/usr/local/bin)
if test "$PKGCONFIG" != "no" ; then
  AC_MSG_CHECKING([for OpenSSL options using pkg-config])

  $PKGCONFIG --exists openssl
  SSL_EXISTS=$?

  if test "$SSL_EXISTS" -eq "0"; then
    SSL_LIBS=`$PKGCONFIG --libs-only-l openssl 2>/dev/null`
    SSL_LDFLAGS=`$PKGCONFIG --libs-only-L openssl 2>/dev/null`
    SSL_CPPFLAGS=`$PKGCONFIG --cflags-only-I openssl 2>/dev/null`

    LIBS="$LIBS $SSL_LIBS"
    CPPFLAGS="$CPPFLAGS $SSL_CPPFLAGS"
    LDFLAGS="$LDFLAGS $SSL_LDFLAGS"

    AC_MSG_RESULT([yes])
  else
    AC_MSG_RESULT([no])
  fi

fi

dnl **********************************************************************
dnl Check for the presence of SSL libraries and headers
dnl **********************************************************************

dnl Default to compiler & linker defaults for SSL files & libraries.
OPT_SSL=off
dnl Default to no CA bundle
ca="no"
AC_ARG_WITH(ssl,dnl
AC_HELP_STRING([--with-ssl=PATH],[where to look for SSL, PATH points to the SSL installation (default: /usr/local/ssl)])
AC_HELP_STRING([--without-ssl], [disable SSL]),
  OPT_SSL=$withval)

if test X"$OPT_SSL" = Xno
then
  AC_MSG_WARN(SSL/https support disabled)  
else

  dnl Check for and handle argument to --with-ssl.

  dnl save the pre-ssl check flags for a while
  CLEANLDFLAGS="$LDFLAGS"
  CLEANCPPFLAGS="$CPPFLAGS"

  case "$OPT_SSL" in
  yes)
    EXTRA_SSL=/usr/local/ssl ;;
  off)
    EXTRA_SSL= ;;
  *)
    dnl check the given spot right away!
    EXTRA_SSL=$OPT_SSL
    LDFLAGS="$LDFLAGS -L$EXTRA_SSL/lib$libsuff"
    CPPFLAGS="$CPPFLAGS -I$EXTRA_SSL/include/openssl -I$EXTRA_SSL/include"
    ;;
  esac

  AC_CHECK_LIB(crypto, CRYPTO_lock,[
     HAVECRYPTO="yes"
     ],[
     OLDLDFLAGS="$LDFLAGS"
     OLDCPPFLAGS="$CPPFLAGS"
     LDFLAGS="$CLEANLDFLAGS -L$EXTRA_SSL/lib$libsuff"
     CPPFLAGS="$CLEANCPPFLAGS -I$EXTRA_SSL/include/openssl -I$EXTRA_SSL/include"
     AC_CHECK_LIB(crypto, CRYPTO_add_lock,[
       HAVECRYPTO="yes" ], [
       LDFLAGS="$OLDLDFLAGS"
       CPPFLAGS="$OLDCPPFLAGS"
       ])
    ])


  if test "$HAVECRYPTO" = "yes"; then
    dnl This is only reasonable to do if crypto actually is there: check for
    dnl SSL libs NOTE: it is important to do this AFTER the crypto lib

    dnl This is for Msys/Mingw
    AC_MSG_CHECKING([for gdi32])
    my_ac_save_LIBS=$LIBS
    LIBS="-lgdi32 $LIBS"
    AC_TRY_LINK([#include <windef.h>
                 #include <wingdi.h>],
               [GdiFlush();],
               [ dnl worked!
               AC_MSG_RESULT([yes])],
               [ dnl failed, restore LIBS
               LIBS=$my_ac_save_LIBS
               AC_MSG_RESULT(no)]
              )

    AC_CHECK_LIB(crypto, CRYPTO_add_lock)
    AC_CHECK_LIB(ssl, SSL_connect)

    if test "$ac_cv_lib_ssl_SSL_connect" != yes; then
        dnl we didn't find the SSL lib, try the RSAglue/rsaref stuff
        AC_MSG_CHECKING(for ssl with RSAglue/rsaref libs in use);
        OLIBS=$LIBS
        LIBS="$LIBS -lRSAglue -lrsaref"
        AC_CHECK_LIB(ssl, SSL_connect)
        if test "$ac_cv_lib_ssl_SSL_connect" != yes; then
            dnl still no SSL_connect
            AC_MSG_RESULT(no)
            LIBS=$OLIBS
        else
            AC_MSG_RESULT(yes)
        fi
    fi


    dnl Check for SSLeay headers
    AC_CHECK_HEADERS(openssl/x509.h openssl/rsa.h openssl/crypto.h \
                     openssl/pem.h openssl/ssl.h openssl/err.h,
      OPENSSL_ENABLED=1)

    if test $ac_cv_header_openssl_x509_h = no; then
      AC_CHECK_HEADERS(x509.h rsa.h crypto.h pem.h ssl.h err.h,
        OPENSSL_ENABLED=1)
    fi

    dnl If the ENGINE library seems to be around, check for the OpenSSL engine
    dnl header, it is kind of "separated" from the main SSL check
    AC_CHECK_FUNC(ENGINE_init, [ AC_CHECK_HEADERS(openssl/engine.h) ])

    AC_SUBST(OPENSSL_ENABLED)

    AC_MSG_CHECKING([CA cert bundle install path])

    AC_ARG_WITH(ca-bundle,
AC_HELP_STRING([--with-ca-bundle=FILE], [File name to install the CA bundle as])
AC_HELP_STRING([--without-ca-bundle], [Don't install the CA bundle]),
    [ ca="$withval" ],
    [
      if test "x$prefix" != xNONE; then
        ca="\${prefix}/share/curl/curl-ca-bundle.crt"
      else
        ca="$ac_default_prefix/share/curl/curl-ca-bundle.crt"
      fi
    ] )

    if test X"$OPT_SSL" = Xno; then
      ca="no"
    fi

    if test "x$ca" != "xno"; then
      CURL_CA_BUNDLE='"'$ca'"'
      AC_SUBST(CURL_CA_BUNDLE)  
    fi
    AC_MSG_RESULT([$ca])

    dnl these can only exist if openssl exists

    AC_CHECK_FUNCS( RAND_status \
                    RAND_screen \
                    RAND_egd \
                    CRYPTO_cleanup_all_ex_data )

  fi

  if test X"$OPT_SSL" != Xoff &&
     test "$OPENSSL_ENABLED" != "1"; then
    AC_MSG_ERROR([OpenSSL libs and/or directories were not found where specified!])
  fi

fi

AM_CONDITIONAL(CABUNDLE, test x$ca != xno)

dnl **********************************************************************
dnl Check for the presence of ZLIB libraries and headers
dnl **********************************************************************

dnl Check for & handle argument to --with-zlib.

_cppflags=$CPPFLAGS
_ldflags=$LDFLAGS
OPT_ZLIB="/usr/local"
AC_ARG_WITH(zlib,
AC_HELP_STRING([--with-zlib=PATH],[search for zlib in PATH])
AC_HELP_STRING([--without-zlib],[disable use of zlib]),
               [OPT_ZLIB="$withval"])

case "$OPT_ZLIB" in
  no)
    AC_MSG_WARN([zlib disabled]) ;;
  *)
    dnl check for the lib first without setting any new path, since many
    dnl people have it in the default path

    AC_CHECK_LIB(z, inflateEnd,
                   dnl libz found, set the variable
                   [HAVE_LIBZ="1"],
                   dnl if no lib found, try to add the given library
                   [if test -d "$OPT_ZLIB"; then
                      CPPFLAGS="$CPPFLAGS -I$OPT_ZLIB/include"
                      LDFLAGS="$LDFLAGS -L$OPT_ZLIB/lib$libsuff"
                   fi])

    AC_CHECK_HEADER(zlib.h,
      [
      dnl zlib.h was found
      HAVE_ZLIB_H="1"
      dnl if the lib wasn't found already, try again with the new paths
      if test "$HAVE_LIBZ" != "1"; then
        AC_CHECK_LIB(z, gzread,
                     [
                     dnl the lib was found!
                     HAVE_LIBZ="1"
                     ],
                     [ CPPFLAGS=$_cppflags
                     LDFLAGS=$_ldflags])
      fi
      ],
      [
        dnl zlib.h was not found, restore the flags
        CPPFLAGS=$_cppflags
        LDFLAGS=$_ldflags]
      )

    if test "$HAVE_LIBZ" = "1" && test "$HAVE_ZLIB_H" != "1"
    then
      AC_MSG_WARN([configure found only the libz lib, not the header file!])
    elif test "$HAVE_LIBZ" != "1" && test "$HAVE_ZLIB_H" = "1"
    then
      AC_MSG_WARN([configure found only the libz header file, not the lib!])
    elif test "$HAVE_LIBZ" = "1" && test "$HAVE_ZLIB_H" = "1"
    then
      dnl both header and lib were found!
      AC_SUBST(HAVE_LIBZ)
      AC_DEFINE(HAVE_ZLIB_H, 1, [if you have the zlib.h header file])
      AC_DEFINE(HAVE_LIBZ, 1, [if zlib is available])

      LIBS="$LIBS -lz"

      dnl replace 'HAVE_LIBZ' in the automake makefile.ams
      AMFIXLIB="1"
      AC_MSG_NOTICE([found both libz and libz.h header])
    fi
    ;;
esac

dnl set variable for use in automakefile(s)
AM_CONDITIONAL(HAVE_LIBZ, test x"$AMFIXLIB" = x1)

dnl Default is to try the thread-safe versions of a few functions
OPT_THREAD=on

dnl detect AIX 4.3 or later
dnl see full docs on this reasoning in the lib/hostip.c source file
AC_MSG_CHECKING([AIX 4.3 or later])
AC_PREPROC_IFELSE([
#if defined(_AIX) && defined(_AIX43)
printf("just fine");
#else
#error "this is not AIX 4.3 or later"
#endif
],
 [ AC_MSG_RESULT([yes])
   OPT_THREAD=off ],
 [ AC_MSG_RESULT([no]) ]
)

AC_ARG_ENABLE(thread,dnl
AC_HELP_STRING([--disable-thread],[don't look for thread-safe functions])
AC_HELP_STRING([--enable-thread],[look for thread-safe functions]),
[ case "$enableval" in
  no)
    OPT_THREAD=off
    AC_MSG_WARN(libcurl will not get built using thread-safe functions)
    ;;
  *)
    ;;
  esac
]
)

if test X"$OPT_THREAD" = Xoff
then
  AC_DEFINE(DISABLED_THREADSAFE, 1, \
Set to explicitly specify we don't want to use thread-safe functions)
else
  if test "$ipv6" != "yes"; then
    dnl dig around for gethostbyname_r()
    CURL_CHECK_GETHOSTBYNAME_R()

    dnl dig around for gethostbyaddr_r()
    CURL_CHECK_GETHOSTBYADDR_R()
  fi

  dnl poke around for inet_ntoa_r()
  CURL_CHECK_INET_NTOA_R()

  dnl is there a localtime_r()
  CURL_CHECK_LOCALTIME_R()

  AC_CHECK_FUNCS( gmtime_r )

fi

dnl **********************************************************************
dnl Back to "normal" configuring
dnl **********************************************************************

dnl Checks for header files.
AC_HEADER_STDC

dnl First check for the very most basic headers. Then we can use these
dnl ones as default-headers when checking for the rest!
AC_CHECK_HEADERS(
        sys/types.h \
        sys/time.h \
        sys/select.h \
        sys/socket.h \
        sys/ioctl.h \
        assert.h \
        unistd.h \
        malloc.h \
        stdlib.h \
        limits.h \
        arpa/inet.h \
        net/if.h \
        netinet/in.h \
        netdb.h \
        sys/sockio.h \
        sys/stat.h \
        sys/param.h \
        termios.h \
        termio.h \
        sgtty.h \
        fcntl.h \
        dlfcn.h \
        alloca.h \
        winsock.h \
        time.h \
        io.h \
        pwd.h \
        utime.h \
        sys/utime.h \
        sys/poll.h \
        setjmp.h,
dnl to do if not found
[],
dnl to do if found
[],
dnl default includes
[
#ifdef HAVE_SYS_TYPES_H
#include <sys/types.h>
#endif
#ifdef HAVE_SYS_TIME_H
#include <sys/time.h>
#endif
#ifdef HAVE_SYS_SELECT_H
#include <sys/select.h>
#endif
#ifdef HAVE_SYS_SOCKET_H
#include <sys/socket.h>
#endif
]
)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T
AC_HEADER_TIME

AC_CHECK_SIZEOF(curl_off_t, ,[
#include <stdio.h>
#include "$srcdir/include/curl/curl.h"
])

AC_CHECK_TYPE(long long,
   [AC_DEFINE(HAVE_LONGLONG, 1, [if your compiler supports 'long long'])])

# check for ssize_t
AC_CHECK_TYPE(ssize_t, ,
   AC_DEFINE(ssize_t, int, [the signed version of size_t]))

TYPE_SOCKLEN_T
TYPE_IN_ADDR_T

AC_FUNC_SELECT_ARGTYPES

dnl Checks for library functions.
dnl AC_PROG_GCC_TRADITIONAL
AC_TYPE_SIGNAL
dnl AC_FUNC_VPRINTF
AC_CHECK_FUNCS( strtoll \
                socket \
                select \
                strdup \
                strstr \
                strtok_r \
                strftime \
                uname \
                strcasecmp \
                stricmp \
                strcmpi \
                gethostbyaddr \
                gettimeofday \
                inet_addr \
                inet_ntoa \
                inet_pton \
                tcsetattr \
                tcgetattr \
                perror \
                closesocket \
                siginterrupt \
                sigaction \
                signal \
                getpass_r \
                strlcat \
                getpwuid \
                geteuid \
                dlopen \
                utime \
                sigsetjmp \
                poll,
dnl if found
[],
dnl if not found, $ac_func is the name we check for
  func="$ac_func"
  AC_MSG_CHECKING([deeper for $func])
  AC_TRY_LINK( [],
               [ $func ();],
               AC_MSG_RESULT(yes!)
               eval "ac_cv_func_$func=yes"
               def=`echo "HAVE_$func" | tr 'a-z' 'A-Z'`
               AC_DEFINE_UNQUOTED($def, 1, [If you have $func]),
               AC_MSG_RESULT(but still no)
               )

)

dnl sigsetjmp() might be a macro and no function so if it isn't found already
dnl we make an extra check here!
if test "$ac_cv_func_sigsetjmp" != "yes"; then
  AC_MSG_CHECKING([for sigsetjmp defined as macro])
  AC_TRY_LINK( [#include <setjmp.h>],
               [sigjmp_buf jmpenv;
                sigsetjmp(jmpenv, 1);],
               AC_MSG_RESULT(yes)
               AC_DEFINE(HAVE_SIGSETJMP, 1, [If you have sigsetjmp]),
               AC_MSG_RESULT(no)
               )
fi

AC_PATH_PROG( PERL, perl, , 
  $PATH:/usr/local/bin/perl:/usr/bin/:/usr/local/bin )
AC_SUBST(PERL)

AC_PATH_PROGS( NROFF, gnroff nroff, , 
  $PATH:/usr/bin/:/usr/local/bin )
AC_SUBST(NROFF)

if test -n "$NROFF"; then
  dnl only check for nroff options if an nroff command was found

  AC_MSG_CHECKING([how to use *nroff to get plain text from man pages])
  MANOPT="-man"
  mancheck=`echo foo | $NROFF $MANOPT 2>/dev/null`
  if test -z "$mancheck"; then
    MANOPT="-mandoc"
   mancheck=`echo foo | $NROFF $MANOPT 2>/dev/null`
    if test -z "$mancheck"; then
      MANOPT=""
      AC_MSG_RESULT([failed])
      AC_MSG_WARN([found no *nroff option to get plaintext from man pages])
    else
      AC_MSG_RESULT([$MANOPT])
    fi
  else
    AC_MSG_RESULT([$MANOPT])
  fi
  AC_SUBST(MANOPT)
fi

if test -z "$MANOPT"
then
  dnl if no nroff tool was found, or no option that could convert man pages
  dnl was found, then disable the built-in manual stuff
  AC_MSG_WARN([disabling built-in manual])
  USE_MANUAL="no";
fi

AC_PROG_YACC

if test -z "$YACC"
then
  AC_MSG_CHECKING([if OK to build without bison/yacc])
  dnl no yacc is a big deal if we have no pre-fixed getdate.y
  if test -r "$srcdir/lib/getdate.c"
  then
    dnl all is well, we don't have to generate it!
    AC_MSG_RESULT(yes)
  else
    AC_MSG_RESULT(no)
    AC_MSG_ERROR([no yacc or bison found, can't build libcurl!])
  fi
fi

dnl *************************************************************************
dnl If the manual variable still is set, then we go with providing a built-in
dnl manual

if test "$USE_MANUAL" = "1"; then
  AC_DEFINE(USE_MANUAL, 1, [If you want to build curl with the built-in manual])
fi

dnl set variable for use in automakefile(s)
AM_CONDITIONAL(USE_MANUAL, test x"$USE_MANUAL" = x1)


dnl AC_PATH_PROG( RANLIB, ranlib, /usr/bin/ranlib, 
dnl   $PATH:/usr/bin/:/usr/local/bin )
dnl AC_SUBST(RANLIB)

dnl ************************************************************
dnl lame option to switch on debug options
dnl
AC_MSG_CHECKING([whether to enable debug options])
AC_ARG_ENABLE(debug,
AC_HELP_STRING([--enable-debug],[Enable pedantic debug options])
AC_HELP_STRING([--disable-debug],[Disable debug options]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       ;;
  *)   AC_MSG_RESULT(yes)

    CPPFLAGS="$CPPFLAGS -DCURLDEBUG"
    CFLAGS="$CFLAGS -g"

    dnl set compiler "debug" options to become more picky, and remove
    dnl optimize options from CFLAGS
    CURL_CC_DEBUG_OPTS
       ;;
  esac
 ],
       AC_MSG_RESULT(no)
)

AC_MSG_CHECKING([whether to enable ares])
AC_ARG_ENABLE(ares,
AC_HELP_STRING([--enable-ares=PATH],[Enable ares for name lookups])
AC_HELP_STRING([--disable-ares],[Disable ares for name lookups]),
[ case "$enableval" in
  no)
       AC_MSG_RESULT(no)
       ;;
  *)   AC_MSG_RESULT(yes)

       if test "x$IPV6_ENABLED" = "x1"; then
         AC_MSG_ERROR([ares doesn't work with ipv6, disable ipv6 to use ares])
       fi

       AC_DEFINE(USE_ARES, 1, [Define if you want to enable ares support])
       dnl substitute HAVE_ARES for curl-config and similar
       HAVE_ARES="1"
       AC_SUBST(HAVE_ARES)

       LIBS="$LIBS -lcares"

       dnl For backwards compatibility default to includes/lib in srcdir/ares
       dnl If a value is specified it is assumed that the libs are in $val/lib
       dnl and the includes are in $val/include. This is the default setup for
       dnl ares so it should not be a problem.
       if test "x$enableval" = "xyes" ; then
         if test -d "$srcdir/ares"; then
            AC_CONFIG_SUBDIRS(ares)
            aresinc=`cd $srcdir/ares && pwd`
            CPPFLAGS="$CPPFLAGS -I$aresinc"

            dnl the pwd= below cannot 'cd' into the ares dir to get the full
            dnl path to it, since it may not exist yet if we build outside of
            dnl the source tree
            pwd=`pwd`
            LDFLAGS="$LDFLAGS -L$pwd/ares"
         fi
       else
         CPPFLAGS="$CPPFLAGS -I$enableval/include"
         LDFLAGS="$LDFLAGS -L$enableval/lib"
       fi
       ;;
  esac ],
       AC_MSG_RESULT(no)
)

AC_CONFIG_FILES([Makefile \
	   docs/Makefile \
           docs/examples/Makefile \
           docs/libcurl/Makefile \
	   include/Makefile \
	   include/curl/Makefile \
	   src/Makefile \
           lib/Makefile \
           tests/Makefile \
           tests/data/Makefile \
           tests/server/Makefile \
           tests/libtest/Makefile \
	   packages/Makefile \
	   packages/Win32/Makefile \
	   packages/Win32/cygwin/Makefile \
	   packages/Linux/Makefile \
	   packages/Linux/RPM/Makefile \
	   packages/Linux/RPM/curl.spec \
	   packages/Linux/RPM/curl-ssl.spec \
           packages/Solaris/Makefile \
           packages/DOS/Makefile \
           packages/EPM/curl.list \
           packages/EPM/Makefile \
           packages/vms/Makefile \
           curl-config
])
AC_OUTPUT
