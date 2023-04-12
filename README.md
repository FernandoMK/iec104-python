__iec104-python__


[[_TOC_]]

---

This software provides an object-oriented high-level python module to simulate scada systems and remote terminal units communicating via 60870-5-104 protocol.

The python module c104 combines the use of lib60870-C with state structures and python callback handlers.

**Example remote terminal unit**

```python
import c104

# server and station preparation
server = c104.Server(ip="0.0.0.0", port=2404)

# add local station and points
station = server.add_station(common_address=47)
measurement_point = station.add_point(io_address=11, type=c104.Type.M_ME_NC_1, report_ms=1000)
command_point = station.add_point(io_address=12, type=c104.Type.C_RC_TA_1)

server.start()
```

**Example scada unit**

```python
import c104

client = c104.Client(tick_rate_ms=1000, command_timeout_ms=5000)

# add RTU with station and points
connection = client.add_connection(ip="127.0.0.1", port=2404, init=c104.Init.INTERROGATION)
station = connection.add_station(common_address=47)
measurement_point = station.add_point(io_address=11, type=c104.Type.M_ME_NC_1, report_ms=1000)
command_point = station.add_point(io_address=12, type=c104.Type.C_RC_TA_1)

client.start()
```

See [examples](examples) folder for more detailed examples.

## Licensing

This software is licensed under the GPLv3 (https://www.gnu.org/licenses/gpl-3.0.en.html).

See [LICENSE](LICENSE) file for the complete license text.

### Dependencies

#### lib60870-C

This project is build on top of lib60870-C v2 from MZ Automation GmbH, which is licensed under [GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html).

The library is used for 60870-5-104 protocol based communication.

[&raquo; Source code](https://github.com/mz-automation/lib60870)

[&raquo; Documentation](https://support.mz-automation.de/doc/lib60870/latest/index.html)

#### mbedtls

This project is build on top of mbedtls from the Mbed TLS Contributors, which is licensed under [Apache-2.0](http://www.apache.org/licenses/LICENSE-2.0).

The library is used to add transport layer security to the 60870-5-104 protocol based communication.

[&raquo; Source code](https://github.com/Mbed-TLS/mbedtls)

[&raquo; Documentation](https://www.trustedfirmware.org/projects/mbed-tls/)

#### pybind11

This project is build on top of pybind11 from Wenzel Jakob, which is licensed under a [BSD-style license](https://github.com/pybind/pybind11/blob/master/LICENSE).

The library is used to wrap c++ code into a python module and allow seamless operability between python and c++.

[&raquo; Source code](https://github.com/pybind/pybind11)

[&raquo; Documentation](https://pybind11.readthedocs.io/en/stable/)

#### catch2

This project is build on top of catch2 from the Catch2 Authors, which is licensed under [BSL-1.0](https://www.gnu.org/licenses/gpl-3.0.en.html).

The library is used as testing framework for test-automation.

[&raquo; Source code](https://github.com/catchorg/Catch2)

[&raquo; Documentation](https://github.com/catchorg/Catch2/blob/devel/docs/Readme.md)


## System requirements

### Operating systems

* Debian/Ubuntu (x64): YES
* Raspbian (arm32v7): YES
* Windows (x64): YES
* Raspbian (aarch64): Not yet

### Python versions
* python >= 3.6, < 3.11

## Installation

### Package distribution

#### Install from pypi package (comming soon)
```bash
python3 -m pip install c104~=1.16.0
```

#### Add to requirements.txt
```
c104~=1.16.0
```

### Source distribution

#### Install from source

```bash
sudo apt-get install build-essential cmake python3-dev ninja-build
python3 -m pip install --upgrade pip setuptools wheel ninja
python3 -m pip install c104@git+https://github.com/fraunhofer-fit-dien/iec104-python.git@v1.16.0
```

#### Add to requirements.txt
```
c104 @ git+https://github.com/fraunhofer-fit-dien/iec104-python.git@v1.16.0
```

## Wiki

Read more about the **Classes** and their **Properties** in our [project Wiki](https://iec104-python.readthedocs.io/).

## Contribution

### How to contribute

1. Add feature requests and report bugs using GitHub's issues

1. Create merge requests

### How to build for multiple python versions (linux with docker)

1. Build wheels via docker
   ```bash
   /bin/bash ./bin/linux-build.sh
   ```

### How to build (linux)

1. Install dependencies
   ```bash
   sudo apt-get install build-essential cmake python3-dev python3-dbg
   python3 -m pip install --upgrade pip
   python3 -m pip install setuptools wheel ninja
   ```

1. Build wheel
   ```bash
   python3 setup.py bdist_wheel
   ```

### How to analyze performance (linux)

1. Install dependencies
   ```bash
   sudo apt-get install google-perftools valgrind
   sudo pip3 install yep
   ```

1. Copy pprof binary
   ```bash
   cd /usr/bin
   sudo wget https://raw.githubusercontent.com/gperftools/gperftools/master/src/pprof
   sudo chmod +x pprof
   ```

1. Execute profiler script
   ```bash
   ./bin/profiler.sh
   ```

### How to build (windows)

1. Install dependencies
    - [Python 3](https://www.python.org/downloads/windows/)
    - `python3 -m pip install --upgrade setuptools wheel ninja`
    - [Buildtools für Visual Studio 201*x*](https://visualstudio.microsoft.com/de/downloads/) (Nach unten scrollen &raquo; Alle Downloads &raquo; Tools für Visual Studio 201*x*)
    - [CMake binary](https://cmake.org/download/)

1. Build wheel
   ```bash
   python3 setup.py bdist_wheel
   ```

### Generate documentation

1. Build c104 module

1. Install dependencies
   - `python3 -m pip install --upgrade sphinx breathe-apidoc`
   - doxygen
   - graphviz

1. Build doxygen xml
   ```bash
   doxygen Doxyfile
   ```

1. Build sphinx html
   ```bash
   python3 bin/build-docs.py
   ```

## Change log

Track all changes in our [CHANGELOG](CHANGELOG.md) documentation.
