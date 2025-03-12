# ansible-redis-sentinel

Ansible Playbook to deploy a High Availability Redis with Sentinel

## Getting started

1. Create 3 servers (Vagrant VMs) with public-key authentication
    ```bash
    vagrant up
    ```
2. Copy `vars.yml.example` to `vars.yml`. Replace `<YOUR_PASSWORD>` with a secured password
3. Copy SSH keys
   ```bash
   mkdir ssh_keys
   cp .vagrant/machines/vm1/virtualbox/private_key ssh_keys/private_key_vm1
   cp .vagrant/machines/vm2/virtualbox/private_key ssh_keys/private_key_vm2
   cp .vagrant/machines/vm3/virtualbox/private_key ssh_keys/private_key_vm3
   ``` 
4. Edit `inventory` file and replace `<SERVER_01_IP>`, `<SERVER_02_IP>` and `<SERVER_03_IP>` with the corresponding IP address for each server.
5. Run playbook `setup-redis-sentinel.yml`

    ```bash
    ansible-playbook setup-redis-sentinel.yml -i inventory
    ```

## Notice

1. The configuration for Redis and Sentinel are defined in `redis.conf.j2` and `sentinel.conf.j2`. The playbook explicitly uses `:` to separate each line and use `regexp` to update the corresponding file on the server. Therefore, the playbook will only touch the necessary setting and doesn't modify any other default settings.
2. Make sure that the `role` in `inventory` is correct before running the playbook. For example, if the Sentinel changes the master to a replica. You need to change the `role` to match the current master-replica setup. Otherwise, the playbook will mess up the setting of Sentinel.
