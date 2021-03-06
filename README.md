# manage-openconnect

Small script I wrote myself to start and manage an openconnect vpn interface.

Using iwd I had problems finding a wrapper program managing a vpn interface, so
I quickly build my own.

For now the script only supports openconnect as an executable, but everything
can be configured from a config file.

Hint: Make sure you properly configure openconnect. I had to use another
vpn-script, as I was always getting weird errors. I saved it to
`/etc/vpnc/vpnc-script-new` and invoke it by passing
`--script=/etc/vpnc/vpnc-script-new` to `openconnect`. Make sure you find one
that works for you.

# Usage:

Simply use

```sh
vpn start
```

to start a connection and

```sh
vpn stop
```

to stop a connection. Just invoking

```sh
vpn
```

or

```sh
vpn status
```

prints the status of the connection (either ON or OFF).

# Configuration

The default configuration file location is
`$XDG_CONFIG_HOME/vpn-script/config`, which is just a simple shell script.

Simply define all the variables you want to overwrite in here. Variable you
need to overwrite are:

- `HOST`
- `REMOTE_USER`
- `PASSWORD`

Optionally you can also overwrite

- `INTERFACE`, to change the interface name
- `PID_FILE`, to use a custom pif-file path
- `START_VPN`, to use a custom executable to start a connection (make sure to
  configure it properly)
- `STOP_VPN`, to interupt the running vpn executable

An alternative config file can be passed via `--config <file>`.

# Using a password manager

Remember you can use any shell command in the configuration file. So using
something like

```sh
PASSWORD_CMD="pass $PASS_PATH | head -n1"
PASSWORD=`eval $PASSWORD_CMD`
```

would suffice, where `PASS_PATH` is the password path in the pass repository.
