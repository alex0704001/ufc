#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.
AC_PREREQ([2.59])

#
# Initialize
AC_INIT([ufc], [1.0.0], [280252120@qq.com])
#
# set version information
LIB_MAJOR_VERSION=1
LIB_MINOR_VERSION=0
LIB_MICRO_VERSION=0
VERSION=$LIB_MAJOR_VERSION.$LIB_MINOR_VERSION.$LIB_MICRO_VERSION
VERSION_INFO=`expr $LIB_MAJOR_VERSION + $LIB_MINOR_VERSION`:$LIB_MICRO_VERSION:$LIB_MINOR_VERSION

AC_SUBST(VERSION)
AC_SUBST(VERSION_INFO)
AC_SUBST(LIB_MAJOR_VERSION)
AC_SUBST(LIB_MINOR_VERSION)
AC_SUBST(LIB_MICRO_VERSION)

AC_DEFINE_UNQUOTED([LIB_MAJOR_VERSION],$LIB_MAJOR_VERSION,[Major version])
AC_DEFINE_UNQUOTED([LIB_MINOR_VERSION],$LIB_MINOR_VERSION,[Minor version])
AC_DEFINE_UNQUOTED([LIB_MICRO_VERSION],$LIB_MICRO_VERSION,[Micro version])

AM_INIT_AUTOMAKE
AC_PREFIX_DEFAULT(/usr/local/ufc)
AC_CONFIG_HEADERS([config.h])
AC_HEADER_STDC

AC_ENABLE_SHARED(yes)
AC_ENABLE_STATIC(no)

case `uname -s` in
	Linux)
		UFC_PLATFORM_CPPFLAGS="-D_DEBUG -DDEBUG"
		UFC_PLATFORM_LDFLAGS=""
		;;
	AIX)
		UFC_PLATFORM_CPPFLAGS="-D_DEBUG -DDEBUG -qcpluscmt -qrtti=all"
		UFC_PLATFORM_LDFLAGS="-bnoentry -G -qmkshrobj"
		;;
	*)
		exit 1
		;;
esac
AC_SUBST(UFC_PLATFORM_CPPFLAGS)
AC_SUBST(UFC_PLATFORM_LDFLAGS)

# Checks for programs.
AC_PROG_CC
AC_PROG_CXX
AC_PROG_INSTALL
AC_PROG_RANLIB
AC_PROG_LIBTOOL
LT_INIT

# Checks for library functions.
AC_CHECK_LIB([pthread],[main])
AC_CHECK_LIB([dl],[main])
AC_CHECK_LIB([rt],[main])
AC_CHECK_LIB([m],[main])
AC_CHECK_LIB([gmp],[main])
AC_CHECK_LIB([crypto],[main])

# Checks for header files.
# Checks for typedefs, structures, and compiler characteristics.

AC_ARG_WITH([gmp],
             AC_HELP_STRING([--with-gmp=PATH], [Specify path to GMP installation]),
             [
             	echo "with-gmp: '"$with_gmp"'"
                UFC_GMP_HOME=$withval
                if [ test -d $UFC_GMP_HOME ]; then
                   echo "GMP path installation: '"$UFC_GMP_HOME"' has always been existed."
                else
                   echo "GMP path installation: '"$UFC_GMP_HOME"' does not exists."
                   exit 1
                fi;
             ])
AM_CONDITIONAL([WITH_GMP], [test -d $UFC_GMP_HOME])
AC_SUBST(UFC_GMP_HOME)

AC_ARG_WITH([ssl],
             AC_HELP_STRING([--with-ssl=PATH], [Specify path to OpenSSL installation]),
             [
             	echo "with-ssl: '"$with_ssl"'"
                UFC_OPENSSL_HOME=$withval
                if [ test -d $UFC_OPENSSL_HOME ]; then
                   echo "OpenSSL path installation: '"$UFC_OPENSSL_HOME"' has always been existed."
                else
                   echo "OpenSSL path installation: '"$UFC_OPENSSL_HOME"' does not exists."
                   exit 1
                fi;
             ])
AM_CONDITIONAL([WITH_SSL], [test -d $UFC_OPENSSL_HOME])
AC_SUBST(UFC_OPENSSL_HOME)

#AC_ARG_WITH([curl],
#             AC_HELP_STRING([--with-curl=PATH], [Specify path to CURL installation]),
#             [
#             	echo "with-curl: '"$with_curl"'"
#                UFC_CURL_HOME=$withval
#                if [ test -d $UFC_CURL_HOME ]; then
#                   echo "CURL path installation: '"$UFC_CURL_HOME"' has always been existed."
#                else
#                   echo "CURL path installation: '"$UFC_CURL_HOME"' does not exists."
#                   exit 1
#                fi;
#             ])
#AM_CONDITIONAL([WITH_CURL], [test -d $UFC_CURL_HOME])
#AC_SUBST(UFC_CURL_HOME)

