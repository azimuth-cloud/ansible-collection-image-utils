# liunx-ansible-init

An initialisation system used to configure instances based on metadata that is given to the instance when it is created.

The ansible-init system consists of a script that is installed in the image and runs as a systemd service of type "oneshot". This service is enabled in the image so that it runs on first boot with no intervention. When executed, the script looks for all the Ansible playbooks in a specific directory and executes them in sort order. After all the playbooks have executed successfully, a sentinel file is written that prevents ansible-init from executing again on subsequent boots.
