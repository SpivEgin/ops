php
===

Install and configure php-fpm for lamp and lemp stack, add your own pools configurations, and customize all the php.ini config from yaml variables

Role Variables
--------------

```
# Choose packages to install
php_packages:
  - php5-fpm
  - php5-cli
  - php5-common
  - php5-imagick
  - php5-intl
  - php5-memcached
  - php5-mysql
  - php5-redis
  - php5-curl
  - php5-json
  - php5-gd
  - php5-xsl
  - php5-mongo
  - php-apc
  - newrelic-php5

# Define your own pools
php_pools:
  www:
    user: "www-data"
    group: "www-data"
    listen: "/var/run/php5-fpm.sock"
    listen.owner: "www-data"
    listen.group: "www-data"
    listen.allowed_clients: "127.0.0.1"
    pm: "dynamic"
    pm.max_children: "5"
    pm.start_servers: "2"
    pm.min_spare_servers: "1"
    pm.max_spare_servers: "3"
    pm.process_idle_timeout: "30s"
    pm.max_requests: "500"

# Custom php.ini configs
php_ini_custom:
  opcache:
    opcache.blacklist_filename: /etc/php5/fpm/opcache.blacklist

# Opcache blacklist
php_opcache_blacklist: []

# Php FPM basic configuration
php_fpm_pid: /run/php5-fpm.pid
php_fpm_error_log: /var/log/php5-fpm.log
php_fpm_syslog_facility: daemon
php_fpm_syslog_ident: php-fpm
php_fpm_log_level: notice
php_fpm_emergency_restart_threshold: 0
php_fpm_emergency_restart_interval: 0
php_fpm_process_control_timeout: 0
php_fpm_process_max: 128
php_fpm_process_priority: -19
php_fpm_daemonize: yes
php_fpm_rlimit_files: 1024
php_fpm_rlimit_core: 0
php_fpm_events_mechanism: epoll
php_fpm_systemd_interval: 10
php_fpm_pools_include: /etc/php5/fpm/pool.d/*.conf
```

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: jebovic.php }
```

License
-------

MIT

Author Information
------------------

Jérémy Baumgarth https://github.com/jebovic
