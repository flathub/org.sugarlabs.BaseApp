# Sugar Labs BaseApp

This BaseApp contains dependencies shared between ALL Sugar Labs applications.

## How To Build

```
git clone --recurse-submodules https://github.com/flathub/org.sugarlabs.BaseApp.git
cd org.sugarlabs.BaseApp
flatpak -y --user install org.gnome.{Platform,Sdk}//42
flatpak-builder --user --force-clean --install build org.sugarlabs.BaseApp.json
```

## How To Update

```
cd org.sugarlabs.BaseApp
git submodule update --remote
```

Then edit `org.sugarlabs.BaseApp.json` to update every single module to the latest supported version. For `python` modules, for each one, go to https://pypi.org and grab the latest.
