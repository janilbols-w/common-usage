# Create a ssh tunnel as proxy
device A || has no internet access
proxy-server B || has internet access

## origin env:
  A <-ssh-> B
# create a proxy for A via B
  A -> B <-> Internet
  - setup ssh:
    ssh -D [port] username@proxy-server
    keep this terminal，ssh to proxy-server
# usage of ssh tunnel
  - apt:
      - vim /etc/apt/apt.conf.d/proxy.conf
      - add the containt below:
        - Acquire::http::Proxy "socks5h://localhost:[port]";

  - git:(only work within the current git folder)
      - git config --global http.proxy "socks5h//localhost:[port]"
      - git config --global https.proxy "socks5h//localhost:[port]"
  - pip:
      - pip install [pkg-name] --proxy=='socks5h//localhost:[port]'
  - conda:
      - vim ~/.condarc
  - docker:
    - reference: https://docks.docker.com/config/daemon/systemd/
    - $ sudo mkdir -p /etc/systemd/system/docker.service.d
    - $ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf
    - $ sudo vim /etc/systemd/system/docker.service.d/https-proxy.conf
    - Add proxy into file http-proxy.conf & https-.proxy.conf
      ```
      [Service]
      Environment="HTTP_PROXY=socks5://localhost:[port]/"
      ```
      ```
      [Service]
      Environment="HTTPS_PROXY=socks5://localhost:[port]/"
      ```
    - $ sudo systemctl daemon-reload
    - $ sudo systemctl restart docker
    - $ systemctl show --property=Environment docker
