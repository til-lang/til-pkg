# til-pkg

A package manager for Til

## Dependencies

* bash
* shell utils (sort, sed, cut)
* make
* git
* ldc2

## Usage

### Install Til in your system

```bash
$ ./til-pkg install_til
```

### Install an "official" package

Example: installing the `http` package:

```bash
$ ./til-pkg install http
```

You can also install a specific version:

```bash
$ ./til-pkg install http 0.1.2
```

### Install a third-party package

```bash
$ ./til-pkg install https://git.sr.ht/til-mypackage
```

### Update a package

```bash
$ ./til-pkg update mypackage
```

(It's going to use the next version **compatible with your current Til's
version**, of course.)

### Upgrade a package

It's the same as **installing** the package again:

```bash
$ ./til-pkg install http
```

If you want to upgrade to a specific version:

```bash
$ ./til-pkg install http 0.1.2
```

# Distributing your Til package

Having a **git repository** that can be cloned by your users using `git
clone` command is enough to distribute your Til packages (no need to
register it anywhere).


`til-pkg` expects all releases to be tagged as `vX.Y.Z` in the master/main
branch.


Your package version `X.Y` numbers must pair with Til's own `X.Y` numbers.

For instance: if current Til version is 0.20.5, your package version
should be `0.20.Z`. `Z` can be any number or text, but keep in mind that
it must be sortable with `sort -V`.


The repository name should be `til-PACKAGENAME`, where PACKAGENAME is the
name it's intended to be called inside Til. The `http` package, for
example, lives in a repository called `til-http` (and generates a shared
object called `libtil_http.so`).


Your package's Makefile should be similar to `til-http` one. Building your
package is done with a simple `make` call (without arguments), preceded by
a `make clean`, so the existence of a `clean` target is mandatory.
