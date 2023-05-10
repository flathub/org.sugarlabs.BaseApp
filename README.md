# Sugar Labs BaseApp

This BaseApp contains dependencies shared between ALL Sugar Labs applications.

## How To Build

```
git clone --recurse-submodules https://github.com/flathub/org.sugarlabs.BaseApp.git
cd org.sugarlabs.BaseApp
flatpak -y --user install org.gnome.{Platform,Sdk}//44
flatpak-builder --user --force-clean --install build org.sugarlabs.BaseApp.json
```

## How To Update

```
cd org.sugarlabs.BaseApp
git submodule update --remote
```

Then edit `org.sugarlabs.BaseApp.json` to:

1. Bump GNOME runtime to the latest stable version, e.g. `"runtime-version": "44"`
2. Bump Python version references to the one included in the GNOME runtime, e.g. `flatpak --user run --command=python org.gnome.Platform//44 --version`
3. Bump Perl version references to the one included in the GNOME SDK, e.g. `flatpak --user run --command=perl org.gnome.Sdk//44 --version`
4. Update `shared-modules` submodule with `git submodule update --remote`.
5. Update every single module to the latest stable version. e.g. for python modules use [flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools).
