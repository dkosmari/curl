# Details about the Wii U port

## Additions

There's a Wii U threading implementation, by defining `USE_THREADS_WIIU`. It borrows the
thread wrappers from `wut`. See `lib/curl_threads.{h,c}` for details.


## Build instructions:

### Compiling

Only the automake build scripts were tested.

    export PORTLIBS_PREFIX=${DEVKITPRO}/portlibs/wiiu

    autoreconf -i

    ./configure \
        --disable-silent-rules \
        --host=powerpc-eabi \
        --enable-wiiu \
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
        --enable-threaded-resolver \
        CFLAGS="-Os -ffunction-sections -fdata-sections"

    make -C lib


### Installing

    make install -C lib
    make install -C include
    make install-binSCRIPTS install-pkgconfigDATA
