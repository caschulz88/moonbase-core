(

  patch_it $SOURCE2 1  &&
  patch_it $SOURCE3 1  &&

  # Fix for make 3.82
  sedit "s;*/module.mk;proc/module.mk ps/module.mk;" Makefile  &&
  sedit "s/\/usr\/bin/\/bin/g" Makefile  &&
  make CFLAGS="$CFLAGS" PKG_CFLAGS="-W"  &&

  prepare_install  &&
  make  -e XSCPT='' DESTDIR=/ install  &&

  if [ -e /etc/init.d/sysctl.sh ]; then
    rm -f /etc/init.d/sysctl.sh  &&
    rm -f /etc/rcS.d/S99sysctl
  fi  &&

  if module_installed sysvinit; then
    cp $SCRIPT_DIRECTORY/init.d/sysctl /etc/init.d &&
    ln -sf ../init.d/sysctl /etc/rcS.d/S99sysctl
  fi  &&

  if [ ! -e /etc/sysctl.conf ] ; then
    install -g0 -o0 -m0600 $SCRIPT_DIRECTORY/sysctl.conf /etc
  fi

) > $C_FIFO 2>&1
