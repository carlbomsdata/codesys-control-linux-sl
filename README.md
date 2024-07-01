# codesys-control-linux-sl

This is a brief guide how to work with Codesys Control Linux SL Runtime in a Linux environment. The guide also explains how to make the Runtime run as a service.

1. Prepare a Linux machine, in this case a Proxmox CT container running Ubuntu 22.04
   
2. Activate SSH on Linux machine and test it
   
3. In Codesys IDE (development system). Go to tools and click on 'Update Linux'. If you dont see 'Update Linux', this has to bee added my going to tools => Customize. Then expand Tools => select empty row and click Add Command. Then scroll down to 'Runtime Deploy Tool' and select 'Update Linux'

4. Enter SSH username, password and IP address to your Linux machine and click on Install.

5. To verify install from Codesys IDE click on System Info 

6. To verify install on Linux machine. SSH to Linux machine and cd in to '/var/opt'. Here shall exist a folder called codesys with all necessary files.

7. Make Codesys runtime run as a service. Verify that codesyscontrol.service is NOT listed here
``` bash
systemctl list-units --type=service
```

9. Create service
``` bash
sudo nano /etc/systemd/system/codesyscontrol.service
```

``` bash
[Unit]
Description=CODESYS SoftPLC
After=network.target

[Service]
ExecStart=/opt/codesys/bin/codesyscontrol.bin /etc/CODESYSControl.cfg
Restart=always
User=root

[Install]
WantedBy=multi-user.target
```

9. Reload services configuration
``` bash
sudo systemctl daemon-reload
```

11. Start service
``` bash
sudo systemctl start codesyscontrol
```

13. Enable service
``` bash
sudo systemctl enable codesyscontrol
```

15. Verify that codesyscontrol.service IS listed here
``` bash
systemctl list-units --type=service
```

17. Check status
``` bash
sudo systemctl status codesyscontrol
```

Now codesys runtime will restart automatically when demo period of 2 hour is reached.

Cheers
