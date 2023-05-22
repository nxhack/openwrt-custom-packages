# OpenWrt Custom Packages

## Description

OpenWrt Custom Packages : for OpenWrt-23.05

Note: support arches are aarch64, arm, x86_64

## Eclipse Mraa (Libmraa) and UPM, which supports the latest node.js.

If you want to replace the OpenWrt community packages, follow the steps below.

Add the following line to feeds.conf or feeds.conf.default.
```
src-git custom https://github.com/nxhack/openwrt-custom-packages.git;openwrt-23.05
```

Run
```
./scripts/feeds update custom
rm ./package/feeds/packages/swig
rm ./package/feeds/packages/libmraa
rm ./package/feeds/packages/libupm
./scripts/feeds install -a -p custom
make defconfig
```

## License

See [LICENSE](LICENSE) file.
