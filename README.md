# Batch Connect - OSC Code Server

![GitHub Release](https://img.shields.io/github/release/osc/bc_osc_codeserver.svg)
[![GitHub License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)

An improved file viewer / editor for OSC OnDemand that launches a
Code Server within a batch job. Code Server leverages VSCode as its
editor.

## Prerequisites

This Batch Connect app requires the following software be available on the
**compute nodes** that the batch job is intended to run on (**NOT** the
OnDemand node):

- [Spack](https://spack.io) must be installed to a location available to compute nodes, such as a shared storage drive.
    - The spack installation must also have a [spack environment](https://spack-tutorial.readthedocs.io/en/latest/tutorial_environments.html) called `codeserver` with a `code-server` executable installed. This setup has been used with `code-server@4.12.0` succesfully.
    - This repo includes a spack environment definition file that can be used to set up a working spack environment, `spack-environment/codeserver/spack.yml`.
    - It may be necessary to change the `. /shared/spack/share/spack/setup-env.sh` line in the `template/script.sh.erb` if your spack installation is located somewhere other than `/shared/spack`

## Known Issues

- In-app installation of extensions does not work
- The authentication provided by code-server is unencrypted

## Contributing

1. Fork it ( https://github.com/OSC/bc_osc_codeserver/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
