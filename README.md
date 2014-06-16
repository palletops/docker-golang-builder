# docker-golang-builder

An image that allows you to use a Dockerfile as a Go build tool. You
can build a Go source repository and deploy the artifacts onto the
resulting image. No compiler or source code is left on the resulting
image.

Available as [pallet/golang-builder][pallet-golang-builder].

## Usage

You should use this image to build your own images using a Dockerfile.
For example, to build an image for [helixdns][helixdns], you would
create a `Dockerfile` that executes the command your project builds:

```
FROM pallet/golang-builder
CMD ["/usr/local/bin/helixdns"]
```

The repository to be built needs to be specified in a docker build
bundle file, named `gorepo` (ie. a file namedd `gorepo` in the same
directory as your `Dockerfile`).  The `gorepo` file must be a shell
script that sets the `GOREPO` environment variable to something that
`go get` will understand.  All built artifacts from GOPATH/bin will be
put into /usr/local/bin.

For the helixdns example, this would be:

```
GOREPO=github.com/mrwilson/helixdns
```

With this configuration, building your image with Docker (ie. `docker
build`) will pull the code, build the binaries, install them in
`/usr/local/bin`, and set them to run when the image launches. The
final image will not contain the Go toolchain or the source code.


## License

Copyright © 2014 Hugo Duncan

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.

[helixdns]: https://github.com/mrwilson/helixdns "helixdns DNS server"
[pallet-golang-builder]: https://registry.hub.docker.com/u/pallet/golang-builder/ "golang-builder image"
