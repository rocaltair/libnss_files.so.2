# How to customize your own hosts file

As we all known, normal users can't not edit file `/etc/hosts` directly.

How to customize your own hosts file for your own processes without affect others?

you can use this lib to customize your own hosts file with file `/code/host`, 

or you can edit `libnss_files.so.2` replace `/code/host` into other path string with 10 characters.

## Usage

First, edit file `/code/host` like following:

```
127.0.0.1 api.example.com
123.123.234.234 www.test.com
```

### use `LD_LIBRARY_PATH`

* save `libnss_files.so.2` into a custom directory, for example, `/tmp/xyz`
* then export env variable `LD_LIBRARY_PATH=/tmp/xyz`
* for example:

```
export LD_LIBRARY_PATH=/tmp/xyz
ping api.example.com
```

or

```
LD_LIBRARY_PATH=/tmp/xyz ping api.example.com
```

### use `LD_PRELOAD`
* save `libnss_files.so.2` into a custom directory, for example, `/tmp/xyz`
* then export env variable `LD_PRELOAD=/tmp/xyz/libnss_files.so.2`
* for example:

```
export LD_PRELOAD=/tmp/xyz/libnss_files.so.2
ping api.example.com
```

or

```
LD_PRELOAD=/tmp/xyz/libnss_files.so.2 ping api.example.com
```

### Usage in [Aliyun Function Compute](https://www.aliyun.com/product/fc)
* put download this lib into your project root directory;
* new a file named `host`, and edit it in your project root directory;
* update your function.
* set ENV variable with key: `LD_LIBRARY_PATH` and value: `/code` in your function.

