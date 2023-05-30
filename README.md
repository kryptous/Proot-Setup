Setup Linux Proot/Chroot on Android with Pulse audio

## 1. Install ubuntu
#### 1.1 Proot ubuntu 
```
echo "allow-external-apps = true" >> ~/.termux/termux.properties
echo "hide-soft-keyboard-on-startup = true" >> ~/.termux/termux.properties
pkg clean && termux-setup-storage && yes | pkg update && pkg install nano wget proot-distro pulseaudio -y && pkg clean && 
proot-distro install ubuntu && proot-distro clear-cache &&
echo 'pulseaudio --kill --start --exit-idle-time=-1 --load="module-native-protocol-tcp auth-ip-acl=127.0.0.1 auth-anonymous=1"    
alias start="proot-distro login ubuntu --shared-tmp --no-sysvipc"' > ~/.bashrc && termux-reload-settings && source ~/.bashrc
```
#### 1.2 Chroot ubuntu 
```
su -c /data/adb/magisk/busybox wget https://raw.githubusercontent.com/xDoge26/Proot-Setup/main/Chroot/Test_install.sh && 
su -c chmod 777 ~/Test_install.sh && ./Test_install.sh && source ~/.bashrc ; su -c rm -rf ~/Test_install.sh
```
## 2. Install xfce
```
wget https://raw.githubusercontent.com/xDoge26/Proot-Setup/main/xfce4.sh &&
chmod +x xfce4.sh && ./xfce4.sh ; rm --force xfce4.sh
```
## 3. Install box86/box64
```
wget https://raw.githubusercontent.com/kryptous/Proot-Setup/main/box86_64.sh && 
chmod +x box86_64.sh && ./box86_64.sh ; rm --force box86_64.sh
```
## 4. VirGL
#### 4.1 VirGL ES (Recommended)
- Install required packages
```
pkg install x11-repo 
pkg install virglrenderer-android
```
- Creating alias
```
echo 'alias gl="MESA_NO_ERROR=1 MESA_GL_VERSION_OVERRIDE=4.3COMPAT MESA_GLES_VERSION_OVERRIDE=3.2 virgl_test_server_android &"' >> /data/data/com.termux/files/home/.bashrc
echo 'alias gl="MESA_NO_ERROR=1 MESA_GL_VERSION_OVERRIDE=4.3COMPAT MESA_EXTENSION_OVERRIDE=GL_EXT_polygon_offset_clamp GALLIUM_DRIVER=virpipe WINEDEBUG=-all"' >> /data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/ubuntu/root/.bashrc
source ~/.bashrc
```
#### 4.2 VirGL zink (Not recommended)
- Install required packages
```
pkg install x11-repo tur-repo
pkg install mesa-zink virglrenderer-mesa-zink
```
- Creating alias
```
echo 'alias zink="MESA_NO_ERROR=1 MESA_GL_VERSION_OVERRIDE=4.3COMPAT MESA_GLES_VERSION_OVERRIDE=3.2 GALLIUM_DRIVER=zink ZINK_DESCRIPTORS=lazy virgl_test_server --use-egl-surfaceless --use-gles &"' >> /data/data/com.termux/files/home/.bashrc
echo 'alias zink="MESA_NO_ERROR=1 MESA_GL_VERSION_OVERRIDE=4.3COMPAT MESA_EXTENSION_OVERRIDE=GL_EXT_polygon_offset_clamp GALLIUM_DRIVER=virpipe WINEDEBUG=-all"' >> /data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/ubuntu/root/.bashrc
source ~/.bashrc
```


