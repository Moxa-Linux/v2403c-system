# V-2403C system package

## base-system
Base system for V-2403C.
It contains the necessary tools for setting up V-2403C

## moxa-configs
The platform-related configuration items are recoreded in this file,
these items will be referred to other platform packages.

## Utilities
[moxa-audio-retask](/moxa-audio-retask.md)

# V-2403C GPIO table

## Build the necessary drivers
### Build moxa-it87-gpio-driver
```bash=
git clone git@gitlab.syssw.moxa.com:MXcore-Package/moxa-it87-gpio-driver.git
cd moxa-it87-gpio-driver
make KRELEASE=$(uname -r) modules
make install
modprobe gpio-it87
```

### Build moxa-it87-serial-driver
```bash=
git clone git@gitlab.syssw.moxa.com:MXcore-Package/moxa-it87-serial-driver.git
cd moxa-it87-serial-driver
make KRELEASE=$(uname -r) modules
make install
modprobe it87_serial
```

## UART
| Port | Device Node | GPIO#0 | GPIO#1 | GPIO#2 | /sys/class/misc/it87_serial |
| ---- | ----------  | ------ | ------ | ------ | ------ |
| 1 | /dev/ttyM0  |   444  |  441   |   442  |   serial1/serial1_rs485  |
| 2 | /dev/ttyM1  |   456  |  445   |   446  |   serial2/serial2_rs485  |
| 3 | /dev/ttyM2  |   462  |  458   |   459  |   serial3/serial3_rs485  |
| 4 | /dev/ttyM3  |   472  |  463   |   471  |   serial4/serial4_rs485  |

### Initial UART GPIO pins
```bash=
# Port 1 (/dev/ttyM0)
init_gpio "444" "out" "0"
init_gpio "441" "out" "0"
init_gpio "442" "out" "0"

# Port 2 (/dev/ttyM1)
init_gpio "456" "out" "0"
init_gpio "445" "out" "0"
init_gpio "446" "out" "0"

# Port 3 (/dev/ttyM2)
init_gpio "462" "out" "0"
init_gpio "458" "out" "0"
init_gpio "459" "out" "0"

# Port 4 (/dev/ttyM3)
init_gpio "472" "out" "0"
init_gpio "463" "out" "0"
init_gpio "471" "out" "0"
```

### Set UART mode

- Port 1 (/dev/ttyM0)

```bash=
# Switch Port 1 to RS232 mode
echo 1 > /sys/class/gpio/gpio444/value
echo 0 > /sys/class/gpio/gpio441/value
echo 0 > /sys/class/gpio/gpio442/value
echo 0 > /sys/class/misc/it87_serial/serial1/serial1_rs485

# Switch Port 1 to RS485-2W
echo 0 > /sys/class/gpio/gpio444/value
echo 1 > /sys/class/gpio/gpio441/value
echo 0 > /sys/class/gpio/gpio442/value
echo 1 > /sys/class/misc/it87_serial/serial1/serial1_rs485

# Switch Port 1 to RS422/RS485-4W
echo 0 > /sys/class/gpio/gpio444/value
echo 0 > /sys/class/gpio/gpio441/value
echo 1 > /sys/class/gpio/gpio442/value
echo 1 > /sys/class/misc/it87_serial/serial1/serial1_rs485
```

- Port 2 (/dev/ttyM1)

```bash=
# Switch Port 2 to RS232 mode
echo 1 > /sys/class/gpio/gpio456/value
echo 0 > /sys/class/gpio/gpio445/value
echo 0 > /sys/class/gpio/gpio446/value
echo 0 > /sys/class/misc/it87_serial/serial2/serial2_rs485

# Switch Port 2 to RS485-2W
echo 0 > /sys/class/gpio/gpio456/value
echo 1 > /sys/class/gpio/gpio445/value
echo 0 > /sys/class/gpio/gpio446/value
echo 1 > /sys/class/misc/it87_serial/serial2/serial2_rs485

# Switch Port 2 to RS422/RS485-4W
echo 0 > /sys/class/gpio/gpio456/value
echo 0 > /sys/class/gpio/gpio445/value
echo 1 > /sys/class/gpio/gpio446/value
echo 1 > /sys/class/misc/it87_serial/serial2/serial2_rs485
```

- Port 3 (/dev/ttyM2)

