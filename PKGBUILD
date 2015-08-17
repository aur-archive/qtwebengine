# Maintainer: Stefan Damm <autama at nurfuerspam.de>
 
pkgname=qtwebengine
pkgver=1
pkgrel=4
pkgdesc="A Chromium integration for Qt. (GIT version)"
arch=('x86_64' 'i686')
url="http://qt-project.org/wiki/QtWebEngine"
license=('custom')
makedepends=('elfutils' 'gperf' 'mesa' 'perl-json' 'python2-jinja' 'python2-ply' 'python2-simplejson' 'yasm' 'git' 'openssh' 're2c')
depends=('qt5-declarative' 'udev' 'cairo' 'nss' 'pciutils' 'minizip' 'snappy' 'speex' 'libevent' 'opus' 're2' 'harfbuzz-icu' 'jsoncpp' 'libxslt')
provides=('libwebrtc' 'qtwebengine')
source=('git://gitorious.org/qt-labs/qtwebengine.git'
'git://gitorious.org/qt-labs/chromium.git'
'jinja_1.patch'
'http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-client/chromium/files/chromium-gpsd-r0.patch'
'http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-client/chromium/files/chromium-system-icu-r0.patch')
md5sums=('SKIP'
'SKIP'
'12009cde409c4a89edb68445ba4dbb15'
'59e2c59702c84e64628cd7b6fac6c875'
'bf96b0666d26cdd172575cab0772a4d3')
_gitname=qtwebengine
 
# Are we in Gnome?
_use_gnome=0
if [ -f /usr/lib/libgnome-keyring.so ]; then
depends+=('libgnome-keyring' )
_use_gnome=1
fi
 
# Use Pulseaudio?
_use_pulseaudio=0
if [ -x /usr/bin/pulseaudio ]; then
depends+=('libpulse')
_use_pulseaudio=1
fi
 
# Google API keys (see http://www.chromium.org/developers/how-tos/api-keys)
# Note: These are for Arch Linux use ONLY. For your own distribution, please
# get your own set of keys. Feel free to contact foutrelis@archlinux.org for
# more information.
_google_api_key="AIzaSyDwr302FpOSkGRpLlUpPThNTDPbXcIn_FM"
_google_default_client_id="413772536636.apps.googleusercontent.com"
_google_default_client_secret="0ZChLK6AxeA3Isu96MkwqDR4"
 
[ "${CARCH}" = "i686" ] && _target_arch='ia32'
[ "${CARCH}" = "x86_64" ] && _target_arch='x64'
 
