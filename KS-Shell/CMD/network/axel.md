# axel

```md
Axel 通过打开多个 HTTP/FTP 连接来将一个文件进行分段下载，从而达到加速下载的目的。
对于下载大文件，该工具将特别有用。
常用 Axel 替代 wget。
```

## install
```sh
yum install axel
```
```sh
brew install axel
```

## /etc/axel/axelrc
```md
axel的全局配置文件，以根据需要对axel进行定制。
```

## 
```sh
$axel -h
Usage: axel [options] url1 [url2] [url...]

--max-speed=x           -s x    Specify maximum speed (bytes per second)
--num-connections=x     -n x    Specify maximum number of connections
--max-redirect=x                Specify maximum number of redirections
--output=f              -o f    Specify local output file
--search[=n]            -S[n]   Search for mirrors and download from n servers
--ipv4                  -4      Use the IPv4 protocol
--ipv6                  -6      Use the IPv6 protocol
--header=x              -H x    Add HTTP header string
--user-agent=x          -U x    Set user agent
--no-proxy              -N      Just don't use any proxy server
--insecure              -k      Don't verify the SSL certificate
--no-clobber            -c      Skip download if file already exists
--quiet                 -q      Leave stdout alone
--verbose               -v      More status information
--alternate             -a      Alternate progress indicator
--help                  -h      This information
--timeout=x             -T x    Set I/O and connection timeout
--version               -V      Version information

Visit https://github.com/axel-download-accelerator/axel/issues to report bugs
```
```sh
axel -a -n 10 url
```

