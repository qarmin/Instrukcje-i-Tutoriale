## Cross compilation of GTK-rs from Ubuntu 20.04 to Windows

Recently I tried to cross compile my app from Ubuntu to Windows, but I get a lot of errors when I doing it.

Don't know why Ubuntu doesn't provide mingw package with gtk3 by default, so I need to download it by hand.

Finally I found a method which is a little strange and not optimal, but works, and is easy to integrate with Github CI.

This guide aimed to be a simpler alternative to tutorial - https://gtk-rs.org/docs-src/tutorial/cross - but it turned out that these guides do not differ much. You can find there how to change icon and app theme.

Commit which adding usage to Czkawka you can find here - https://github.com/qarmin/czkawka/commit/1defc06c75606d73bd0011cdf95ffa1e1ca4367c  
Choose any(of cours after merging commit) from https://github.com/qarmin/czkawka/actions to see Windows cross build artifacts.

This is how Czkawka(https://github.com/qarmin/czkawka/) looks on Ubuntu

![Ubuntu](https://user-images.githubusercontent.com/41945903/95159765-2660ba80-079f-11eb-844c-b20b8ea5483e.png)

And this is how looks on Windows

![Windows](https://user-images.githubusercontent.com/41945903/95159750-1fd24300-079f-11eb-9c84-8ca8161129a0.png)


### Required libraries
There are 2 types to use libraries

- Download prepared by libraries needed https://github.com/qarmin/gtk_library_store/releases

- Manually download and extract this libraries
  - Create VM with Windows or use it on bare metal
  - Install on it MSyS 2 from https://msys2.org or https://github.com/msys2/msys2-installer/releases to C:/msys64 (default path)
  - Run in MSys command:
```
pacman -S mingw-w64-x86_64-gtk3

```
  - After installation compress `C:\msys64\mingw64\` to `mingw.zip` and copy it to you Ubuntu OS.


### On Ubuntu
- Install Rust `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  - Restart OS or shell to get properly working Cargo and Rust

- Execute this commands
```
# Adds Windows target config to cargo
echo "[target.x86_64-pc-windows-gnu]" > ~/.cargo/config
echo "linker = \"x86_64-w64-mingw32-gcc\"" >> ~/.cargo/config
echo "ar = \"x86_64-w64-mingw32-gcc-ar\"" >> ~/.cargo/config

GTK_LIBRARY="/home/rafal"
GTK_APP="/home/rafal/gtk_app"

# Installs required packages - for my project minimal gtk version is 3.22, wget, unzip and zip are needed to download and unpack gtk library and later pack it
sudo apt install mingw-w64 libgtk-3-dev unzip wget zip -y

# Download required library to build and ship application(here you can use manually zipped mingw64.zip)
wget https://github.com/qarmin/gtk_library_store/releases/download/3.24.0/mingw64.zip
unzip mingw64.zip -d $GTK_LIBRARY
GTK_LIBRARY="$GTK_LIBRARY/mingw64"

# Clone repository
git clone https://github.com/qarmin/czkawka.git ~/czkawka
cd ~/czkawka

# Test build for Linux
cargo build --bin czkawka_gui

# Linux crossbuild for Windows
PKG_CONFIG_ALLOW_CROSS=1 PKG_CONFIG_PATH="$GTK_LIBRARY/lib/pkgconfig" RUSTFLAGS="-L $GTK_LIBRARY/lib" cargo build --target=x86_64-pc-windows-gnu --bin czkawka_gui --release


# Create app folder and copy to it all files and dependiences
mkdir $GTK_APP
cp target/x86_64-pc-windows-gnu/release/czkawka_gui.exe $GTK_APP
cp $GTK_LIBRARY/bin/*.dll $GTK_APP
mkdir -p $GTK_APP/share/glib-2.0/schemas
mkdir $GTK_APP/share/icons
cp $GTK_LIBRARY/share/glib-2.0/schemas/* $GTK_APP/share/glib-2.0/schemas
cp -r $GTK_LIBRARY/share/icons/* $GTK_APP/share/icons
mkdir $GTK_APP/lib
cp -r $GTK_LIBRARY/lib/gdk-pixbuf-2.0 $GTK_APP/lib

zip -r gtk_app.zip $GTK_APP

```
- Your application should be ready