#AC_ARG_WITH([event],
#             AC_HELP_STRING([--with-event=PATH], [Specify path to EVENT installation]),
#             [
#             	echo "with-event: '"$with_event"'"
#                UFC_EVENT_HOME=$withval
#                if [ test -d $UFC_EVENT_HOME ]; then
#                   echo "EVENT path installation: '"$UFC_EVENT_HOME"' has always been existed."
#                else
#                   echo "EVENT path installation: '"$UFC_EVENT_HOME"' does not exists."
#                   exit 1
#                fi;
#             ])
#AM_CONDITIONAL([WITH_EVENT], [test -d $UFC_EVENT_HOME])
#AC_SUBST(UFC_EVENT_HOME)

AC_ARG_ENABLE([imq],
               AC_HELP_STRING([--enable-imq[=PATH]], [Specify path to IBM WebSphere MQ installation]),
               [
               	  echo "Enter IBM WebSphere MQ :"$enable_imq
                  if [ test "x$enable_imq" = "xyes" ]; then
                     enable_imq=/opt/mqm
                     if [ test ! -d $enable_imq ]; then
                        enable_imq=/usr/mqm
                     fi;
                  fi;

               	  UFC_PLUGIN_IMQ_HOME=$enable_imq
                  if [ test -d $UFC_PLUGIN_IMQ_HOME ]; then
                     echo "IBM WebSphere MQ path installation: '"$UFC_PLUGIN_IMQ_HOME"' has always been existed."
                  else
                     echo "IBM WebSphere MQ path installation: '"$UFC_PLUGIN_IMQ_HOME"' does not exists."
                     exit 1
                  fi;

                  UFC_PLUGIN_IMQ_CPPFLAGS="-I$UFC_PLUGIN_IMQ_HOME/inc"
                  if [ test -d $UFC_PLUGIN_IMQ_HOME/lib64 ]; then
                     UFC_PLUGIN_IMQ_LDFLAGS="-L$UFC_PLUGIN_IMQ_HOME/lib64"
                  else
                     UFC_PLUGIN_IMQ_LDFLAGS="-L$UFC_PLUGIN_IMQ_HOME/lib"
                  fi;
                  case `uname -s` in
                  Linux)
                     UFC_PLUGIN_IMQ_LDFLAGS_S="$UFC_PLUGIN_IMQ_LDFLAGS -limqb23gl_r -limqs23gl_r"
                     UFC_PLUGIN_IMQ_LDFLAGS_C="$UFC_PLUGIN_IMQ_LDFLAGS -limqb23gl_r -limqc23gl_r"
                     ;;
                  AIX)
                     UFC_PLUGIN_IMQ_LDFLAGS_S="$UFC_PLUGIN_IMQ_LDFLAGS -limqb23ia_r -limqs23ia_r"
                     UFC_PLUGIN_IMQ_LDFLAGS_C="$UFC_PLUGIN_IMQ_LDFLAGS -limqb23ia_r -limqc23ia_r"
                     ;;
                  *)
                     exit 1
                     ;;
                  esac
               ],
               [enable_imq=no])
AM_CONDITIONAL([ENABLE_IMQ], [test -d $enable_imq])
AC_SUBST(UFC_PLUGIN_IMQ_CPPFLAGS)
AC_SUBST(UFC_PLUGIN_IMQ_LDFLAGS_C)
AC_SUBST(UFC_PLUGIN_IMQ_LDFLAGS_S)

#AC_ARG_ENABLE([tlq],
#               AC_HELP_STRING([--enable-tlq[=PATH]], [Specify path to Oracle installation]),
#               [
#                  if [ test "x$enable_tlq" = "xyes" ]; then
#                  	 enable_tlq=$TLQHOME
#                  fi;
#
#                  UFC_PLUGIN_TLQ_HOME=$enable_tlq
#                  if [ test -d $UFC_PLUGIN_TLQ_HOME ]; then
#                     echo "TongLINK/Q path installation: '"$UFC_PLUGIN_TLQ_HOME"' has always been installed."
#                  else
#                     echo "TongLINK/Q path installation: '"$UFC_PLUGIN_TLQ_HOME"' has not been installed."
#                     exit 1
#                  fi;
#               ],
#              [enable_tlq=no])
#AM_CONDITIONAL([ENABLE_TLQ], [test -d $enable_tlq])
#AC_SUBST(UFC_PLUGIN_TLQ_HOME)

