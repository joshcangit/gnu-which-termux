# gnu-which-termux
Latest release can be downloaded with this script.

```bash
url="https://carlowood.github.io/which/"
if command -v curl > /dev/null; then
	cmd="curl -Ls"
	download="curl -o"
elif command -v wget > /dev/null; then
	cmd="wget -qO-"
	download="wget -O"
fi
file="$($cmd $url | xmllint --html --xpath 'string(/html/body/li[1]/a/@href)' - 2>&0)"
download_url="${url}${file}"
$download $file $download_url
tar -axf $file
cd which-*/
```

Built using the commands below.

Use `strip` to remove unneeded symbols.

```shell
./configure --prefix=$PREFIX
make -j$(nproc)
strip --strip-unneeded -o which.gnu which
```

Package version info

debianutils 5.7-1

> Modified to work with `gnu-which`.

gnu-which 2.21

> For use with modified `debianutils`.

gnu-which 2.21~a

> Works with the current `debianutils` in Termux.

To package into a _deb_, use `dpkg-deb --root-owner-group --build` on a folder.