prepare() {
cd "${_gitname}"
 
msg2 "Init submodules"
git submodule init
git config submodule.3rdparty.url ${srcdir}/chromium
git submodule update
 
msg2 "Remove unnecesary components to save space"
find src/3rdparty/chromium/third_party -type f \! -iname '*.gyp*' \
\! -path 'src/3rdparty/chromium/third_party/WebKit/*' \
\! -path 'src/3rdparty/chromium/third_party/angle/*' \
\! -path 'src/3rdparty/chromium/third_party/angle_dx11/*' \
\! -path 'src/3rdparty/chromium/third_party/cacheinvalidation/*' \
\! -path 'src/3rdparty/chromium/third_party/cld/*' \
\! -path 'src/3rdparty/chromium/third_party/cros_system_api/*' \
\! -path 'src/3rdparty/chromium/third_party/ffmpeg/*' \
\! -path 'src/3rdparty/chromium/third_party/flot/*' \
\! -path 'src/3rdparty/chromium/third_party/freetype2/*' \
\! -path 'src/3rdparty/chromium/third_party/gold/*' \
\! -path 'src/3rdparty/chromium/third_party/hunspell/*' \
\! -path 'src/3rdparty/chromium/third_party/iccjpeg/*' \
\! -path 'src/3rdparty/chromium/third_party/icu/*' \
\! -path 'src/3rdparty/chromium/third_party/jstemplate/*' \
\! -path 'src/3rdparty/chromium/third_party/khronos/*' \
\! -path 'src/3rdparty/chromium/third_party/leveldatabase/*' \
\! -path 'src/3rdparty/chromium/third_party/libXNVCtrl/*' \
\! -path 'src/3rdparty/chromium/third_party/libjingle/*' \
\! -path 'src/3rdparty/chromium/third_party/libjpeg_turbo/*' \
\! -path 'src/3rdparty/chromium/third_party/libphonenumber/*' \
\! -path 'src/3rdparty/chromium/third_party/libsrtp/*' \
\! -path 'src/3rdparty/chromium/third_party/libxml/chromium/*' \
\! -path 'src/3rdparty/chromium/third_party/libusb/*' \
\! -path 'src/3rdparty/chromium/third_party/libvpx/*' \
\! -path 'src/3rdparty/chromium/third_party/libwebp/*' \
\! -path 'src/3rdparty/chromium/third_party/libyuv/*' \
\! -path 'src/3rdparty/chromium/third_party/lss/*' \
\! -path 'src/3rdparty/chromium/third_party/lzma_sdk/*' \
\! -path 'src/3rdparty/chromium/third_party/mesa/*' \
\! -path 'src/3rdparty/chromium/third_party/modp_b64/*' \
\! -path 'src/3rdparty/chromium/third_party/mongoose/*' \
\! -path 'src/3rdparty/chromium/third_party/mt19937ar/*' \
\! -path 'src/3rdparty/chromium/third_party/npapi/*' \
\! -path 'src/3rdparty/chromium/third_party/openssl/*' \
\! -path 'src/3rdparty/chromium/third_party/ots/*' \
\! -path 'src/3rdparty/chromium/third_party/protobuf/*' \
\! -path 'src/3rdparty/chromium/third_party/pywebsocket/*' \
\! -path 'src/3rdparty/chromium/third_party/ply/*' \
\! -path 'src/3rdparty/chromium/third_party/qcms/*' \
\! -path 'src/3rdparty/chromium/third_party/re2/*' \
\! -path 'src/3rdparty/chromium/third_party/sfntly/*' \
\! -path 'src/3rdparty/chromium/third_party/skia/*' \
\! -path 'src/3rdparty/chromium/third_party/smhasher/*' \
\! -path 'src/3rdparty/chromium/third_party/sqlite/*' \
\! -path 'src/3rdparty/chromium/third_party/tcmalloc/*' \
\! -path 'src/3rdparty/chromium/third_party/tlslite/*' \
\! -path 'src/3rdparty/chromium/third_party/trace-viewer/*' \
\! -path 'src/3rdparty/chromium/third_party/undoview/*' \
\! -path 'src/3rdparty/chromium/third_party/usrsctp/*' \
\! -path 'src/3rdparty/chromium/third_party/webdriver/*' \
\! -path 'src/3rdparty/chromium/third_party/webrtc/*' \
\! -path 'src/3rdparty/chromium/third_party/widevine/*' \
\! -path 'src/3rdparty/chromium/third_party/x86inc/*' \
\! -path 'src/3rdparty/chromium/third_party/yasm/*' \
\! -path 'src/3rdparty/chromium/third_party/zlib/google*' \
-delete
 
msg2 "Fix to really use python2."
rm -rf "${srcdir}/python"
mkdir "${srcdir}/python"
ln -s /usr/bin/python2 "${srcdir}/python/python"
export PATH="${srcdir}/python":$PATH
 
msg2 "Patch Files"
patch -p0 -d "${srcdir}/qtwebengine/src/3rdparty/chromium" -i "${srcdir}/chromium-gpsd-r0.patch"
patch -p1 -d "${srcdir}" -i "${srcdir}/jinja_1.patch"
patch -p0 -d "${srcdir}/qtwebengine/src/3rdparty/chromium" -i "${srcdir}/chromium-system-icu-r0.patch"
# Make it possible to remove third_party/adobe
echo > "${srcdir}/flapper_version.h"
}
 
