# codesys-control-linux-sl

This is a brief guide how to work with Codesys Control Linux SL Runtime in a Linux environment. The guide also explains how to make the Runtime run as a service.

1. Prepare a Linux machine, in this case a Proxmox CT container running Ubuntu 22.04
   
2. Activate SSH on Linux machine and test it
   
3. In Codesys IDE (development system). Go to tools and click on 'Update Linux'. If you dont see 'Update Linux', this has to bee added my going to tools => Customize. Then expand Tools => select empty row and click Add Command. Then scroll down to 'Runtime Deploy Tool' and select 'Update Linux'

4. Enter SSH username, password and IP address to your Linux machine and click on Install.

5. To verify install from Codesys IDE click on System Info 

6. To verify install on Linux machine. SSH to Linux machine and cd in to /var/opt. Here shall exist a folder called codesys with all necessary files.

7. Make Codesys runtime run as a service. Verify that codesyscontrol.service is NOT listed here systemctl list-units --type=service

8. Create service sudo nano /etc/systemd/system/codesyscontrol.service
[Unit]
Description=CODESYS SoftPLC
After=network.target

[Service]
ExecStart=/opt/codesys/bin/codesyscontrol.bin /etc/CODESYSControl.cfg
Restart=always
User=root

[Install]
WantedBy=multi-user.target

9. sudo systemctl daemon-reload

10. sudo systemctl start codesyscontrol

11. sudo systemctl enable codesyscontrol

12. Verify that codesyscontrol.service IS listed here systemctl list-units --type=service

13. Check status sudo systemctl status codesyscontrol

Now codesys runtime will restart automatically when demo period of 2 hour is reached.

Cheers
