# Building with only a Makefile

If only building for native systems, it is possible to significantly reduce the complexity of the build by removing Bazel (and Docker). This simple approach builds only what is needed, removes build-time depenency fetching, increases the speed, and uses upstream Debian packages.

To prepare your system, you'll need the following packages (both available on Debian Bullseye):
```
sudo apt install libabsl-dev libflatbuffers-dev
```

Next, you'll need to clone the [Tensorflow Repo](https://github.com/tensorflow/tensorflow) at the desired checkout (using TF head isn't advised). If you are planning to use libcoral or pycoral libraries, this should match the ones in those repos' WORKSPACE files. For example, if you are using TF2.17.0, we can check that [tag in the TF Repo](https://github.com/tensorflow/tensorflow/commit/ad6d8cc177d0c868982e39e0823d0efbfb95f04c) and then checkout that address:
```
git clone https://github.com/tensorflow/tensorflow
git checkout v2.17.0
```

To build the library:
```
TFROOT=<Directory of Tensorflow> make -j$(nproc) libedgetpu
```
