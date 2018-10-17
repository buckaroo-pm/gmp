genrule(
  name = 'make', 
  out = 'out', 
  srcs = [
    '.bootstrap', 
  ] + glob([
    'cxx/**/*.am', 
    'cxx/**/*.cc', 
    'demos/**/*.am', 
    'demos/**/*.in', 
    'demos/**/*.h', 
    'demos/**/*.c', 
    'demos/**/*.y', 
    'demos/**/*.l', 
    'doc/**/*', 
    'mpf/**/*.am', 
    'mpf/**/*.h', 
    'mpf/**/*.c', 
    'mpn/**/*.m4', 
    'mpn/**/*.am', 
    'mpn/**/*.asm', 
    'mpn/**/*.h', 
    'mpn/**/*.c', 
    'mpn/m4-ccas', 
    'mpq/**/*.am', 
    'mpq/**/*.h', 
    'mpq/**/*.c', 
    'mpz/**/*.am', 
    'mpz/**/*.h', 
    'mpz/**/*.c', 
    'mini-gmp/**/*.h', 
    'mini-gmp/**/*.c', 
    'printf/**/*.h', 
    'printf/**/*.c', 
    'printf/**/*.am', 
    'rand/**/*.am', 
    'rand/**/*.h', 
    'rand/**/*.c', 
    'scanf/**/*.h', 
    'scanf/**/*.c', 
    'scanf/**/*.am', 
    'tests/**/*.h', 
    'tests/**/*.c', 
    'tests/**/*.cc', 
    'tests/**/*.am', 
    'tests/**/*.asm', 
    'tests/**/*.pl', 
    'tune/**/*.am', 
    'tune/**/*.h', 
    'tune/**/*.c', 
    'tune/**/*.asm', 
    'tune/**/*.pl', 
    'ChangeLog', 
    'COPYING*', 
    'install-sh', 
    'missing', 
    'AUTHORS', 
    'INSTALL', 
    'NEWS', 
    'README', 
    '*.h', 
    '*.c', 
    '*.ac', 
    '*.autoconf', 
    '*.am', 
    '*.in', 
    '*.guess', 
    '*.m4', 
    '*.sub', 
    '*.status', 
    '*.txt', 
  ]), 
  cmd = ' && '.join([
    'mkdir -p $OUT', 
    'cp -r $SRCDIR/. $TMP', 
    'cd $TMP', 
    'chmod +x ./.bootstrap', 
    'chmod +x ./mpn/m4-ccas', 
    './.bootstrap', 
    './configure --prefix=$OUT', 
    'make -j4', 
    'make check', 
    'make install', 
  ]), 
)

genrule(
  name = 'gmp-h', 
  out = 'gmp.h', 
  cmd = 'cp $(location :make)/include/gmp.h $OUT', 
)

genrule(
  name = 'gmp-static-linux', 
  out = 'libgmp.a', 
  cmd = 'cp $(location :make)/lib/libgmp.a $OUT', 
)

genrule(
  name = 'gmp-shared-linux', 
  out = 'libgmp.so', 
  cmd = 'cp $(location :make)/lib/libgmp.so $OUT', 
)

prebuilt_cxx_library(
  name = 'gmp', 
  header_namespace = '', 
  exported_headers = {
    'gmp.h': ':gmp-h', 
  }, 
  platform_static_lib = [
    ('^linux.*', ':gmp-shared-linux'),
  ], 
  platform_shared_lib = [
    ('^linux.*', ':gmp-shared-linux'),
  ], 
  preferred_linkage = 'static', 
  visibility = [
    'PUBLIC', 
  ], 
)

cxx_binary(
  name = 'primes', 
  header_namespace = '', 
  headers = [
    'demos/primes.h', 
  ], 
  srcs = [
    'demos/primes.c', 
  ], 
  deps = [
    '//:gmp', 
  ], 
)
