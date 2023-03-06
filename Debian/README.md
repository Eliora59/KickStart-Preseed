# Documentation preseed

## Permettre le choix de la langue d'installation
d-i debian-installer/locale string fr_FR

## Permet le choix du clavier
d-i console-keymaps-at/keymap select fr  
d-i keyboard-configuration/xkb-keymap select fr(latin9)  

## Permettre la sélection automatique de l'interface réseau
d-i netcfg/choose_interface select auto

## Permet de mettre un choix sur le nom d'hôte
d-i netcfg/get_hostname string DEB-SRV

## Permet la configuration du domaine
d-i netcfg/get_domain string overcomputing.net

## Configuration des mirroirs
d-i mirror/country string manual  
d-i mirror/http/hostname string http.us.debian.org  
d-i mirror/http/directory string /debian  
d-i mirror/http/proxy string  

## Permet de sélectionner le type de distribution 
d-i mirror/suite string stable

## Permet la configuration des repos non-free et contrib
d-i apt-setup/non-free boolean true  
d-i apt-setup/contrib boolean true  

## Permet la configuration du fuseau horaire
d-i clock-setup/utc boolean true  
d-i time/zone string Europe/Paris  

## Permet la configuration du ntp
d-i clock-setup/ntp boolean false

## Configuration du partitionnement
d-i partman-auto/method string regular  
d-i partman-auto/choose_recipe select atomic  
d-i partman/confirm_write_new_label boolean true  
d-i partman/choose_partition select finish  
d-i partman/confirm boolean true  
d-i partman/confirm_nooverwrite boolean true  

## Configuration du compte root
d-i passwd/root-password password root  
d-i passwd/root-password-again password root  
d-i passwd/make-user boolean false  

## Configuration des utilisateurs
d-i passwd/user-fullname string theophile  
d-i passwd/username string theophile  
d-i passwd/user-password password root  
d-i passwd/user-password-again password root  

## Eviter le scan de médias supplémentaires
d-i apt-setup/cdrom/set-first boolean false                                   
d-i apt-setup/cdrom/set-next boolean false                                   
d-i apt-setup/cdrom/set-failed boolean false  

## Permet de répondre à l'enquête de popularité des packages
popularity-contest popularity-contest/participate boolean false

## Permet la configuration de l'environnement
tasksel tasksel/first multiselect standard

## Permet l'ajout de packages supplémentaires
d-i pkgsel/include string openssh-server build-essential open-vm-tools vim

## Installation de grub
d-i grub-installer/only_debian boolean true  
d-i grub-installer/bootdev string /dev/sda  

## Permet l'extinction de la machine après installation
d-i debian-installer/exit/poweroff boolean true  
d-i finish-install/reboot_in_progress note  

## Permet d'exécuter des post-actions sur la machine
d-i preseed/late_command string in-target sh -c "echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config"; in-target /etc/init.d/ssh restart