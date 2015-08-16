# Maintainer: GordonGR <ntheo1979@gmail.com>
# Contributor: mikers <mikeonthecomputer@gmail.com>
# Contributor: Splex


pkgname=kokua-opensimulator
pkgver=3.7.81.33408
_pkgver=3_7_81_33408
_pkgprever=3.7.81
pkgrel=2
pkgdesc="An Open Source third party viewer for Open Simulator (opensim), only."
url="http://www.kokuaviewer.org"
license=('GPL')
arch=('i686' 'x86_64')
depends=('apr-util' 'gtk2' 'libgl' 'libidn' 'libjpeg-turbo' 'mesa' 'nss' 'sdl' 'glu' 'pangox-compat')
optdepends=('libpulse: for PulseAudio support' 'alsa-lib: for ALSA support' 'nvidia-utils: for NVIDIA support' 'flashplugin: for inworld Flash support' 'gstreamer0.10: for video support, may need good, bad and ugly plugins' 'lib32-freealut: for OpenAL support')

if [ "$CARCH" = "i686" ]; then
source=("http://sourceforge.net/projects/kokua.team-purple.p/files/Kokua-OpenSim-${_pkgprever}/Kokua_OpenSim_Release_${_pkgver}_${CARCH}.tar.bz2"
		'kokua-opensimulator.desktop'
		'kokua-opensimulator.launcher')
md5sums=('242fe670a23863c6cd62a09f7e74ecb7'
         'c1f20863e4e980b93771e33f442277c8'
         '97be394f1e12071401f45e3653bb4559')
        
elif [ "$CARCH" = "x86_64" ]; then
source=("http://sourceforge.net/projects/kokua.team-purple.p/files/Kokua-OpenSim-${_pkgprever}/Kokua_OpenSim_Release_64_${_pkgver}_${CARCH}.tar.bz2"
		'kokua-opensimulator.desktop'
		'kokua-opensimulator.launcher')
md5sums=('b7223eddb88a0a13cf82e1402cc9f7a9'
         'c1f20863e4e980b93771e33f442277c8'
         '97be394f1e12071401f45e3653bb4559')
fi


package() {
cd $srcdir
  
# Rename Data Directory
if [ "$CARCH" = "i686" ]; then
mv Kokua_OpenSim_Release_${_pkgver}_$CARCH kokua-opensimulator
elif [ "$CARCH" = "x86_64" ]; then
mv Kokua_OpenSim_Release_64_${_pkgver}_$CARCH kokua-opensimulator
fi

# Install Desktop File
install -D -m644 $srcdir/kokua-opensimulator.desktop \
  $pkgdir/usr/share/applications/kokua-opensimulator.desktop

# Install Icon File
install -D -m644 $srcdir/kokua-opensimulator/kokua_icon.png \
  $pkgdir/usr/share/pixmaps/kokua-opensimulator.png

# Install Launcher
install -D -m755 $srcdir/kokua-opensimulator.launcher \
  $pkgdir/usr/bin/kokua-opensimulator

# Move Data to Destination Directory
install -d $pkgdir/opt
mv kokua-opensimulator $pkgdir/opt/

# Change Permissions of files to root:games
chown -R root:games $pkgdir/opt/kokua-opensimulator
chmod -R g+rw $pkgdir/opt/kokua-opensimulator

# Make Binary Group-Executable
chmod g+x $pkgdir/opt/kokua-opensimulator/kokua

# Do not re-register the application with the desktop system at every launch, saves from locally installed desktop files.
sed -i 's|./etc/refresh_desktop_app_entry.sh|#./etc/refresh_desktop_app_entry.sh|' $pkgdir/opt/kokua-opensimulator/kokua
  
}