build() {
cd "${_gitname}"
# Silence "typedef 'x' locally defined but not used" warnings
CFLAGS+=' -Wno-unused-local-typedefs'
 
# NOTES:
# enable_sql_database=0 | http://crbug.com/22208
# logging_like_official_build=1 | Save space by removing DLOG and DCHECK messages (about 6% reduction).
# linux_use_gold_flags=0 | Never use bundled gold binary. Disable gold linker flags for now.
# usb_ids_path=/usr/share/hwdata/usb.ids | Use the file at run time instead of effectively compiling it in.
# linux_use_tcmalloc=0 | https://bugs.gentoo.org/show_bug.cgi?id=413637
 
local _flags=""
 
_flags+="disable_glibc=1
disable_sse2=1
flapper_version_h_file="${srcdir}/flapper_version.h"
google_api_key="${_google_api_key}"
google_default_client_id="${_google_default_client_id}"
google_default_client_secret="${_google_default_client_secret}"
linux_link_gnome_keyring="${_use_gnome}"
linux_link_gsettings=1
linux_link_libpci=1
linux_link_pulseaudio="${_use_pulseaudio}"
linux_strip_binary=1
linux_use_gold_binary=0
linux_use_gold_flags=0
linux_use_tcmalloc=0
logging_like_official_build=1
no_strict_aliasing=1
python_ver=2.7
remove_webcore_debug_symbols=1
target_arch="${_target_arch}"
usb_ids_path=/usr/share/hwdata/usb.ids
use_gconf=0
use_gnome_keyring="${_use_gnome}"
use_pulseaudio="${_use_pulseaudio}"
werror="
 
# TODO
# -Duse_system_hunspell=1 | upstream changes needed
# -Duse_system_libsrtp=1 | https://bugs.gentoo.org/show_bug.cgi?id=459932
# -Duse_system_libusb=1 | http://crbug.com/266149
# -Duse_system_libvpx | https://bugs.gentoo.org/show_bug.cgi?id=487926
# -Duse_system_libwebp=1 | http://crbug.com/288019
# -Duse_system_ssl=1 | http://crbug.com/58087
# -Duse_system_sqlite=1 | http://crbug.com/22208
local _replaced_system_libs=""
_replaced_system_libs="-Duse_system_bzip2=1
-Duse_system_expat=1
-Duse_system_flac=1
-Duse_system_harfbuzz=1
-Duse_system_icu=1
-Duse_system_jsoncpp=1
-Duse_system_libevent=1
-Duse_system_libjpeg=1
-Duse_system_libpng=1
-Duse_system_libsrtp=0
-Duse_system_libusb=0
-Duse_system_libvpx=0
-Duse_system_libwebp=0
-Duse_system_libxml=1
-Duse_system_libxslt=1
-Duse_system_mesa=1
-Duse_system_minizip=1
-Duse_system_nspr=1
-Duse_system_openssl=1
-Duse_system_opus=1
-Duse_system_protobuf=1
-Duse_system_re2=1
-Duse_system_snappy=1
-Duse_system_speex=1
-Duse_system_sqlite=0
-Duse_system_ssl=0
-Duse_system_v8=0
-Duse_system_xdg_utils=1
-Duse_system_yasm=1
-Duse_system_zlib=1"
src/3rdparty/chromium/build/linux/unbundle/replace_gyp_files.py ${_replaced_system_libs}
 
_replaced_system_libs=$(cat ${_replaced_system_libs} | sed 's|-D||g')
 
export GYP_DEFINES="${_flags} ${_replaced_system_libs}"
 
qmake
make
}
 
package() {
cd "${_gitname}"
make INSTALL_ROOT="${pkgdir}" install
}
