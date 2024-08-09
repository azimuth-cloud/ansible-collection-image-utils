# liunx-ansible-init

An initialisation system used to configure instances based on metadata that is given to the instance when it is created.

The ansible-init system consists of a script that is installed in the image and runs as a systemd service of type "oneshot". This service is enabled in the image so that it runs on first boot with no intervention. When executed, the script looks for all the Ansible playbooks in a specific directory and executes them in sort order. After all the playbooks have executed successfully, a sentinel file is written that prevents ansible-init from executing again on subsequent boots.

ansible-init is able to execute playbooks that are baked into the images, and also from arbitrary Ansible collections, e.g. from Galaxy or from a Git repository. These extra playbooks are specified by the Azimuth operator in their Azimuth configuration, and communicated to the instances that make up platforms using cloud-init instance metadata. This allows site- or platform-specific customisations to be applied to instances in a consistent way without modifying the images.

## Usage

The 255 byte limit per key/value pair for instance metadata means that collections will be defined by metadata items of the following structure:

```
ansible_init_coll_{0,1,2,...}_name
ansible_init_coll_{0,1,2,...}_source
ansible_init_coll_{0,1,2,...}_type
ansible_init_coll_{0,1,2,...}_version
```

where name, source, type and version correspond to the properties for a collection in an Ansible Galaxy requirements.yml file. The items for the same index define a single collection.

Similarly, the playbooks will be specified using metadata items of the form:

`ansible_init_pb_{0,1,2,...}_stage` - one of pre or post, defaults to post

`ansible_init_pb_{0,1,2,...}_name` - the name of the playbook

Playbooks in the pre stage will execute before any playbooks baked into the image, and those in the post stage will execute after.
