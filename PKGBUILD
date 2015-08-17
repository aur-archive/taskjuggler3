# Maintainer: alucryd <alucryd at gmail dot com>
# Contributor: Mathieu Clabaut <mathieu dot clabaut at gmail dot com>

pkgname=taskjuggler3
pkgver=3.5.0
pkgrel=4
pkgdesc="Project Management Software"
arch=('any')
url="http://www.taskjuggler.org"
license=('GPL')
depends=('ruby-mail>=2.4.3' 'ruby-term-ansicolor>=1.0.7')
source=("http://rubygems.org/downloads/${pkgname%3}-${pkgver}.gem"
        'tj-system-dirs.patch')
noextract=("${pkgname%3}-${pkgver}.gem")
sha256sums=('42f2e81470be9b2486fc074ba6ff04180258f462fed5c46cba871b7518cd0465'
            '8174f62598b4230df033feb213e5ec25bc6d3105c71455a88514eaff3db0410a')

prepare() {
  gem install --no-{document,user-install} --ignore-dependencies -i . ${pkgname%3}-${pkgver}.gem

  cd gems/${pkgname%3}-${pkgver}
  patch -Np1 -i ../../tj-system-dirs.patch
}

package() {
  cd gems/${pkgname%3}-${pkgver}

  local _rubyver="$(ruby --version | sed 's/.* \(.*\..*\..*\)p.*/\1/')"

  install -dm 755 "${pkgdir}"/usr/{lib/ruby/{gems/${_rubyver},vendor_ruby},share/{doc,vim/vimfiles/syntax}}
  mv bin "${pkgdir}"/usr/
  mv lib "${pkgdir}"/usr/lib/ruby/vendor_ruby/${_rubyver}

# Gem compatibility
  mv ../../specifications "${pkgdir}"/usr/lib/ruby/gems/${_rubyver}/

# Vim syntax
  mv data/tjp.vim "${pkgdir}"/usr/share/vim/vimfiles/syntax/

# Data
  mv data "${pkgdir}"/usr/share/${pkgname%3}
  mv examples "${pkgdir}"/usr/share/${pkgname%3}/

# Documentation
  mv manual "${pkgdir}"/usr/share/doc/${pkgname%3}
}

# vim: ts=2 sw=2 et:
