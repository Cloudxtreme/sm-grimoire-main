# DEBUG=-DNDEBUG is needed to get the spell compiling
# However the variable must not be exported otherwise
# Sorcery will create a /-DNDEBUG file at the end of install

OPTS="DEBUG=-DNDEBUG \
  --libexecdir=$DEFAULT_ROOT/usr/lib \
  --sbindir=$DEFAULT_ROOT/sbin \
  $OPTS" &&

OPTIMIZER=$CFLAGS make_single &&
default_build &&
make_normal
