# Installing OpenVino toolkit on Red Hat Enterprise Linux 7.7

This procedure has been adapted from the Centos 7.4 installation:

* [https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_linux.html](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_linux.html)
* [https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_yum.html](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_yum.html)

## Installing the host

* Install a RHEL 7.7 (in my case in a Lenovo ThinkPad x240).
* Set release to 7.7:

```
# subscription-manager release --set=7.7
```
* Update and reboot if necessary:

```
# yum update -y
```
* Follow [https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_yum.html](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_yum.html) to install OpenVino toolkit from Intel RPMs repository.

* Configure EPEL:

```
# wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# yum install epel-release-latest-7.noarch.rpm
```

* Download and install these RPMS:

  * **freebidi** from RHN or from [rpmfind](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/fribidi-1.0.2-1.el7.x86_64.rpm).
  * **lib64va1** from [rpmfind](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libva-1.8.3-1.el7.x86_64.rpm).
  * **lib64wayland-client0** from [rpmfind](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libwayland-client-1.15.0-1.el7.x86_64.rpm).

```
# yum install fribidi-1.0.2-1.el7.x86_64.rpm libva-1.8.3-1.el7.x86_64.rpm libwayland-client-1.15.0-1.el7.x86_64.rpm
```

## Installing OpenVino

* Install openvino dependencies:

```
# cd /opt/intel/openvino/install_dependencies
# ./install_openvino_dependencies.sh 
...
No package glibc-static available.
...
No package libstdc++-static available.
...
Add third-party RPM Fusion repository and install FFmpeg package (y/n): y
...
[root@neurotic install_dependencies]# 
#
```

> NOTE: if needed [glibc-static for i686](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libstdc++-static-4.8.5-39.el7.i686.rpm), [glib-static for x86_64](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libstdc++-static-4.8.5-39.el7.x86_64.rpm), [libstdc++-static for i686](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libstdc++-static-4.8.5-39.el7.i686.rpm) and [libstdc++-static for x86_64](https://rpmfind.net/linux/centos/7.7.1908/os/x86_64/Packages/libstdc++-static-4.8.5-39.el7.x86_64.rpm).

## Configure the model optimizer

* Install model-optimizer:

```
# yum install intel-openvino-model-optimizer
```

* Create an user a give it sudo privileges:

```
# cat /etc/sudoers.d/jadebustos 
jadebustos	ALL = ( root ) NOPASSWD:ALL
# 
```

* Go to __cd /opt/intel/openvino/deployment_tools/model_optimizer/install_prerequisites/__ and make a backup of the file:

```
# cp install_prerequisites.sh install_prerequisites.sh.bck
```

* To run in Red Hat Enterprise Linux you will need to modify the __install_prerequisites.sh** script it to consider RHEL as centos:

```
if [[ -f /etc/centos-release ]]; then
    DISTRO="centos"
elif [[ -f /etc/lsb-release ]]; then
    DISTRO="ubuntu"
elif [[ -f /etc/redhat-release ]]; then
    DISTRO="centos"
fi
```

* As a non-root user go to the Model Optimizer prerequisites directory and configure the model optimizer:

```
$ cd /opt/intel/openvino/deployment_tools/model_optimizer/install_prerequisites
$ sudo ./install_prerequisites.sh
...
[WARNING] All Model Optimizer dependencies are installed globally.
[WARNING] If you want to keep Model Optimizer in separate sandbox
[WARNING] run install_prerequisites.sh venv {caffe|tf|mxnet|kaldi|onnx}
$
```

## Install omz

* Install:

```
# yum install intel-openvino-omz-tools intel-openvino-omz-dev intel-openvino-omz
```
