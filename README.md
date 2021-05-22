# m3u8-downloader

Golang multi-thread download of live streaming video in m3u8 format, cross-platform. You only need to specify the necessary flags (`u`, `o`, `n`, `ht`) to run, and the tool will automatically parse the M3U8 file for you, and download the TS fragments and merge them into one file.


## Features

1. Download and parse M3U8
2. Download TS failed to retry (encrypted synchronous decryption)
3. Merge TS fragments

> Can download island country movies
> Can download island country movies
> Can download island country movies
> Say important things three times...

## Show results
![demo](./demo.gif)

## Parameter Description:

```
-u M3U8 address
-o Custom file name, default output
-n The number of concurrent downloads of the coroutine, the default is 16
-ht sets the getHost method (a total of two apiv1 and apiv2), the default is apiv1
-c Custom request cookie, empty by default
```

By default, only the `u` parameter needs to be passed, and other parameters can be kept as default. Some links may limit the request frequency, and the value of the `n` parameter can be adjusted according to the actual situation.

## Download

The compiled platforms are: [click to download](https://github.com/llychao/m3u8-downloader/releases)

-windows/amd64
-linux/amd64
-darwin/amd64

## Usage

### Source code method

```bash
Compile by yourself: go build -o m3u8-downloader
Concise use: ./m3u8-downloader -u=http://example.com/index.m3u8
Full use: ./m3u8-downloader -u=http://example.com/index.m3u8 -o=example -n=16 -ht=apiv1 -c="key1=v1; key2=v2"
```

### Binary method:

Linux and MacOS and Windows PowerShell

```
Concise use:
./m3u8-downloader-v1.0.0-linux-amd64 -u=http://example.com/index.m3u8
./m3u8-downloader-v1.0.0-darwin-amd64 -u=http://example.com/index.m3u8
.\m3u8-downloader-v1.0.0-windows-amd64.exe -u=http://example.com/index.m3u8

Full use:
./m3u8-downloader-v1.0.0-linux-amd64 -u=http://example.com/index.m3u8 -o=example -n=16 -ht=apiv1 -c="key1=v1; key2=v2 "
./m3u8-downloader-v1.0.0-darwin-amd64 -u=http://example.com/index.m3u8 -o=example -n=16 -ht=apiv1 -c="key1=v1; key2=v2 "
.\m3u8-downloader-v1.0.0-windows-amd64.exe -u=http://example.com/index.m3u8 -o=example -n=16 -ht=apiv1 -c="key1=v1; key2 =v2"
```

## Problem description

1. On Linux or mac platform, if it shows no running permission, please use chmod command to add permission
```bash
 # Linux amd64 platform
 chmod 0755 m3u8-downloader-v1.0.0-linux-amd64
 # Mac darwin amd64 platform
 chmod 0755 m3u8-downloader-v1.0.0-darwin-amd64
 ```
2. If the download fails, please set -ht="apiv1" or -ht="apiv2" (default is apiv1)
```golang
func get_host(Url string, ht string) string {
    u, err := url.Parse(Url)
    var host string
    checkErr(err)
    switch ht {
    case "apiv1":
        host = u.Scheme + "://" + u.Host + path.Dir(u.Path)
    case "apiv2":
        host = u.Scheme + "://" + u.Host
    }
    return host
}
```
