# homebrew-pkgconfig-path

This is a zsh script to generate a `PKG_CONFIG_PATH` string that includes your Homebrew kegs.
I ran into trouble compiling something recently and didn't realize that `libffi` installed
by homebrew wasn't recognized by pkg-config. I really prefer to just use a nice package 
manager for everything so I wanted pkg-config to automatically recognize my homebrew kegs.
This does that. 

![](https://i.imgur.com/FVXAaFP.png)

My `.zshrc` automatically reads from a file called `~/.pc_path` which I update via this
script.


#### `~/.zshrc`
```zsh
export PKG_CONFIG_PATH=$(cat "$HOME/.pc_path")
```

#### `~/.pc_path`
```
/usr/local/lib/pkgconfig:/usr/local/opt/icu4c/lib/pkgconfig:/usr/local/opt/libf
fi/lib/pkgconfig:/usr/local/opt/libxml2/lib/pkgconfig:/usr/local/opt/ncurses/li
b/pkgconfig:/usr/local/opt/openssl/lib/pkgconfig:/usr/local/opt/readline/lib/pk
gconfig:/usr/local/opt/ruby/lib/pkgconfig:/usr/local/opt/sqlite/lib/pkgconfig
```

Then anytime I install a new library with homebrew just run...
```console
harry@mac:~$ homebrew-pkgconfig-path > ~/.pc_path
```
