# Non-Packaged Libraries and Programs

Linux Mint is nice but some of the software is not recent enough.  Not
too hard to compile own bits or fetch from elsewhere.

May want to `sudo apt install git gcc make autoconf cmake` and add
some `deb-src` entries via "System -> Software Sources" (just toggle
the "Source code repositories" option)

## tree-sitter library

For a more up-to-date tree-sitter...

```
cd ~/src
git clone https://github.com/tree-sitter/tree-sitter
cd tree-sitter
git checkout v0.25.8
# you did create ~/.local earlier, right?
make PREFIX=$HOME/.local clean
make PREFIX=$HOME/.local
make PREFIX=$HOME/.local install
# there is even an uninstall target, nice -- though PREFIX
# may need to be specified for that to work well as well
# as having the appropriate tag checked out (e.g. here
# we did `git checkout v0.25.8` -- we'll want the same
# if using the uninstall target)
```

## emacs

For an emacs that uses a more up-to-date tree-sitter...

```
# get emacs build dependencies -- this is what the deb-src stuff above was for
sudo apt build-dep emacs-gtk
# don't want these though -- they are too old
sudo apt remove libtree-sitter-dev libtree-sitter0
cd ~/src
git clone https://github.com/emacs-mirror/emacs/
cd emacs
git checkout emacs-30.1
# needs autoconf -- used apt get earlier, right?
bash autogen.sh
TREE_SITTER_CFLAGS=-I$HOME/.local/include TREE_SITTER_LIBS="-L$HOME/.local/lib -ltree-sitter" \
  ./configure \
  --prefix=$HOME/.local \
  --with-tree-sitter \
  --with-cairo
LD_LIBRARY_PATH=$HOME/.local/lib make
LD_LIBRARY_PATH=$HOME/.local/lib make install
```

## LD_LIBRARY_PATH

Put `export LD_LIBRARY_PATH=$HOME/.local/lib` into `~/.profile`.

This is for things that want to use our local libraries to work, emacs
is one such thing.

This might be kind of a work-around.  May be there's a better
method...

## tree-sitter-module

For tree-sitter parser shared objects / libraries.

Already had these bits (also linked to from under `~/.emacs.d`), but FWIW:

```
cd ~/src
git clone https://github.com/casouri/tree-sitter-module
cd tree-sitter-module
bash batch.sh
```

## neovim

To follow development of neovim.

```
cd ~/src
git clone https://github.com/neovim/neovim
cd neovim
# you did install cmake via apt, right?
make CMAKE_BUILD_TYPE=RelWithDebInfo CMAKE_INSTALL_PREFIX=$HOME/.local
make install
```

## janet

To follow development of janet.

```
cd ~/src
git clone https://github.com/janet-lang/janet
cd janet
make clean && PREFIX=$HOME/.local make && PREFIX=$HOME/.local make install
```

## clojure

```
sudo apt install openjdk-21-jdk curl rlwrap
curl -L -O https://github.com/clojure/brew-install/releases/latest/download/linux-install.sh
bash linux-install.sh --prefix $HOME/.local
```

## brave

https://brave.com/linux/

## gnucash

https://wiki.gnucash.org/wiki/Building_On_Linux

```
sudo apt install libdbd-sqlite3
sudo apt build-dep gnucash
git clone https://github.com/Gnucash/gnucash
cd gnucash
git checkout 5.12
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local ..
make
make check
make install
```

### Python Bindings

* If python bindings are desired, build with:

    ```
    cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local -DWITH_PYTHON=on ..
    ```

* https://lists.gnucash.org/pipermail/gnucash-devel/2008-July/023431.html
* https://wiki.gnucash.org/wiki/Python_Bindings
* https://code.gnucash.org/docs/STABLE/python_bindings_page.html
* https://code.gnucash.org/docs/STABLE/group__python__bindings.html
* https://code.gnucash.org/docs/STABLE/group__python__bindings__examples.html
* https://codigoparallevar.com/blog/2023/programmatic-access-to-gnucash-using-python/

### Custom Reports

* https://wiki.gnucash.org/wiki/Custom_Reports - Scheme, Guile, Samples, etc.

## gnucash-docs

https://wiki.gnucash.org/wiki/Building_On_Linux

```
sudo apt build-dep gnucash-docs
git clone https://github.com/Gnucash/gnucash-docs
cd gnucash-docs
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local ..
make
make install
```

