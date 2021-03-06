<h1 align="center"> miqsel</h1>
<h3 align="center">Miq Selenium Server</h3>

<p align="center">
<a href="https://pypi.org/project/miqsel"><img alt="Python Versions"
src="https://img.shields.io/pypi/pyversions/miqsel.svg?style=flat"></a>
<a href="https://github.com/digitronik/miqsel/actions?query=workflow%3A%22%F0%9F%95%B5%EF%B8%8F+Test+suite%22"><img alt="Build Status"
src="https://github.com/digitronik/miqsel/workflows/%F0%9F%95%B5%EF%B8%8F%20Test%20suite/badge.svg"></a>
<a href="https://github.com/digitronik/miqsel/blob/master/LICENSE"><img alt="License: GPLV3"
src="https://img.shields.io/pypi/l/miqsel.svg?version=latest"></a>
<a href="https://pypi.org/project/miqsel/#history"><img alt="PyPI version"
src="https://badge.fury.io/py/miqsel.svg"></a>
<a href="https://pepy.tech/project/miqsel"><img alt="Downloads"
src="https://pepy.tech/badge/miqsel"></a>
<a href="https://pypi.org/project/black"><img alt="Code style: black"
src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>

Simple command line application to spin [selenium container](http://quay.io/redhatqe/selenium-standalone) and provide `vnc` access.


### Prerequisite:
1. **Podman/Docker**:

    Make sure `podman` or `docker` running on your system.
    - [Podman Installation](https://podman.io/getting-started/installation.html)
    - [Docker Installation](https://docs.docker.com/engine/install/)

2. **VNC Viewer**:

    You can choose any vnc viewer but most of user used _tigervnc_.
    - Fedora:
        ```
        sudo dnf install tigervnc
        ```
    - [TigerVNC link for other Distro's](http://tigervnc.bphinz.com/nightly/)

### Installation:
```bash
pip install miqsel --user
```
or
```bash
 pip install git+https://github.com/digitronik/miqsel#egg=miqsel --user
```

## Usage:

```shell
❯❯❯ miqsel --help

Usage: miqsel [OPTIONS] COMMAND [ARGS]...

  Miq Selenium Server

Options:
  --version  Show the version and exit.
  --help     Show this message and exit.

Commands:
  appliance  Appliance
  browser    Set Browser
  config     Configure Miq Selenium Server
  executor   Selenium executor URL
  start      Start Selenium Server
  status     Status of Selenium Server
  stop       Stop Selenium Server
  viewer     VNC viewer
  vnc        VNC URL
```

- **Configuration**:
If the project directory `not set` then `miqsel` need to run from `integration_tests` project directory.  It will help to manage `env.local.yaml`.

    ```shell
    ❯❯❯ miqsel config
    Miq project working dir: /home/.../integration_tests
    ```

- **Status**:
Check status of selenium container (running/ stopped).
    ```shell
    ❯❯❯ miqsel status
    stopped
    ```

- **Start/Stop**:
The start will set command executor in `env.local.yaml` and provide `vnc` access.
    ```shell
    ❯❯❯ miqsel start
    Selenium Server started

    TigerVNC Viewer 64-bit v1.9.0

    ❯❯❯ miqsel stop

    Sun Apr 28 12:29:02 2019
     CConn:       End of stream
    Selenium Server stopped
    ```

- **Appliance**:
Check current appliance or set new.
    ```shell
    ❯❯❯ miqsel appliance

    ❯❯❯ miqsel appliance -s 192.168.1.1
    Appliance set to 192.168.1.1
    ❯❯❯ miqsel appliance
    192.168.1.1
    ```

- **Browser**:
Check current browser or set other.
    ```shell
    ❯❯❯ miqsel browser
    chrome
    ❯❯❯ miqsel browser --firefox
    Browser set to firefox
    ❯❯❯ miqsel browser
    firefox
    ```

- **Viewer**:
Take `vnc` access of selenium server. At the start of selenium server, vnc viewer will be `invoked` automatically.
If the `status` is `running` and the `viewer` is `close` then viewer command will help to re-open vnc session.

    ```shell
    ❯❯❯ miqsel status
    running
    ❯❯❯ miqsel viewer
    TigerVNC Viewer 64-bit v1.9.0
    ```

- **Executor**:
Get command executor url
    ```shell
    ❯❯❯ miqsel executor
    http://172.17.0.2:4444/wd/hub
    ```

- **VNC**:
Get vnc session url
    ```shell
    ❯❯❯ miqsel vnc
    172.17.0.2:5999
    ```
