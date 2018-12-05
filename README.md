# Kirigami application template

This repository can be used as a template to develop Plasma Mobile applications.
It already includes templates for the qml ui, a c++ part, app metadata and flatpak packaging.

## Building (requires Qt and Kirigami development libraries)
```
mkdir build && cmake -B build -S $PWD -GNinja -DCMAKE_INSTALL_PREFIX=/usr ..
ninja -C build
```

## Local building and testing using the SDK
```
flatpak install flathub org.kde.Sdk//5.11 # Only needs to be done once
flatpak-builder flatpak-build --force-clean --ccache *.json
flatpak-builder --run flatpak-build *.json hellokirigami
```

## Creating a flatpak for the phone
This assumes your system is already set up as described [here](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak).
Make sure your system also supports qemu user emulation. If not, you can find help for example [here](https://wiki.debian.org/QemuUserEmulation)

```
flatpak install flathub org.kde.Sdk/arm/5.11 # Only needs to be done once
flatpak-builder flatpak-build --repo=arm-phone --arch=arm --force-clean --ccache *.json
flatpak build-bundle arm-phone app.flatpak org.kde.hellokirigami
```

Now your app is exported into app.flatpak. You can copy the file to the phone using scp:
```
scp app.flatpak phablet@10.15.19.82:/home/phablet/app.flatpak
```

```
ssh phablet@10.15.19.82
flatpak install app.flatpak
```

Your new application should now appear on the homescreen.