```bash=
# Switch Port 3 to RS232 mode
echo 0 > /sys/class/gpio/gpio462/value
echo 1 > /sys/class/gpio/gpio458/value
echo 0 > /sys/class/gpio/gpio459/value
echo 0 > /sys/class/misc/it87_serial/serial3/serial3_rs485

# Switch Port 3 to RS485-2W
echo 1 > /sys/class/gpio/gpio462/value
echo 0 > /sys/class/gpio/gpio458/value
echo 0 > /sys/class/gpio/gpio459/value
echo 1 > /sys/class/misc/it87_serial/serial3/serial3_rs485

# Switch Port 3 to RS422/RS485-4W
echo 0 > /sys/class/gpio/gpio462/value
echo 0 > /sys/class/gpio/gpio458/value
echo 1 > /sys/class/gpio/gpio459/value
echo 1 > /sys/class/misc/it87_serial/serial3/serial3_rs485
```

- Port 4 (/dev/ttyM3)

```bash=
# Switch Port 4 to RS232 mode
echo 1 > /sys/class/gpio/gpio472/value
echo 0 > /sys/class/gpio/gpio463/value
echo 0 > /sys/class/gpio/gpio471/value
echo 0 > /sys/class/misc/it87_serial/serial4/serial4_rs485

# Switch Port 4 to RS485-2W
echo 0 > /sys/class/gpio/gpio472/value
echo 1 > /sys/class/gpio/gpio463/value
echo 0 > /sys/class/gpio/gpio471/value
echo 1 > /sys/class/misc/it87_serial/serial4/serial4_rs485

# Switch Port 4 to RS422/RS485-4W
echo 0 > /sys/class/gpio/gpio472/value
echo 0 > /sys/class/gpio/gpio463/value
echo 1 > /sys/class/gpio/gpio471/value
echo 1 > /sys/class/misc/it87_serial/serial4/serial4_rs485
```

## Digital IO
| Output Pin   |   DO0  |   DO1  |   DO2  |   DO3  |
| ------------ | ------ | ------ | ------ | ------ |
| SYS GPIO PIN |   492  |  493   |   494  |   495  |

| Input Pin    |   DI0  |  DI1   |   DI2  |  DI3   |
| ------------ | ------ | ------ | ------ | ------ |
| SYS GPIO PIN |   488  |  489   |   490  |   491  |

### Initial Digital IO GPIO pins
```bash=
# setup output pins (DO0~DO3)
init_gpio "492" "out" "0"
init_gpio "493" "out" "0"
init_gpio "494" "out" "0"
init_gpio "495" "out" "0"

# export input pins (DI0~DI3)
init_gpio "488"
init_gpio "489"
init_gpio "490"
init_gpio "491"
```
### Example for controlling Digital IO GPIO pins
```bash=
# set output high for DO0
echo 1 > /sys/class/gpio/gpio496/value
# set output low for DO1
echo 0 > /sys/class/gpio/gpio493/value

# get input from DI0
cat /sys/class/gpio/gpio488/value
# get input from DI1
cat /sys/class/gpio/gpio489/value
```

## miniPCIe
### Power control
| miniPCIe Slot | Slot 1 | Slot 2 |
| ------------- | ------ | ------ |
|  SYS GPIO PIN |   497  |  499   |

### Initial miniPCIe Power control GPIO pins
```bash=
init_gpio "497" "out" "0"
init_gpio "499" "out" "0"
```
### Example for controlling miniPCIe power
```bash=
# power on miniPCIe slot 1
echo 1 > /sys/class/gpio/gpio497/value
# power off miniPCIe slot 1
echo 0 > /sys/class/gpio/gpio497/value

# power on miniPCIe slot 2
echo 1 > /sys/class/gpio/gpio499/value
# power off miniPCIe slot 2
echo 0 > /sys/class/gpio/gpio499/value
```

## SIM card
### SIM card select
| SIM card slot | Slot 1 | Slot 2 |
| ------------- | ------ | ------ |
|  SYS GPIO PIN |   496  |  498   |

### Initial miniPCIe Power control GPIO pins
```bash=
init_gpio "496" "out" "0"
init_gpio "498" "out" "0"
```
### Example for SIM card select
```bash=
# switch SIM card slot 1 to slot(side) A
echo 0 > /sys/class/gpio/gpio496/value
# switch SIM card slot 1 to slot(side) B
echo 1 > /sys/class/gpio/gpio496/value

# switch SIM card slot 2 to slot(side) A
echo 0 > /sys/class/gpio/gpio498/value
# switch SIM card slot 2 to slot(side) B
echo 1 > /sys/class/gpio/gpio498/value
```