AC_ARG_ENABLE([oracle],
               AC_HELP_STRING([--enable-oracle[=PATH]], [Specify path to Oracle installation]),
               [
                  if [ test "x$enable_oracle" = "xyes" ]; then
                  	 enable_oracle=$ORACLE_HOME
                  fi;

                  UFC_PLUGIN_ORACLE_HOME=$enable_oracle
                  if [ test -d $UFC_PLUGIN_ORACLE_HOME ]; then
                     echo "ORACLE path installation: '"$UFC_PLUGIN_ORACLE_HOME"' has always been installed."
                  else
                     echo "ORACLE path installation: '"$UFC_PLUGIN_ORACLE_HOME"' has not been installed."
                     exit 1
                  fi;
               ],
              [enable_oracle=no])
AM_CONDITIONAL([ENABLE_ORACLE], [test -d $enable_oracle])
AC_SUBST(UFC_PLUGIN_ORACLE_HOME)

AC_ARG_ENABLE([db2],
              AC_HELP_STRING([--enable-db2[=PATH]], [Specify path to DB2 installation]),
              [
                  if [ test "x$enable_db2" = "xyes" ]; then
                     enable_db2=/$DB2INSTANCE/sqllib
                     if [ test ! -d $enable_db2 ]; then
                        enable_db2=/home/$DB2INSTANCE/sqllib
                     fi;
                  fi;

              	  UFC_PLUGIN_DB2_HOME=$enable_db2
                  if [ test -d $UFC_PLUGIN_DB2_HOME ]; then
                     echo "IBM DB2 path installation: '"$UFC_PLUGIN_DB2_HOME"' has always been installed."
                  else
                     echo "IBM DB2 path installation: '"$UFC_PLUGIN_DB2_HOME"' has not been installed."
                     exit 1
                  fi;

                  if [ test -d $UFC_PLUGIN_IMQ_HOME/lib64 ]; then
                     UFC_PLUGIN_DB2_LIBPATH="$UFC_PLUGIN_DB2_HOME/lib64"
                  else
                     UFC_PLUGIN_DB2_LIBPATH="$UFC_PLUGIN_DB2_HOME/lib"
                  fi;
              ],
              [enable_db2=no])
AM_CONDITIONAL([ENABLE_DB2], [test -d $enable_db2])
AC_SUBST(UFC_PLUGIN_DB2_HOME)
AC_SUBST(UFC_PLUGIN_DB2_LIBPATH)

AC_ARG_ENABLE([mysql],
               AC_HELP_STRING([--enable-mysql[=PATH]], [Specify path to MySQL installation]),
               [
                  if [ test "x$enable_mysql" = "xyes" ]; then
                     enable_mysql=/opt/mysql
                  fi;

               	  UFC_PLUGIN_MYSQL_HOME=$enable_mysql
                  if [ test -d $UFC_PLUGIN_MYSQL_HOME ]; then
                     echo "MySQL path installation: '"$UFC_PLUGIN_MYSQL_HOME"' has always been installed."
                  else
                     echo "MySQL path installation: '"$UFC_PLUGIN_MYSQL_HOME"' has not been installed."
                     exit 1
                  fi;
               ],
              [enable_mysql=no])
AM_CONDITIONAL([ENABLE_MYSQL], [test -d $enable_mysql])
AC_SUBST(UFC_PLUGIN_MYSQL_HOME)

AC_ARG_ENABLE([tools],
              AC_HELP_STRING([--enable-tools], [Compiling tools (Default = yes)]),
              [enable_tools=$enableval],
              [enable_tools=no])
AM_CONDITIONAL([ENABLE_TOOLS], [test x$enable_tools = xyes])


# Output Makefile
AC_CONFIG_FILES([Makefile
                 include/ufc/Makefile
                 include/ufc/core/Makefile
                 include/ufc/crypto/Makefile
                 include/ufc/dbo/Makefile
                 include/ufc/imq/Makefile
                 include/ufc/json/Makefile
                 include/ufc/logging/Makefile
                 include/ufc/net/Makefile
                 include/ufc/pkt/Makefile
                 include/ufc/sql/Makefile
                 source/Makefile
                 source/core/Makefile
                 source/core/deelx/Makefile
                 source/core/linenoise/Makefile
                 source/core/utf8/Makefile
                 source/core/zlib/Makefile
                 source/crypto/Makefile
                 source/dbo/Makefile
                 source/imq/Makefile
                 source/json/Makefile
                 source/logging/Makefile
                 source/net/Makefile
                 source/pkt/Makefile
                 source/sql/Makefile
                 plugin/Makefile
                 plugin/ufc.sql.db2/Makefile
                 plugin/ufc.sql.mysql/Makefile
                 plugin/ufc.sql.oracle/Makefile
                 plugin/ufc.imq/Makefile
                 plugin/ufc.nfs.ftp/Makefile
                 plugin/ufc.nfs.sftp/Makefile
                 tools/Makefile])
AC_OUTPUT
