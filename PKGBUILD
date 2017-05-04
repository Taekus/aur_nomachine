# Maintainer: Runnytu < runnytu at gmail dot com >
# OldMaintainer: FreeK <stephan@confidr.me>
# Contributor: olav-st <olav.s.th@gmail.com>
# Contributor: David Manouchehri <manouchehri@riseup.net>

### BUILD OPTIONS
# Set to n to disable nomachine service autostart
_autoservice=y
# Set to n to disable firewall autorules
_autofirewall=y
### END BUILD OPTIONS

pkgname=nomachine
pkgver=5.2.21
pkgrel_i686=1
pkgrel_x86_64=1
pkgrel_armv6h=3
pkgrel_armv7h=1
pkgrel_armv8h=1
pkgrel=1
pkgdesc="Remote desktop application"
groups=('network')
url="http://www.nomachine.com"
license=('custom:"NoMachine EULA"')
arch=('x86_64' 'i686' 'armv6h' 'armv7h' 'armv8h')
options=('!strip')
conflicts=('nxmanager nxwebplayer nxserver nxnode nxclient')
depends=('bash' 'openssh')
sha512sums_x86_64=('66849acbbdcbd4fb5f61319db26a7264a2efd1835a0f449228528c73711e727561b6995acd8b99c100c45cf931af1a7498da441e387db3e50846894cc40aaf3c')
sha512sums_i686=('060480f440cef59df9daa3a053ac915d230325ba3c15f0291164db269159639c1119585654aed6aa060d5afad49ac9f1746f1f22467a5ca192e5a3793dc8e2f6')
sha512sums_armv6h=('2211203d8a0e3ea0f3606dfb4b247afda34947a6d6ac080c0cb0f81eac06d4bc9a7d7c7e762beb10917725332213503dcfb1df42754b03e07e9c4d922b73b77a')
sha512sums_armv7h=('2b408eff94fc6f519931f5d776c99c76490c52c574baa25715eed898794e2bac8311fa105ee011e9472f0b6feaed8d3709d00931d085144c0eca75ea9219aaa8')
sha512sums_armv8h=('3011dc1c91f61e62fb1dfcd9ce16a1568e3c30865db9b27c2845d0f4c85c919d5cc045d48445d3938b1488c74aaaabfe30e40162aaa0359fbd40fa2edabdcee0')
source_x86_64=("http://download.nomachine.com/download/5.2/Linux/${pkgname}_${pkgver}_${pkgrel_x86_64}_x86_64.tar.gz")
source_i686=("http://download.nomachine.com/download/5.2/Linux/${pkgname}_${pkgver}_${pkgrel_i686}_i686.tar.gz")
source_armv6h=("http://download.nomachine.com/download/5.2/Linux/${pkgname}_${pkgver}_${pkgrel_armv6h}_armv6hl.tar.gz")
source_armv7h=("http://download.nomachine.com/download/5.2/Linux/${pkgname}_${pkgver}_${pkgrel_armv7h}_armv7hl.tar.gz")
source_armv8h=("http://download.nomachine.com/download/5.2/Linux/${pkgname}_${pkgver}_${pkgrel_armv8h}_aarch64.tar.gz")
install=nomachine.install

prepare()
{
#Fix Fedora Version Var
tar -zxf $srcdir/NX/etc/NX/server/packages/nxclient.tar.gz NX/scripts/setup/nxclient
sed -i 's/    majorFedoraVersion.*/    majorFedoraVersion=23/' $srcdir/NX/scripts/setup/nxclient
gzip -d $srcdir/NX/etc/NX/server/packages/nxclient.tar.gz
tar -rf $srcdir/NX/etc/NX/server/packages/nxclient.tar NX/scripts/setup/nxclient  -C $srcdir/NX/scripts/setup/nxclient
gzip $srcdir/NX/etc/NX/server/packages/nxclient.tar
rm -fr $srcdir/NX/scripts*
#Change Automatic Service Start And/Or Firewall Automatic Rules If Apply
if [ $_autoservice = y ] && [ $_autofirewall = y ]; then
echo "####################################################################"
echo "#No Changes To Automatic Service Start And Firewall Automatic Rules#"
echo "####################################################################"
else
tar -zxf $srcdir/NX/etc/NX/server/packages/nxserver.tar.gz NX/etc/server-fedora.cfg.sample
if [ $_autoservice = n ] && [ $_autofirewall = n ]; then
sed -i 's/#EnableFirewallConfiguration 1/EnableFirewallConfiguration 0/' NX/etc/server-fedora.cfg.sample
sed -i 's/#StartNXDaemon Automatic/StartNXDaemon Manual/' NX/etc/server-fedora.cfg.sample
elif [ $_autoservice = y ] && [ $_autofirewall = n ]; then
sed -i 's/#EnableFirewallConfiguration 1/EnableFirewallConfiguration 0/' NX/etc/server-fedora.cfg.sample
elif [ $_autoservice = n ] && [ $_autofirewall = y ]; then
sed -i 's/#StartNXDaemon Automatic/StartNXDaemon Manual/' NX/etc/server-fedora.cfg.sample
fi
gzip -d $srcdir/NX/etc/NX/server/packages/nxserver.tar.gz
tar -rf $srcdir/NX/etc/NX/server/packages/nxserver.tar NX/etc/server-fedora.cfg.sample -C $srcdir/NX/etc/server-fedora.cfg.sample
gzip $srcdir/NX/etc/NX/server/packages/nxserver.tar
rm -fr $srcdir/NX/etc/server-fedora.cfg.sample
fi
}

package()
{
cd "$srcdir"
mkdir "$srcdir/NX/etc" -p
install -d "$pkgdir/usr/"
cp -a NX "$pkgdir/usr/NX"
}

