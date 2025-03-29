# listen

listen on a TCP port, accept connection and do simple I/O


# To install

```sh
sudo make install
```


# To use

```sh
/usr/local/bin/listen [-h] [-v lvl] [-V] [-d] [interface:]port

    -h              print help and exit
    -v lvl          verbose / debug level
    -V              print version and exit

    -d  daemon mode, re-listen after connection is dropped

    [interface:]port    the local interface and port to listen on

listen version: 1.10.1 2025-03-28
```


# Example

Listen in TCP port 12345 on 127.0.0.1:

```sh
$ /usr/local/bin/listen -v 1 127.0.0.1:12345
DEBUG: debug level: 1
DEBUG: listening only on interface: 127.0.0.1 (127.0.0.1)
DEBUG: will listen on port: 12345
DEBUG: listen queue created
DEBUG: listening for a connection
```

Then in another terminal telnet to TCP port 12345 on 127.0.0.1:

```sh
$ telnet 127.0.0.1 12345
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
```

Once connected, the listen program and telnet can "chat" with each other.
I/O can go both ways:

For example, from the listen program we see:

```
DEBUG: accepted connection from 127.0.0.1(54568) == localhost(54568)
This line is from listen
The other line is from telnet
^C
zsh: interrupt  ./listen -v 1 127.0.0.1:12345
```

The **^C** is when we interrupt the listen program and terminate it.

And for example, from the telnet program we see:

```
This line is from listen
The other line is from telnet
Connection closed by foreign host.
zsh: exit 1     telnet 127.0.0.1 12345
```

In this example, we listen on TCP port 8080 of our external IP address (10.10.1.215):

```sh
$ /usr/local/bin/listen -v 1 10.10.1.215:8080
DEBUG: debug level: 1
DEBUG: listening only on interface: 10.10.1.215 (10.10.1.215)
DEBUG: will listen on port: 8080
DEBUG: listen queue created
DEBUG: listening for a connection
```

Then we use a browser to collect to `http://10.10.1.215:8080`, we see the browser connection show up in the listen window:

```
DEBUG: accepted connection from 10.10.1.215(54872) == computer.example.org(54872)
GET / HTTP/1.1
Host: 10.10.1.215:8080
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.3.1 Safari/605.1.15
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.9
Priority: u=0, i
Accept-Encoding: gzip, deflate
Connection: keep-alive

...
```


# Reporting Security Issues

To report a security issue, please visit "[Reporting Security Issues](https://github.com/lcn2/listen/security/policy)".
