Configure a k3s node to be a worker node and join it on the cluster
=========

This role can be used together with:

  - https://github.com/lucaslehnen/k3s-install -> prepare
  - https://github.com/lucaslehnen/k3s-config-master -> Master node
  - https://github.com/lucaslehnen/k3s-reset -> Reset

Configure the variables
-----------------------

`master_ip` :  

The k3s master node IP;

`extra_agent_args` : 

Extra args that can be passed to the service. 
Check the k3s documentation: https://rancher.com/docs/k3s/latest/en/installation/install-options/agent-config/

Example
----------------

In your `main.yml`:

```yaml
  - hosts: workers
    roles:
        - k3s-config-worker
    vars:
      master_ip: "192.168.99.11"
      extra_agent_args: ""
```

In your `requirements.yml`:

```yaml
  - name: k3s-config-worker
    src: https://github.com/lucaslehnen/k3s-config-worker
    version: 1.0.0
```

Define target hosts in your inventory file `hosts`:

    [workers]    
    192.168.99.12
    192.168.99.13

Install requirements:

```
ansible-galaxy install -r requirements.yml
```

Call the playbook:

    ansible-playbook -i hosts main.yml

License
-------

MIT

Author
------------------

https://github.com/lucaslehnen
