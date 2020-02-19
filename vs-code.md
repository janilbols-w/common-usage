# VS Code
## Remote version installation.

https://code.visualstudio.com/docs/remote/faq

### via ssh
https://code.visualstudio.com/remote-tutorials/ssh/getting-started

### via ssh + jumper
- Use case
  - A <--   ok   --> B
  - B <--   ok   --> C
  - A <-- NOT ok --> C
  - Here you are trying to use A to access C (remote-server) via B (Jumper)
- Instruction
  - Modify config file```C:\Users\username\.ssh\config```
    ```
    # Read more about SSH config files: https://linux.die.net/man/5/ssh_config
    Host Jumper
        HostName 1.1.1.1 # ip for jumper
        User [username] # username on jumper
        Port 22 # ssh port for jumper

    Host remote-server
        Hostname 2.2.2.2 # ip for remote-server
        User [username] # username on remote-server
        Port 22
        ProxyCommand C:\Windows\System32\OpenSSH\ssh.exe -W %h:%p Jumper
    ```
  - Okay to access remote-server
    - you will need to type in key4Jumper, then key4Remote-server
