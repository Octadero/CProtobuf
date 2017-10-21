# CProtobuf

## Using CTensorFlow
Add that dependency to your Package.swift file.
That module makes bridge to libtensorflow library.
```
let package = Package(
    name: "YourProject",
    dependencies: [
        .package(url: "git@github.com:Octadero/CProtobuf.git", from: "3.4.1")
        ]
)
```

## Install protobuff.
You could install protobuf library from package manager (brew or apt) or from sources.

### Install from sources.
Clone and build version related to tensorflow, currently is 3.4.1.

```
git clone https://github.com/google/protobuf.git
git checkout 3.4.x
```

#### Build and Install.
```
cd protobuf
./autogen.sh
./configure
make
make check
sudo make install
```

#### Copy protobuf.pc file (if you don't have) to your pkgconfig folder.
```
sudo cp protobuf.pc /usr/local/lib/pkgconfig/
```

### Brew version
If you install protobuf library on mac os using brew, you must copy `protobuf.pc` file from package or create link.
```
sudo cp /usr/local/Cellar/protobuf/3.4.1/lib/pkgconfig/protobuf.pc /usr/local/lib/pkgconfig/
```
Also you have to remove unacceptable flags (See Troubleshooting).

### Troubleshooting
* At build phase error:
```
warning: error while trying to use pkgConfig flags for CProtobuf: nonWhitelistedFlags("Non whitelisted flags found: [\"-D_THREAD_SAFE\", \"-D_THREAD_SAFE\"] in pc file protobuf")
```
Remove `-D_THREAD_SAFE` keys from file /usr/local/lib/pkgconfig/protobuf.pc

If you use apt or brew package manager, make shure that your `tensorflow.pc` file contains only [whitelisted flags](https://github.com/apple/swift-package-manager/blob/740b6667d8dfbea579927045c038d2d885543316/Sources/PackageLoading/Module%2BPkgConfig.swift#L159).
