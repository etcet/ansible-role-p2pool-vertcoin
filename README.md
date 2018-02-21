## About

An ansible role which installs vertcoind and p2pool-vtc on CentOS 7.

An example play, which also uses https://github.com/etcet/ansible-role-firewalld to open ports.

    - hosts: all
      user: root
      roles:
        - role: ansible-role-firewalld
          firewalld_allowed_ports:
            - '5889/tcp'
            - '9171/tcp'
            - '9181/tcp'
            - '9346/tcp'
            - '9347/tcp'
        - role: ansible-role-p2pool-vertcoin
          vertcoin_rpc_user: 'rpcuser'
          vertcoin_rpc_pass: 'MyBijv6CZt7NMjXMYqmcL9LMrT5oRE'
          vertcoin_download_bootstrap: True

On initial setup, it'll take several hours to download and load the blockchain from the bootstrap.dat. During this time, vertcoind will have high CPU usage and the p2pool sites will not load.

Once it's all loaded and you can load your p2pool sites on ports 9171 and 9181, you should re-run the play without vertcoin_download_bootstrap so that the bootstrap.dat.old file gets removed.

## Defaults

You should change vertcoin_rpc_user and vertcoin_rpc_password.

    vertcoin_rpc_user: rpcuser
    vertcoin_rpc_password: rpcpassword

You should set this to true for the first run only so that a bootstrap.dat file is downloaded which improves the initial blockchain sync time.

    vertcoin_download_bootstrap: False

The author fee is the percent of shares to donate to the vertcoin developers. The admin fee

    vertcoin_author_fee: 1
    vertcoin_admin_fee: 1

There are separate addresses and minimum difficulties for each network, if you like.

    vertcoin_admin_address_1: 'Vg96gBBBENPojYwRr1gTRfgFS5d5Ru1wKC'
    vertcoin_min_difficulty_1: 16
    vertcoin_admin_address_2: 'Vg96gBBBENPojYwRr1gTRfgFS5d5Ru1wKC'
    vertcoin_min_difficulty_2: 8


