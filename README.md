# Using `python-kasa`

Document with hints and examples on how to use the
[`python-kasa`](https://github.com/python-kasa/python-kasa) package.

## Installation

The simplest way to install the package is under a virtual environment:

```bash
$ python3 -m venv venv-3.13
$ . venv-3.13/bin/activate
(venv-3.13) $ pip install python-kasa
```

## Usage

### Discovering Devices

Some devices may require authentication to be discovered. The error during
discovery will look something like this:

```bash
(venv-3.13) $ kasa --host IP_OF_DEVICE discover
Discovering device IP_OF_DEVICE for 10 seconds
== Authentication failed for device ==
...
```

The [README](https://github.com/python-kasa/python-kasa/blob/master/README.md#discovering-devices) explains that setting `KASA_USERNAME` and `KASA_PASSWORD` will
allow for proper authentication. These are the credentials used to add the
device to the Kasa App:

```
(venv-3.13) $ export KASA_USERNAME=YOUR_USERNAME
(venv-3.13) $ read -sr KASA_PASSWORD; export KASA_PASSWORD
(venv-3.13) $ kasa --host IP_OF_DEVICE discover
```

should result in a valid login and data (assuming credentials are valid).

### Setting Date and Time

Date and time must be set correctly for historical stats to work. To set the
date and time use the `time set` command:

```
(venv-3.13) $ kasa --host IP_OF_DEVICE time set --timezone "EST" 2025 08 22 23 44
```

### Showing Energy Usage

```
$ kasa --host IP_OF_DEVICE energy
Discovering device IP_OF_DEVICE for 10 seconds
== Energy ==
Current: 1.726 A
Voltage: 123.629 V
Power: 224.294 W
Total consumption: None kWh
Today: 0.036 kWh
This month: 0.066 kWh

```
