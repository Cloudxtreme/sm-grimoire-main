CFLAGS="$CFLAGS -I$INSTALL_ROOT/usr/include/libnl3"
cd "$SOURCE_DIRECTORY/wpa_supplicant"

# Create .config file for make (this is here instead of PRE_BUILD because
# OPTS isn't available there, and this is equivalent to running ./configure
# anyway).
local VARS="CONFIG_NO_WPA CONFIG_DNET_PCAP CONFIG_L2_PACKET CONFIG_NO_WPA2  \
            CONFIG_NO_STDOUT_DEBUG CONFIG_CTRL_IFACE CONFIG_DRIVER_HOSTAP   \
            CONFIG_DRIVER_ATMEL CONFIG_DRIVER_NL80211 \
            CONFIG_DRIVER_WEXT CONFIG_DRIVER_NDISWRAPPER                    \
            CONFIG_DRIVER_IPW CONFIG_DRIVER_WIRED    \
            CONFIG_EAP_MD5 CONFIG_EAP_MSCHAPV2 CONFIG_EAP_TLS               \
            CONFIG_EAP_PEAP CONFIG_EAP_TTLS CONFIG_EAP_GTC CONFIG_EAP_OTP   \
            CONFIG_EAP_SIM CONFIG_EAP_AKA CONFIG_EAP_PSK CONFIG_EAP_PAX     \
            CONFIG_EAP_LEAP CONFIG_EAP_SAKE CONFIG_EAP_GPSK                 \
            CONFIG_EAP_GPSK_SHA256 CONFIG_PKCS12 CONFIG_SMARTCARD"  var     &&

VARS="$VARS CONFIG_TLS" &&

for var in $VARS $OPTS; do
  if [[ ${!var} != n ]]; then
    echo "$var=${!var:-y}" >> .config
    # We ship libnl-3.
    if [[ "$var" = CONFIG_DRIVER_NL80211 ]]; then
      echo CONFIG_LIBNL32=y >> .config
    fi
  fi
done &&

make &&

if is_depends_enabled $SPELL qt4; then
  PATH=$QT4DIR/bin:$PATH make wpa_gui-qt4
fi &&

if is_depends_enabled $SPELL qt-x11; then
  make wpa_gui
fi

