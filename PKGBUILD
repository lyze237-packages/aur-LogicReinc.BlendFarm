# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
_name=LogicReinc.BlendFarm
pkgname=("logicreinc.blendfarm" "logicreinc.blendfarm.server")
pkgver=1.1.6
_hash=915b0746f05d10ddac85b442eeda80cc3d1e5b57
pkgrel=1
pkgdesc="A stand-alone Blender Network Renderer"
arch=("x86_64")
url="https://github.com/lyze237-forks/LogicReinc.BlendFarm"
license=('GPL-3.0')
depends=("icu")
makedepends=("dotnet-sdk-6.0")
options=("!debug" "!strip")
source=("$url/archive/$_hash.tar.gz")
sha256sums=("0f0f33c9bc1c460ead9bc007c9f62c5a91d4d7bf6628f2f553788b22d862e40e")

build() {
	cd "$_name-$_hash/$_name"

	MSBUILDDISABLENODEREUSE=1 DOTNET_CLI_TELEMETRY_OPTOUT=1 dotnet publish \
		--configuration Release \
		--self-contained true \
		--runtime linux-x64 \
		-p:PublishSingleFile=true \
		--self-contained \
		--output ../out/client \
		./LogicReinc.BlendFarm.csproj

	cd "../$_name.Server"

	MSBUILDDISABLENODEREUSE=1 DOTNET_CLI_TELEMETRY_OPTOUT=1 dotnet publish \
		--configuration Release \
		--self-contained true \
		--runtime linux-x64 \
		-p:PublishSingleFile=true \
		--self-contained \
		--output ../out/server \
		./LogicReinc.BlendFarm.Server.csproj
}

package_logicreinc.blendfarm.server() {
	install -d $pkgdir/usr/{bin,lib}

	cd "$_name-$_hash/out/server"

	install -Dm755 -t "$pkgdir/usr/lib/$pkgname" LogicReinc.BlendFarm.Server LogicReinc.BlendFarm.Server.pdb LogicReinc.BlendFarm.Shared.pdb peek.py
	ln -s "/usr/lib/$pkgname/$_name.Server" "$pkgdir/usr/bin/$pkgname"
}

package_logicreinc.blendfarm() {
	install -d $pkgdir/usr/{bin,lib}

	cd "$_name-$_hash/out/client"

	install -Dm755 -t "$pkgdir/usr/lib/$pkgname" libHarfBuzzSharp.so libSkiaSharp.so LogicReinc.BlendFarm LogicReinc.BlendFarm.Client.pdb LogicReinc.BlendFarm.pdb LogicReinc.BlendFarm.Shared.pdb peek.py
	install -Dm755 -t "$pkgdir/usr/lib/$pkgname/Images" Images/LogicReinc.BlendFarm.icns Images/render.ico
	ln -s "/usr/lib/$pkgname/$_name" "$pkgdir/usr/bin/$pkgname"
}
