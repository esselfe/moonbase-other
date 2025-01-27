cd /usr/lib/virtualbox/src &&

if module_installed linux; then
  export KERN_VER=$(installed_version linux)
  export KERN_DIR=/usr/src/linux-$KERN_VER &&
elif module_installed linux-lts; then
  export KERN_VER=$(installed_version linux-lts)
  export KERN_DIR=/usr/src/linux-lts-$KERN_VER &&
fi
export MODULE_DIR=/lib/modules/$KERN_VER/misc

ln -sf ../vboxdrv    ./vboxdrv/vboxdrv &&
ln -sf ../vboxnetadp ./vboxnetadp/vboxnetadp &&
ln -sf ../vboxnetflt ./vboxnetflt/vboxnetflt &&
#ln -sf ../vboxpci    ./vboxpci/vboxpci &&

rm -fR vboxpci &&

default_make &&

install -Dm0644 /dev/null /usr/lib/modules-load.d/virtualbox-modules.conf &&
echo -e "vboxdrv\nvboxpci\nvboxnetadp\nvboxnetflt\n" > /usr/lib/modules-load.d/virtualbox-modules.conf &&

make clean
