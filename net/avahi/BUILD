export PYTHONDONTWRITEBYTECODE=1 &&

#Fix a security vulnerabilty in avahi-daemon: 
sedit '426a if (events & AVAHI_WATCH_HUP) {client_free(c);return;}' avahi-daemon/simple-protocol.c &&

autoreconf -fiv &&

if module_installed qt5; then
  . /etc/profile.d/qt5.rc
  QT5_CFLAGS="-I/usr/include/qt5/QtCore -I/usr/include/qt5" &&
  QT5_LIBS="-L/usr/lib/qt5 -lQt5Core"
fi &&

add_priv_user avahi:avahi -d /dev/null -s /usr/bin/false &&
add_priv_user avahi-autoipd:avahi-autoipd -d /dev/null -s /usr/bin/false &&

# Add this missing group. It is used in /etc/dbus-1/system.d/avahi-dbus.conf
add_priv_group netdev &&

OPTS+=" --enable-compat-howl \
        --enable-compat-libdns_sd \
        --disable-stack-protector \
        --disable-mono \
        --disable-monodoc \
        --disable-static \
        --disable-qt3 \
        --disable-qt4 \
        --disable-gtk \
        --disable-manpages \
        --disable-core-docs \
        --with-distro=none \
        --enable-python-dbus \
        --enable-introspection=yes \
        --with-avahi-priv-access-group=network
        --prefix=/usr \
        --sysconfdir=/etc \
        --runstatedir=/run \
        --localstatedir=/var \
        --sbindir=/usr/bin" &&

./configure $OPTS &&
sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool &&

default_make &&

if ! ( module_installed xmltoman ); then
  rm -f /usr/share/man/man1/avahi*
  rm -f /usr/share/man/man1/bvnc.1
fi
