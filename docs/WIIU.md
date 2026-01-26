# Details about the Wii U port

## Changes from upstream

Currently a patch is needed for WUT 1.9.0 to support `fcntl(..., F_SETFD, FD_CLOEXEC)`

The libcurl.pc script was tweaked to reduce the amount of duplicated flags.


## Build instructions:

### Compiling

Only the automake build system was tested.

    source "${DEVKITPRO}/wiiuvars.sh"

    autoreconf -i

    ./configure \
        --disable-silent-rules \
        --host=powerpc-eabi \
        --prefix=${PORTLIBS_PREFIX} \
        --disable-shared \
        --disable-ipv6 \
        --disable-unix-sockets \
        --disable-socketpair \
        --disable-manual \
        --with-mbedtls=${PORTLIBS_PREFIX} \
        --with-ca-path=/vol/storage_mlc01/sys/title/0005001b/10054000/content/scerts \
        --without-libpsl \
        --enable-websockets \
        --enable-verbose \
        --disable-docs \
        --enable-threaded-resolver

    make -C lib


### Installing

    make install -C lib
    make install -C include
    make install-binSCRIPTS install-pkgconfigDATA
