# CHANGELOG

## v22.03

* Updates `required_versions` for `packer` to `>= v1.8.0`.
* Updates `required_versons` for `terraform` to `>= v1.1.7`.
* Updates `required_versons` for `hashicorp/vsphere` to `>= v2.1.1`.

> Release Date: 2022-03-17

## Release v22.02

> Release Date: 2022-02-22

* Updates the configuration of Linux machine images to use the Ansible roles instead of shell scripts.
* Updates `required_versions` for `packer` to `>= v1.7.10`.
* Updates `required_versons` for `terraform` to `>= v1.1.5`.

## Release v22.01

> Release Date: 2022-01-21

* Updates the structure of the subdirectories in `builds/`.
* Updates `required_versions` for `packer` to `>= v1.7.9`.
* Updates `required_plugins` for `packer-plugin-vsphere` to `>= v1.0.3`.
* Updates `required_versons` for `terraform` to `>= v1.1.4`.
* Updates Microsoft Windows 11 Professional to use virtual trusted platform module (vTPM) and removes experimental project support. vTPM is now supported by `packer-plugin-vsphere` to `>= v1.0.3`.
* Updates VMware Photon OS 4.0 to [Revision 2](https://github.com/vmware/photon/wiki/Downloading-Photon-OS).
* Adds configurable data source provisioning for VMware Photon OS 4.0. Revision 2 adds support for secondary devices with kickstart. Edit the `common_data_source` in `common.pkvars.hcl` from `http` to `disk`. The build will attach an on-demand `.iso` as the secondary CD-ROM for the kickstart. This is useful for environments that can not use HTTP-based kickstart.
* Updates the `notes` to automatically include the Packer version and a `build_version`.
* Updates the naming for the machine image output and includes a `build_version` (_e.g._, `linux-photon-4-v22.01`).
* Updates all Microsoft Windows Server machine image builds to a default of 4096 MB of memory to increase performance during operating system patching.
* Adds a GitHub Action on pull requests to check code quality using linters.
* Updates all of project code to address issues found by the linter(s).

## Release v21.11

> Release Date: 2021-11-09

* Adds support for `cloud-init` and the `[VMware]` data source introduced in cloud-init v21.3 for Ubuntu Server 20.04 LTS

    **Important Note**: Uncomment these lines in the script for Ubuntu 20.04 and guest customization will be performed by VMware Tools vs. `cloud-init`.

    ```shell
    # Uncomment below if guest customization will be performed by VMware Tools.
    # touch /etc/cloud/cloud.cfg.d/99.disable-network-config.cfg
    # echo "network: {config: disabled}" >> /etc/cloud/cloud.cfg.d/99.disable-network-config.cfg
    ```

* Adds custom disk partitioning for Ubuntu Server 20.04 LTS and Ubuntu Server 18.04 LTS
* Updates Ubuntu 18.04 LTS to `efi-secure`.
* Updates all certificates to the PEM-encoded `.cer` format.
* Adds example Terraform plans for deployment testing.
* Adds an Ansible playbook example to create a custom role in vSphere for Packer.

## Release v21.10.01

> Release Date: 2021-10-20

* Updates `LICENSE` and `NOTICE` to BSD-2.
* Updates `required_versions` for `packer` to `>= v1.7.7`.
* Updates `required_plugins` for `packer-plugin-vsphere` to `>= v1.0.2`.
* Updates Linux distributions to generate new host keys on first-boot.
* Adds option to use`floppy_content` included in `packer-plugin-vsphere` release`v1.0.2`. Ubuntu Server 18.04 LTS will toggle to use `floppy_content` from `http_content` when `common_data_source = "disk"` is enabled.
* Updates VMware Photon OS 4.0 to Revision 1.
* Adds Microsoft Windows 11 Professional as experimental until `vsphere-iso` supports vTPM.
* Adds support for `skip_import` Adds to `packer-plugin-vsphere` in `v1.0.2`. When set to `true` the virtual machine will not be imported into the content library. This is useful for testing / debugging. Defaults to false.

## Release v21.10

> Release Date: 2021-10-11

* Adds the `config.sh` to create `config/*.prkvars.hcl` (default) files from the examples in `builds/`.
* Adds the option for create >1 set of configuration set by passing an argument to `config.sh` (_e.g._ `config.sh config/us-west-1`) and the pass the configuration set to `build.sh` (_e.g._ `build.sh config/us-west-1`).
* Use of the content library is now optional by updating the `config/common.pkvars.hcl` settings to the following:

    ```hcl
    common_template_conversion     = true
    common_content_library_name    = null
    common_content_library_ovf     = false
    common_content_library_destroy = false
    ```
* Adds support for a SOCKS proxy by editing `config/proxy.pkvars.hcl`.
* Adds the ability to set the IP address to bind the HTTP server by editing the `common_http_ip` in `config/common.pkvars.hcl` from `null` to an IP address on the Packer host:
    ```hcl
    common_http_ip = "172.16.11.100"
    ```
* Add configurable data source provisioning for Linux images. By default, HTTP is used for the kickstart. By editing the `common_data_source` in `config/common.pkvars.hcl` from `http` to `disk` the build will use a disk-based method, such as a `.iso` as the secondary CD-ROM. This is useful for environments that can not communicate back to the Packer host's HTTP server.
    ```hcl
    common_data_source = "disk"
    ```
* Renames all certificates to `*.ctr.example` and `*.pb7.example`. Please add your own custom certificates to the directories per the README.md.
* Adds the ability for Packer to be run from any directory by including the use of `$(path.cwd)/`.
* Adds the `ansible` provisioner to Linux builds for base configuration using roles. More updates to follow.
* Adds information on least privilege service account using a custom role in vSphere.
* Adds a Terraform example for creation of the custom role in vSphere.
* Updates `manifests` to use `manifests/` and a JSON output based on the timestamp.
* Updates `manifests` to use include relevant data in the JSON output for the build.
* Adds RHEL 7 and CentoOS 7 back to the builds per requests.
* Refactors RHEL and RHEL derivative kickstarts templates.
* Adds Windows 10 Professional.
* Updates PhotonOS to `efi-secure`.
* Updates Ubuntu 20.04 LTS to `efi-secure`.
* Adds vendor provided filename and checksums to the build examples.
* Updates CONTRIBUTING.md with the contributor workflow.
* Adds headers to various scripts and files, as needed.
* Add public keys and specific Terraform files to `.gitignore`.
* Updates issue templates to use forms.
* Various bugfixes and code cleanliness.
* Bumped Packer to `>= 1.7.6`.
* Thanks to the new contributors: @sestegra, @metabsdm, and @gcblack!

## Release v21.09.1

> Release Date: 2021-09-16

* Refactors issue templates to use GitHub custom issue forms.
* Refactors all builds to pass the language, keyboard, and timezone to the configuration files.
* Updates the Rocky Linux build to use UEFI; however without secure boot.
* Updates the defaults in `common.pkvars.hcl` to use hardware version 19, which provides the best performance and latest features available in ESXi 7.0 U2. Refer to the VMware vSphere 7.0 [product documentation](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-789C3913-1053-4850-A0F0-E29C3D32B6DA.html) if using a previous release
* Refactors all builds with input variable definitions separated into `variables.pkr.hcl`.
* Refactors all builds to use `<build>.auto.pkvars.hcl` for input variables the and `<build>.pkr.hcl` for the template configurations, with simplified names for `<build>`.
* Refactors all builds to use `${path.cwd}/output/` as the path for the manifest post-processor.
* Adds disclaimers and Updates descriptions in script files.
* Updates README.md.

## Release v21.09

> Release Date: 2021-09-07

* Adds support for Microsoft Windows Server 2022 machine image builds.
* Refactors configuration files to be generated using templates. Reduces the number of files and passes variables into the `.pkrtpl.hcl` content.
* Refactors builds for Linux distributions to use `http_content` instead of `http_directory` and `http_file`.
* Refactors builds for Microsoft Windows to use `cd_content` instead of `floppy_files`, which allows for use generated configuration files. A Packer compatible `.iso` command-line tool is required and noted in the [README.md](README.md#Requirements).
* Adds disclaimers and Updates descriptions in script files.
* Adds [NOTICE](NOTICE).
* Updates the `packer init` commands run in `build.sh`.
* Updates MAINTAINERS.md.
* Updates CONTRIBUTING.md.
* Updates README.md.

## Release v21.08

> Release Date: 2021-08-18

* Moves `vsphere.pkrvars.hcl` and `rhsm.pkrvars.hcl` to the `builds` directory.
* Isolates variables to simplify updates to common settings with `builds/common.pkrvars.hcl`.
* Refactors all build definitions to use variables and reduce any hard-coded settings.
* All machine image build definitions use the the recommended firmware based on the guest operating system and the minimum vSphere release supported by the repository. EFI Secure Boot is enabled for Red Hat Enterprise Linux 8, CentoOS Linux/Stream 8, AlmaLinux 8, and Microsoft Windows Server 2019/2016. BIOS is enabled Rocky Linux 8.
* Adds the manifest post-provisioner to machine image build definitions.
* Moves public keys to variables.
* Adds a user for Ansible to Linux machine images with authorized_keys. Uses `builds/ansible.pkrvars.hcl`. Password is randomized.
* Updates the Packer block to all builds with `required_versions >= "1.7.4"` for Packer.
* Adds the `required_plugins` to the Packer block for all builds to use the `vsphere` plugin `version = ">= v1.0.1"`.
* Updates the Packer block for Windows builds with `required_plugins` and `version = "0.14.0"` for the [Windows-Update plugin](https://github.com/rgl/packer-plugin-windows-update).
* All builds automatically run `packer init` to initialize required plugins before running a build with `build.sh`.
* Updates Microsoft Windows `autounattend.xml` files to use the attached VMware Tools `.iso` for PVSCSI driver.
* Simplified and reduced the script files used by provisioners.
* Patches the script for VNware Photon OS 4 due to an issue performing updates with `tdnf`.
* Patches the script for Ubuntu Server 20.04 LTS to remove cloud-init and remove all netplan configurations before GuestOS customization.
* Removes support for VMware Photon OS 3 machine image builds.
* Removes support for Red Hat Enterprise Linux 7 machine image builds.
* Removes support for CentOS Linux 7 machine image builds.
* Deprecates CentOS Linux 8. Removing in a future update. The CentOS Project [has shifted focus](https://www.redhat.com/en/blog/faq-centos-stream-updates) from CentOS Linux to CentOS Stream. CentOS Linux 8 EOL: `2021-12-31`.
* Deprecating Microsoft Windows Server 2016. Removing in a future update. Microsoft Windows Server 2016 EOL: `2022-01-22`.
* Adds MAINTAINERS.md.
* Updates README.md.

## Release v21.07

> Release Date: 2021-07-21

* Adds support for [VMware Photon OS](https://vmware.github.io/photon/) 4.
* Adds [support](https://github.com/vmware-samples/packer-examples-for-vsphere/issues/18) for [AlmaLinux](http://almalinux.org) 8.
* Adds [support](https://github.com/vmware-samples/packer-examples-for-vsphere/issues/13) for [Rocky Linux](https://rockylinux.org) 8.
* Adds [support](https://github.com/vmware-samples/packer-examples-for-vsphere/issues/19) for [CentOS Stream](https://www.centos.org/centos-stream/) 8.
* Updates to `>=` vSphere 7.0 U2.
* Adds the Packer block to all builds with `required_versions >= "1.7.3"` for Packer.
* Adds the Packer block for Windows builds with `required_plugins` and `version = "0.12.0"` for the [Windows-Update plugin](https://github.com/rgl/packer-plugin-windows-update).

## Release v20.11

> Release Date: 2020-11-26

* Initial release.
