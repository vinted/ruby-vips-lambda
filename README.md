
# Ruby Libvips Lambda Layer

<a href="https://github.com/customink/lamby"><img src="https://user-images.githubusercontent.com/2381/59363668-89edeb80-8d03-11e9-9985-2ce14361b7e3.png" alt="Lamby: Simple Rails & AWS Lambda Integration using Rack." align="right" width="300" /></a>Are you using the [ruby-vips](https://github.com/libvips/ruby-vips) or [image_processing](https://github.com/janko/image_processing) gems with a Lambda microservice? Maybe you are using [Lamby](https://github.com/customink/lamby) to deploy your entire Rails application to AWS Lambda with its simple Rack integration? If yes to any of the above, this [Lambda Layer](https://aws.amazon.com/blogs/compute/working-with-aws-lambda-and-lambda-layers-in-aws-sam/) is just for you.

**[Lamby: Simple Rails & AWS Lambda Integration using Rack.](https://github.com/customink/lamby)**

## Usage

Ensure you have both Docker installed and your AWS CLI configured. After you clone this repository, please run:

```shell
$ ./bin/deploy
```

This will call `./bin/build` for you and push your built Lambda Layer to your own account. Use the ARN in the script's output within your [AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-layers.html) `template.yaml` file. If needed you can use the `AWS_PROFILE` environment variable to control which CLI account is used.

## Ruby 2.7 or 2.5?

The master branch of this repo is targeted for the Ruby 2.7 runtime which is Amazon Linux 2. Most all dependencies needed for `libvips` have to be installed and packaged. Please use the [ruby25](https://github.com/customink/ruby-vips-lambda/tree/ruby25) branch which is Amazon Linux 1 if you use the ruby2.5 runtime.

## Methodology

Simplicity and small file size! We followed the [docs](https://libvips.github.io/libvips/install.html) for `libvips` install. Our build script uses `lambci/lambda:build-ruby2.7` Docker image from the [docker-lambda](https://github.com/lambci/docker-lambda) project as our build environment. All build commands are located in the `Dockerfile` which install all the dependencies for libvips in the `/opt` directory. This includes common file format openers and savers as well as libs that ensure libvips is fast. The current version built is `8.10.0` and easy to configure by providing the `VIPS_VERSION` environment variable during the build or deploy script. 

## Contents

Current size of the layer's un-compressed contents is around `28MB` in size. Contents include:

```shell
$ ls -lAGp /opt/lib
drwxr-xr-x 3 root    4096 May 31 16:05 cmake/
drwxr-xr-x 2 root    4096 May 31 16:11 girepository-1.0/
-rw-r--r-- 1 root  441838 May 31 16:00 libexpat.a
-rwxr-xr-x 1 root     920 May 31 16:00 libexpat.la
lrwxrwxrwx 1 root      18 May 31 16:00 libexpat.so -> libexpat.so.1.6.11
lrwxrwxrwx 1 root      18 May 31 16:00 libexpat.so.1 -> libexpat.so.1.6.11
-rwxr-xr-x 1 root  231496 May 31 16:00 libexpat.so.1.6.11
-rwxr-xr-x 1 root     926 May 31 16:05 libfftw3.la
lrwxrwxrwx 1 root      17 May 31 16:05 libfftw3.so -> libfftw3.so.3.5.8
lrwxrwxrwx 1 root      17 May 31 16:05 libfftw3.so.3 -> libfftw3.so.3.5.8
-rwxr-xr-x 1 root 2327176 May 31 16:05 libfftw3.so.3.5.8
-rwxr-xr-x 1 root    1004 May 31 16:05 libfftw3_threads.la
lrwxrwxrwx 1 root      25 May 31 16:05 libfftw3_threads.so -> libfftw3_threads.so.3.5.8
lrwxrwxrwx 1 root      25 May 31 16:05 libfftw3_threads.so.3 -> libfftw3_threads.so.3.5.8
-rwxr-xr-x 1 root   33968 May 31 16:05 libfftw3_threads.so.3.5.8
-rw-r--r-- 1 root   45562 May 31 16:00 libgif.a
lrwxrwxrwx 1 root      11 May 31 16:00 libgif.so -> libgif.so.7
lrwxrwxrwx 1 root      15 May 31 16:00 libgif.so.7 -> libgif.so.7.2.0
-rwxr-xr-x 1 root   36568 May 31 16:00 libgif.so.7.2.0
-rw-r--r-- 1 root   80414 May 31 16:02 libimagequant.a
lrwxrwxrwx 1 root      18 May 31 16:02 libimagequant.so -> libimagequant.so.0
-rw-r--r-- 1 root   62432 May 31 16:02 libimagequant.so.0
-rwxr-xr-x 1 root     956 May 31 16:05 liborc-0.4.la
lrwxrwxrwx 1 root      20 May 31 16:05 liborc-0.4.so -> liborc-0.4.so.0.25.0
lrwxrwxrwx 1 root      20 May 31 16:05 liborc-0.4.so.0 -> liborc-0.4.so.0.25.0
-rwxr-xr-x 1 root  797976 May 31 16:05 liborc-0.4.so.0.25.0
-rwxr-xr-x 1 root    1009 May 31 16:05 liborc-test-0.4.la
lrwxrwxrwx 1 root      25 May 31 16:05 liborc-test-0.4.so -> liborc-test-0.4.so.0.25.0
lrwxrwxrwx 1 root      25 May 31 16:05 liborc-test-0.4.so.0 -> liborc-test-0.4.so.0.25.0
-rwxr-xr-x 1 root   37120 May 31 16:05 liborc-test-0.4.so.0.25.0
-rwxr-xr-x 1 root     921 May 31 16:00 libpng16.la
lrwxrwxrwx 1 root      19 May 31 16:00 libpng16.so -> libpng16.so.16.37.0
lrwxrwxrwx 1 root      19 May 31 16:00 libpng16.so.16 -> libpng16.so.16.37.0
-rwxr-xr-x 1 root  285720 May 31 16:00 libpng16.so.16.37.0
lrwxrwxrwx 1 root      11 May 31 16:00 libpng.la -> libpng16.la
lrwxrwxrwx 1 root      11 May 31 16:00 libpng.so -> libpng16.so
-rw-r--r-- 1 root 6609278 May 31 16:11 libvips.a
-rw-r--r-- 1 root  399402 May 31 16:11 libvips-cpp.a
-rwxr-xr-x 1 root    1278 May 31 16:11 libvips-cpp.la
lrwxrwxrwx 1 root      22 May 31 16:11 libvips-cpp.so -> libvips-cpp.so.42.12.3
lrwxrwxrwx 1 root      22 May 31 16:11 libvips-cpp.so.42 -> libvips-cpp.so.42.12.3
-rwxr-xr-x 1 root  257848 May 31 16:11 libvips-cpp.so.42.12.3
-rwxr-xr-x 1 root    1230 May 31 16:11 libvips.la
lrwxrwxrwx 1 root      18 May 31 16:11 libvips.so -> libvips.so.42.12.3
lrwxrwxrwx 1 root      18 May 31 16:11 libvips.so.42 -> libvips.so.42.12.3
-rwxr-xr-x 1 root 4293368 May 31 16:11 libvips.so.42.12.3
-rw-r--r-- 1 root 1059222 May 31 16:02 libwebp.a
-rw-r--r-- 1 root  587612 May 31 16:02 libwebpdecoder.a
-rwxr-xr-x 1 root     973 May 31 16:02 libwebpdecoder.la
lrwxrwxrwx 1 root      23 May 31 16:02 libwebpdecoder.so -> libwebpdecoder.so.3.1.1
lrwxrwxrwx 1 root      23 May 31 16:02 libwebpdecoder.so.3 -> libwebpdecoder.so.3.1.1
-rwxr-xr-x 1 root  404664 May 31 16:02 libwebpdecoder.so.3.1.1
-rw-r--r-- 1 root   15826 May 31 16:02 libwebpdemux.a
-rwxr-xr-x 1 root     979 May 31 16:02 libwebpdemux.la
lrwxrwxrwx 1 root      21 May 31 16:02 libwebpdemux.so -> libwebpdemux.so.2.0.7
lrwxrwxrwx 1 root      21 May 31 16:02 libwebpdemux.so.2 -> libwebpdemux.so.2.0.7
-rwxr-xr-x 1 root   21736 May 31 16:02 libwebpdemux.so.2.0.7
-rwxr-xr-x 1 root     924 May 31 16:02 libwebp.la
-rw-r--r-- 1 root   57384 May 31 16:02 libwebpmux.a
-rwxr-xr-x 1 root     965 May 31 16:02 libwebpmux.la
lrwxrwxrwx 1 root      19 May 31 16:02 libwebpmux.so -> libwebpmux.so.3.0.6
lrwxrwxrwx 1 root      19 May 31 16:02 libwebpmux.so.3 -> libwebpmux.so.3.0.6
-rwxr-xr-x 1 root   49200 May 31 16:02 libwebpmux.so.3.0.6
lrwxrwxrwx 1 root      16 May 31 16:02 libwebp.so -> libwebp.so.7.1.1
lrwxrwxrwx 1 root      16 May 31 16:02 libwebp.so.7 -> libwebp.so.7.1.1
-rwxr-xr-x 1 root  720376 May 31 16:02 libwebp.so.7.1.1
drwxr-xr-x 1 root    4096 May 31 16:11 pkgconfig/

$ ls -lAGp /opt/include
-rw-r--r-- 1 root  3836 May 31 16:00 expat_config.h
-rw-r--r-- 1 root  5528 May 31 16:00 expat_external.h
-rw-r--r-- 1 root 41473 May 31 16:00 expat.h
-rw-r--r-- 1 root   792 May 31 16:06 ffi.h
-rw-r--r-- 1 root   840 May 31 16:06 ffitarget.h
-rw-r--r-- 1 root  4343 May 31 16:06 ffitarget-x86_64.h
-rw-r--r-- 1 root 13481 May 31 16:06 ffi-x86_64.h
-rw-r--r-- 1 root  2447 May 31 16:05 fftw3.f
-rw-r--r-- 1 root 54596 May 31 16:05 fftw3.f03
-rw-r--r-- 1 root 31394 May 31 16:05 fftw3.h
-rw-r--r-- 1 root 26983 May 31 16:05 fftw3l.f03
-rw-r--r-- 1 root 25682 May 31 16:05 fftw3q.f03
-rw-r--r-- 1 root 12986 May 31 16:00 gif_lib.h
drwxr-xr-x 3 root  4096 May 31 16:07 gio-unix-2.0/
drwxr-xr-x 5 root  4096 May 31 16:07 glib-2.0/
drwxr-xr-x 2 root  4096 May 31 16:07 gobject-introspection-1.0/
-rw-r--r-- 1 root  2166 May 31 16:00 jconfig.h
-rw-r--r-- 1 root 15177 Dec 31  2019 jerror.h
-rw-r--r-- 1 root 15143 Dec 31  2019 jmorecfg.h
-rw-r--r-- 1 root 50281 Dec 31  2019 jpeglib.h
-rw-r--r-- 1 root  6942 May 31 16:02 libimagequant.h
drwxr-xr-x 2 root  4096 May 31 16:00 libpng16/
drwxr-xr-x 4 root  4096 May 31 16:05 orc-0.4/
lrwxrwxrwx 1 root    18 May 31 16:00 pngconf.h -> libpng16/pngconf.h
lrwxrwxrwx 1 root    14 May 31 16:00 png.h -> libpng16/png.h
lrwxrwxrwx 1 root    21 May 31 16:00 pnglibconf.h -> libpng16/pnglibconf.h
-rw-r--r-- 1 root 73889 Dec 31  2019 turbojpeg.h
drwxr-xr-x 2 root  4096 May 31 16:11 vips/
drwxr-xr-x 2 root  4096 May 31 16:02 webp/
```

## Alternatives

The [Yumda](https://github.com/lambci/yumda) project form Serverless Hero Michael Hart recently added libvips package support. It installs both ImageMagick and Libvips and is an excellent alterative to this project. Check it out!

