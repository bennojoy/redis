redis
=====

This role helps to deploy a Redis master or replication server on target host.
This roles sets several default values for Redis configuration which can be
overrriden by the user.

Requirements
------------

This role requires Ansible 1.4 or higher, and platform requirements are listed
in the metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows. See the documentation for Redis for details:

	redis_pidfile: /var/run/redis.pid 		# PID File
	redis_bind_address: "0.0.0.0" 			# The network address for redis to bind to
	redis_port: 6379 						# Port for the Redis server
	redis_unixsocket: null					# (Optional) Socket file
	redis_unixsocketperm: null				# (Optional) Socket permissions
	redis_syslog_enabled: "yes"				# enable_syslog
	redis_databases: 16 					# Set number of databases
	redis_database_save_times:          	# Save the DB on disk (seconds changes)
	  - [900, 1]
	  - [300, 10]
	  - [60, 10000]
	redis_dbfilename: dump.rdb 				# Filename for the db
	redis_db_dir: /var/lib/redis  			# DB Directory
	redis_role: master 						# Role for redis deployment (master/slave)
	redis_requirepass: false 				# If a password is required
	redis_pass: None  						# Password is requirepass is enabled
	redis_max_clients: 10000  				# Maximum number of clients allowed to connect
	redis_maxmemory: null					# (Optional) Maximum memory that Redis can use
	redis_maxmemory_policy: volatile-lru	
	redis_appendfsync: everysec
	redis_timeout: 0
	redis_loglevel: notice					# Loglevel
	redis_logfile: /var/log/redis.log 		# File to log to
	redis_hz: 10
	redis_tcp_keepalive: 0
	redis_syslog_ident: redis
	redis_disable_tcp_nodelay: no
	redis_appendonly: no
	redis_appendfilename: appendonly.aof

	If role is slave set these values too
	redis_master_ip: 1.1.1.1
	redis_master_port: 6379
	redis_master_auth: None
	redis_slave_serve_stale_data: yes
	redis_slave_read_only: yes
	redis_slave_priority: 100

Examples
--------

The following example sets up a master Redis server.

	- hosts: all
	  sudo: true
	  roles:
	  - {role: bennojoy.redis, redis_port: 11244}

The following example sets up a slave Redis server.

	- hosts: all
	  sudo: true
	  roles:
	  - {role: bennojoy.redis,
	     redis_role: 'slave',
	     master_ip: '192.168.2.10',
	     master_auth: 'foobar'}


Dependencies
------------

None

License
-------

BSD

Author Information
------------------

Benno Joy


