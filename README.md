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
```

Built using the commands below.

Use `strip` to remove unneeded symbols.

```shell
cd which-*/
./configure --prefix=$PREFIX
make -j$(nproc)
strip --strip-unneeded which
cd ..
```

To package into a _deb_, use `dpkg-deb --root-owner-group --build` on a folder.
