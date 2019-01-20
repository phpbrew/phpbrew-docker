# phpbrew-ready docker images

See phpbrew/phpbrew on Docker Hub <https://hub.docker.com/r/phpbrew/phpbrew/tags>


## Build

The build script already provides the magic to build all the images:

```sh
./build
```

To build the phpbrew base image only:

```
./build phpbrew-base
```


To build a specific image only:

```
./build phpbrew/18.04-minimum
```

