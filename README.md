# docker-golang-builder

An image that can build a go source repository.  All built artifacts
from `GOPATH/bin` will be put into `/usr/local/bin`.  Available as
[pallet/golang-builder][pallet-golang-builder].

You should use this image to build your own images using a Dockerfile.
For example, to build an image for [helixdns][helixdns]:

```
FROM pallet/golang-builder
CMD ["/usr/local/bin/helixdns"]
```

The repository to be built needs to be specified in a docker build
bundle file, named `gorepo` (ie. a file namedd `gorepo` in the same
directory as your `Dockerfile`).  The `gorepo` file must be a shell
script that sets the `GOREPO` environment variable to something that
`go get` will understand.

For the helixdns example, this would be:

```
GOREPO=github.com/mrwilson/helixdns
```

## License

Copyright © 2014 Hugo Duncan

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.

[helixdns]: https://github.com/mrwilson/helixdns "helixdns DNS server"
[pallet-golang-builder]: https://registry.hub.docker.com/u/pallet/golang-builder/ "golang-builder image"
