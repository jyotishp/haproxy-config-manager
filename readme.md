# HAProxy Configuration Manager
HAProxy uses a single configuration file which makes it too difficult to manage a large number of domains. This tool will (hopefully) help in managing the configuration with ease.

## Initial Setup
Clone the repository
```git clone https://github.com/jyotishp/haproxy-config-generator.git```

Modify the `header.cfg` file to include all your required defaults. Make sure to change the path to SSL certificate file to the right one.

Make sure there is some file (at least an empty one) with the name `haproxy.cfg` in the `conf.d` directory.

Create a symbolic link of `haproxy.cfg` to `/etc/haproxy/haproxy.cfg`
```sudo ln -s `pwd`/conf.d/haproxy.cfg /etc/haproxy/haproxy.cfg```

### Optional
In case you want to have a separate directory to save your configuration, open the file haconf with any text editor and change the line `base_dir = './conf.d/'` to `base_dir = 'path_to_conf_directory/'`. If you are doing this, the symbolic link for actual configuration file should be changed accordingly.

You can also consider adding `haconf` to `/usr/bin` or `/bin` for ease of use. But in this case make sure you modify `base_dir` variable to appropriate configuration directory path in the script.

## How to use
### Managing Domains
#### Adding a domain
```haconf domain add <domain> <port_number> <list_of_space_seperated_IPs>```
For example, if you want to add example.iiit.ac.in pointing to 127.0.0.1 listening on port 80
```haconf domain add example.iiit.ac.in 80 127.0.0.1```

#### Deleting a domain
```haconf domain del <domain>```

#### Listing loaded domains
```haconf domain list```


# Caution
- Work is still in progress for adding ACL rules.
- As of now, the script only handles 80 and port 443.
- Everyting on port 80 is redirected to 443 on haproxy (this won't effect the reverse proxy behaviour).