FROM archlinux/base

WORKDIR /opt/oomox-gtk-theme
VOLUME /opt/oomox-gtk-theme/test_results
ENTRYPOINT /bin/bash

# App dependensies:
RUN echo "Update arch deps 2019-03-02" && \
    echo -e 'Server = http://archlinux.cu.be/$repo/os/$arch\nServer = http://mirror.metalgamer.eu/archlinux/$repo/os/$arch' > /etc/pacman.d/mirrorlist && \
    pacman -Syu --noconfirm && \
    pacman -S --needed --noconfirm bash grep sed bc glib2 gdk-pixbuf2 sassc gtk-engine-murrine gtk-engines gtk3 make && \
    rm -fr /var/cache/pacman/pkg/ /var/lib/pacman/sync/

# Test dependencies:
RUN pacman -Syu --noconfirm && \
    pacman -S --needed --noconfirm git base-devel && \
    useradd -m user && \
    echo "user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    sudo -u user bash -c "\
        git clone https://aur.archlinux.org/awf-git /home/user/awf && \
        cd /home/user/awf && \
        makepkg --install --syncdeps --noconfirm" && \
    pacman -S --needed --noconfirm ttf-roboto scrot xorg-server-xvfb libfaketime xdotool parallel gnome-themes-extra adwaita-icon-theme openbox xorg-xrdb xorg-xsetroot imagemagick shellcheck && \
    rm -fr /var/cache/pacman/pkg/ /var/lib/pacman/sync/

# Debug dependencies:
#RUN pacman -S --needed --noconfirm fish

COPY . /opt/oomox-gtk-theme/
