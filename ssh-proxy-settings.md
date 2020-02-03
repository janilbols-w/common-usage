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
  -apt:
      vim /etc/apt/apt.conf.d/proxy.conf
      add the containt below:
        Acquire::http::Proxy "socks5h://localhost:[port]";

  - git:(only work within the current git folder)
      - git config --global http.proxy "socks5h//localhost:[port]"
      - git config --global https.proxy "socks5h//localhost:[port]"
  - pip:
      - pip install [pkg-name] --proxy=='socks5h//localhost:[port]'
  - conda:
      - vim ~/.condarc
