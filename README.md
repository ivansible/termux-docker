# Termux environment for Docker/Podman (FORK).

A [Termux](https://termux.com) environment packaged into Docker image.
Environment doesn't have Android runtime components, so certain things will
not be available (DalvikVM, OpenSLES, etc...).

## How to use

1. Make sure that Docker is installed and running.
2. `git clone https://github.com/termux/termux-docker && cd ./termux-docker`
3. `./run.sh` or `./run-x86_64.sh` - if need x86_64 arch.

You can use the image directly without startup script. For example:
```
docker run -it kcubeterm/termux:latest
```

You can build Docker image yourself by running this script:
```
./build-all.sh
```

### Using with Podman

If you have Podman instead of Docker, usage is nearly same.

Building image:
```
./build-all.sh --podman
```

Running image:
```
./run.sh --podman
./run-x86_64.sh --podman
```

## Known issues

There a number of known issues which may not be resolved:

* ARM containers may require a custom seccomp profile to remove restrictions from
  `personality()` system call. Whereas Docker Hub contains prebuilt ARM image, it
  is outdated and won't receive updates anymore.

* DNS: Docker image has to use a static DNS resolver through `/system/etc/hosts`.
  You can regenerate this file by editing `/system/etc/static-dns-hosts.txt` and
  executing script `/system/bin/update-static-dns`.
