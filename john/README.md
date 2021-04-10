# john

## Links
* [The GNU C Library Release Timeline](https://sourceware.org/glibc/wiki/Glibc%20Timeline)
* [Statically linking libgomp (distroless)](https://groups.google.com/g/bazel-discuss/c/jVf2oCHJECY?pli=1)


## Checking distroless image for glibc version
```bash
$ docker create --name=cc  gcr.io/distroless/cc echo; docker export cc | tar -t | grep -i "libc-"
57f159b7e1230390bc901e5ced4d139f84dce08e2f29bcdf24ea41ea11208f9a
lib/x86_64-linux-gnu/libc-2.24.so

$ docker create --name=base  gcr.io/distroless/base echo; docker export base | tar -t | grep -i "libc-"
9650d04f0a6d9a8a3d7f0f5f9b6366d08d9d59d4a580ffec91319a07fe5ff9b3
lib/x86_64-linux-gnu/libc-2.24.so

$docker create --name=d10  gcr.io/distroless/base-debian10 echo; docker export d10 | tar -t | grep -i "libc-"
8da8cc2e9a0450e8d35c355008dbf4a4889c5e8d1f3700d76dd11ecd6febf095
lib/x86_64-linux-gnu/libc-2.28.so
```

