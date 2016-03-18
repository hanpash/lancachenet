# Origin Cache Docker Container

## Introduction

This docker container provides a caching proxy server for Origin content. For any network with more than one PC gamer in connected this will drastically reduce internet bandwidth consumption. 

The primary use case is gaming events, such as LAN parties, which need to be able to cope with hundreds or thousands of computers receiving an unannounced patch - without spending a fortune on internet connectivity. Other uses include smaller networks, such as Internet Cafes and home networks, where the new games are regularly installed on multiple computers; or multiple independent operating systems on the same computer.

## Usage

You will need to have a DNS server forwarding queries to the machine your docker container is running on. You can use the [steamcache-dns](https://hub.docker.com/r/steamcache/steamcache-dns/) docker image to do this or you can use a DNS service already on your network see the [steamcache-dns github page](https://github.com/steamcache/steamcache-dns) for more information.

Run the origin container with the using the following to allow TCP port 80 (HTTP) through the host machine:

```
docker run --name origin -p 192.168.0.5:80:80 steamcache/origin:latest
```
## Quick Explanation

For an Origin cache to function on your network you need two services.

* An Origin cache service [This container](https://github.com/steamcache/origin)
* A special DNS service [steamcache-dns](https://github.com/steamcache/steamcache-dns)

The Origin cache service transparently proxies your requests for content to Origin, or serves the content to you if it already has it.

The special DNS service handles DNS queries normally (recursively), except when they're about Origin and in that case it responds that the depot cache service should be used.

Note: steamcache-dns does not currently support Twitch. It will be updated shortly.

## Suggested Hardware

Regular commodity hardware (a single 2TB WD Black on an HP Microserver) can achieve peak throughputs of 30MB/s+ using this setup (depending on the specific content being served).

## Monitoring

Tail the access logs (default: /data/logs/access.log).

## Running on Startup

Follow the instructions in the Docker documentation to run the container at startup.
[Documentation](https://docs.docker.com/articles/host_integration/)

## Thanks

Based on original configs from [ansible-lanparty](https://github.com/ti-mo/ansible-lanparty).

## License

The MIT License (MIT)

Copyright (c) 2016 Michael Smith, Robin Lewis, Brian Wojtczak, Jason Rivers

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

