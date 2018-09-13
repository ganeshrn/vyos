# Load configuration into device
The `load` function provides a means to load a configuration file onto a
target device running VYOS. The `load` function provides configuration
values that allow the source configuration to either be merged with the
current active configuration (default) or to replace the current active
configuration on the device.  


## How to load a configuration
Loading a configuration onto a target device is fairly simple and
straightforward. By default, the `load` function will merge the
contents of the provided configuration file with the configuration running on
the target device.  

Below is an example of how to call the `load` function.

```
- hosts: vyos
  
  roles:
    - name: ansible-network.vyos
      function: config_manager/load
      config_file: vyos.cfg
```

The example playbook above will simple load the contents of `vyos.cfg` onto the
target network devices.

### How to load and replace a configuration
The `load` function also provides support for replacing the current
configuration on a device.

In order to replace the configuration, the function as before but adds the
value `replace: yes` to the playbook to indicate that the configuration should
be replace.

Note: Take caution when doing configuration replace that you do not
inadvertantly replace your access to the device.

```
- hosts: vyos

  roles:
    - name: ansible-network.vyos
      function: config_manager/load
      config_file: vyos.cfg
      replace: yes
```

## Arguments

### vyos_config_replace

This value enables or disables the configuration replace feature of the
function. In order to use `vyos_config_replace` the target device must
support config replace function.

The default value is `False`

#### Aliases
* replace

### vyos_config_file

This required value provides the path to the configuration file to load when
the function is called. The path to the file can either be provided as
relative to the playbook root or an absolute path.  

The default value is `null`

This value is *required*

#### Aliases

* config_file

### vyos_config_remove_temp_files

Configures the function to remove or not remove the temp files created when
preparing to load the configuration file for replace. There are two locations
for temp files, one on the Ansible controller and one on the device. This
argument accepts a boolean value.

The default value is `True`

##### Aliases

* remove_temp_files