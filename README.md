Role Name
=========

A role to bootstrap fresh install of Ubuntu on Raspberry Pi 4 board.
Multiple functionalities can be enabled such as but not limited to:

  * Insallation of arbitrary list of packages
  * Cloning of dotfiles repo
  * Cloning of other repo such as media center project
  * Docker installation
  * Desktop environment installation
  * VNC server installation
  * Tailscale VPN setup and node registration
  * Setup of zRAM SWAP
  * root disk TRIM
  * Borgmatic backup to Borgbase repo
  * and more

Get from Ansible Galaxy: https://galaxy.ansible.com/pentago/rpi_bootstrap_ansible_role

Example Playbook
----------------

    - name: Bootstrap Raspberry Pi 4
      hosts: rpi
      become: true
      become_flags: -E
      gather_facts: false
      roles:
        - pentago.rpi_bootstrap_ansible_role

      vars:

        # Setup Host
        hostname: rpi
        locale: en_US.UTF-8
        timezone: Europe/Belgrade
        ntp_server: time.cloudflare.com
        ubuntu_dist: jammy

        # Setup Mount Points
        root_disk_label: writable
        storage_disk_label: STORAGE-1
        aux_storage_disk_label: STORAGE-2

        # Setup User
        user: ubuntu
        uid: 1000
        password: "some password"
        password_salt: f2tq74rufu5ixnf
        pub_ssh_key: id_ed25519.pub
        dotfiles_repo: git@github.com:user/dotfiles.git
        dotfiles_dir: dotfiles

        # Setup Docker
        setup_docker: true

        # Setup Desktop Environment
        setup_desktop: true
        setup_vnc: true
        vnc_session: gnome-session
        vnc_geometry: 1680x1050
        vnc_depth: 32
        vnc_passwd: "somepass"

        # Setup zRAM
        setup_zram: true
        zram_algo: zstd
        zram_percent: "50"
        zram_priority: "100"

        # Setup Tailscale
        setup_tailscale: true
        tailscale_auth_key: "tskey-kzg9gk6CTRLA-bQSgMdPPdZgxu1FECiNCo5"

        # Setup Git Repos
        project_repo: git@github.com:user/media-center.git
        project_data_dir: /data
        project_storage_dir: /storage-1
        aux_storage_dir: /storage-2

        # Setup Borgmatic
        setup_borgmatic: true
        borgbase_passphrase: "some passphrase"
        borgbase_user: repouser
        borgbase_repo: repouser.repo.borgbase.com
        borgbase_ssh_key: borgbase.key
        borgbase_healthcheck_url: https://hc-ping.com/27121397-a6d8-09ba-81b4-1f7770f887f9

        # Setup SSD TRIM
        # https://www.jeffgeerling.com/blog/2020/enabling-trim-on-external-ssd-on-raspberry-pi
        setup_trim: true

        # Setup Packages
        install_packages:
          - zsh
          - tmux
          - neovim
          - fzf
          - git
          - htop
          - exfat-fuse
          - exfatprogs
          - ncdu
          - ranger
          - rsync
          - iotop
          - localepurge
          - dphys-swapfile
          - gnupg
          - lsscsi
          - sg3-utils
          - net-tools
          - parallel
          - python3-llfuse
          - ripgrep
          - sdparm
          - libsensors5

        purge_packages:
          - snapd

        reboot: true

License
-------

MIT
