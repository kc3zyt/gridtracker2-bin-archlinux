# Maintainer: you
pkgname=gridtracker2-bin
pkgver=0            # overwritten below
pkgrel=1
pkgdesc="GridTracker (repackaged upstream binary)"
arch=('x86_64')
url="https://gridtracker.org"
license=('BSD-3-Clause')
options=('!strip' '!debug')

# Scrape the download page at source time
_page="https://gridtracker.org/index.php/downloads/gridtracker-downloads"
_url=$(curl -sL "$_page" | grep -oP 'https?://[^"'\'' ]+x64\.pacman' | head -n1)
_file=${_url##*/}

# Derive version from the filename (adjust the sed to match its naming)
_ver=${_file#*-}        # strip "GridTracker2-"
pkgver=${_ver%-x64.pacman}

source=("$_file::$_url")
noextract=("$_file")        # makepkg doesn't know .pacman; we extract manually
sha256sums=('SKIP')

package() {
    bsdtar -xpf "$srcdir/$_file" -C "$pkgdir" \
    --exclude='.PKGINFO' --exclude='.MTREE' \
    --exclude='.BUILDINFO' --exclude='.INSTALL' --exclude='.CHANGELOG'
}
