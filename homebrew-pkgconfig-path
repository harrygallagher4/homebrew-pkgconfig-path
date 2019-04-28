#!/bin/zsh

if ! (( $+commands[jq] )) ; then
  echo "jq is not installed"
  exit 1
fi

kegs=$(brew info --installed --json | jq 'map(select(.keg_only == true))[]["name"]' | tr -d '"')

kegs=(${(f)kegs})

path_str="$PKG_CONFIG_PATH"

for keg in $kegs; do
  keg_pc_dir="/usr/local/opt/$keg/lib/pkgconfig"
  [[ -d $keg_pc_dir ]] && ! (pkg-config --exists "$keg") && path_str="$path_str:$keg_pc_dir"
done

echo -n "$path_str"
