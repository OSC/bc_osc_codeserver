# Batch Connect - OSC Code Server

![GitHub Release](https://img.shields.io/github/release/osc/bc_osc_codeserver.svg)
[![GitHub License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)

An improved file viewer / editor for OSC OnDemand that launches a
Code Server within an Owens batch job. Code Server leverages VSCode as its
editor.

## Prerequisites

This Batch Connect app requires the following software be installed on the
**compute nodes** that the batch job is intended to run on (**NOT** the
OnDemand node):

- [Lmod] 6.0.1+ or any other `module purge` and `module load <modules>` based
  CLI used to load appropriate environments within the batch job before
  launching Code server.
- [Code Server] 2.x+ available from Github: https://github.com/cdr/code-server/releases

[Code Server]: https://coder.com/
[Lmod]: https://www.tacc.utexas.edu/research-development/tacc-projects/lmod
[VS Code]: https://code.visualstudio.com/

## Install

1. Use Git to clone this app and checkout the desired branch/version you want to
use and place this wherever you store batch connect apps (`/var/www/ood/apps/sys` or `~/ondemand/dev`):

    ```sh
    scl enable git29 -- git clone <repo>
    cd <dir>
    scl enable git29 -- git checkout <tag/branch>
    ```

2. Deloy code-server on your systems.

    ```sh
    # replace URL with latest release from code-server
    wget https://github.com/cdr/code-server/releases/download/3.4.1/code-server-3.4.1-linux-amd64.tar.gz
    tar -xzf code-server-3.4.1-linux-x86_64.tar.gz
    mv code-server-3.4.1-linux-x86_64 code-server
    ```
    
3. You will notice code-server is an executable inside that directory and can get the full path: 
    
    ```sh
    $ readlink -f code-server
    /users/PZS0562/efranz/code-server/bin/code-server
    ```

4. Update the path to the code-server binary in the script https://github.com/OSC/bc_osc_codeserver/blob/d44f805289557482ad682ee63d4074273f6a1a68/template/script.sh.erb#L23:

    ```diff
     # An arbitrary path...
    - CODE_SERVER="${CODE_SERVER:-/usr/local/code-server/bin/code-server"
    + CODE_SERVER="/users/PZS0562/efranz/code-server/bin/code-server"
    ```

5. Update form.yml to use the correct cluster, and any other changes as necessary to form.yml or submit.yml that is appropriate for your cluster.

## Update

To update the app you would:

```sh
cd <dir>
scl enable git29 -- git fetch
scl enable git29 -- git checkout <tag/branch>
```

Again, you do not need to restart the app as it isn't a Passenger app.

## Known Issues

- The authentication provided by code-server is unencrypted

## Contributing

1. Fork it ( https://github.com/OSC/bc_osc_codeserver/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
