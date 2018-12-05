# Kirigami application template

This repository can be used as a template to develop Plasma Mobile applications.
It already includes templates for the qml ui, a c++ part, app metadata and flatpak packaging.

## Local building and testing using the SDK
```
flatpak install flathub org.kde.Sdk//5.11 # Only needs to be done once
flatpak-builder flatpak-build-desktop --force-clean --ccache *.json
flatpak-builder --run flatpak-build-desktop *.json hellokirigami
```

## Creating a flatpak for the phone
This assumes your system is already set up as described [here](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak).
Make sure your system also supports qemu user emulation. If not, you can find help for example [here](https://wiki.debian.org/QemuUserEmulation)

```
flatpak install flathub org.kde.Sdk/arm/5.11 # Only needs to be done once
flatpak-builder flatpak-build-phone --repo=arm-phone --arch=arm --force-clean --ccache *.json
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


## Using the template to develop your application
Edit the files to fit your naming and needs. In each command, replace "io.you.newapp" and "newapp" with the id and name you want to use

```
find . -name "CMakeLists.txt" -or -name "*.desktop" -or -name "*.xml" -or -name "*.json" -exec sed -i 's/org.kde.hellokirigami/io.you.newapp/g;s/hellokirigami/newapp/g' {} \;

for file in $(find . -name "org.kde.hellokirigami*"); do mv $file $(echo $file | sed "s/org.kde.hellokirigami/io.you.newapp/g"); done
```
