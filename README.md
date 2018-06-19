# Ansible-network_ospf

Ansible role that configures ospf global and interface settings on network devices.  

The configuration of the role is done so that it shouldn't be necessary to modify the role for any configuration.
All settings can be configured by changing role parameters or by declaring new config as variable.

Please report any issues or send PR.

nxos specific: feature ospf has to be enabled. To remove an existing authentication configuration you should use 

## Examples

```yaml
---
- name: Example of how to configure ospf global settings
  hosts: sw1
  vars:
    vrfs:
      1:
        name: dev                         # the name default is a valid vrf representing the global default vrf 
        ospf:          
          ospf_id: dev1                   # by default uses the vrf 'name' var defined above if this is not defined. 
          state: present            
          router_id: 10.11.1.1
          auto_cost: 1000000              # value is integer representing Mbps
          def_metric: 10
          log_adj: log                    # controls level of log messages when a neighbor changes state. values log/detail/default
          passive_interface: true
# configure specific lsa/spf settings:  
          #timer_throttle_lsa_hold:
          #timer_throttle_lsa_max:
          #timer_throttle_lsa_start:
          #timer_throttle_spf_hold:
          #timer_throttle_spf_max:
          #timer_throttle_spf_start:          
  roles:
    - Ansible-network_ospf

```

## Role variables

```yaml
---
# Define the ospf global and interface settings to be configured (see README for examples)
vrfs: { }
interfaces: { }
```


## License

Apache


## Author

Dan Murarasu