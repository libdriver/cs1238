### 1. Board

#### 1.1 Board Info

Board Name: Raspberry Pi 4B.

GPIO Pin: SCLK/DIO GPIO27/GPIO17.

### 2. Install

#### 2.1 Dependencies

Install the necessary dependencies.

```shell
sudo apt-get install libgpiod-dev pkg-config cmake -y
```

#### 2.2 Makefile

Build the project.

```shell
make
```

Install the project and this is optional.

```shell
sudo make install
```

Uninstall the project and this is optional.

```shell
sudo make uninstall
```

#### 2.3 CMake

Build the project.

```shell
mkdir build && cd build 
cmake .. 
make
```

Install the project and this is optional.

```shell
sudo make install
```

Uninstall the project and this is optional.

```shell
sudo make uninstall
```

Test the project and this is optional.

```shell
make test
```

Find the compiled library in CMake. 

```cmake
find_package(cs1238 REQUIRED)
```

### 3. CS1238

#### 3.1 Command Instruction

1. Show cs1238 chip and driver information.

    ```shell
    cs1238 (-i | --information)  
    ```

2. Show cs1238 help.

    ```shell
    cs1238 (-h | --help)        
    ```

3. Show cs1238 pin connections of the current board.

    ```shell
    cs1238 (-p | --port)        
    ```

4. Run cs1238 register test.

    ```shell
    cs1238 (-t reg | --test=reg)
    ```

5. Run cs1238 read test, voltage is the reference voltage in volt, hex is the temperature raw data, deg is the temperature  in C and num is the test times.

    ```shell
    cs1238 (-t read | --test=read) [--ref=<voltage>] [--temp-raw=<hex>] [--temp-deg=<deg>] [--times=<num>]
    ```
    
6. Run cs1238 read function,  voltage is the reference voltage in volt and num is the test times.

    ```shell
    cs1238 (-e read | --example=read) [--ref=<voltage>] [--times=<num>]
    ```
    
7. Run cs1238 temperature function, hex is the temperature raw data, deg is the temperature  in C and num is the test times.

    ```shell
    cs1238 (-e temperature | --example=temperature) [--temp-raw=<hex>] [--temp-deg=<deg>] [--times=<num>]
    ```

#### 3.2 Command Example

```shell
./cs1238 -i

cs1238: chip is CHIPSEA CS1238.
cs1238: manufacturer is CHIPSEA.
cs1238: interface is GPIO.
cs1238: driver version is 1.0.
cs1238: min supply voltage is 3.0V.
cs1238: max supply voltage is 5.5V.
cs1238: max current is 2.34mA.
cs1238: max temperature is 85.0C.
cs1238: min temperature is -40.0C.
```

```shell
./cs1238 -p

cs1238: GPIO interface SCLK connected to GPIO27(BCM).
cs1238: GPIO interface DIO connected to GPIO17(BCM).
```

```shell
./cs1238 -t reg

cs1238: chip is CHIPSEA CS1238.
cs1238: manufacturer is CHIPSEA.
cs1238: interface is GPIO.
cs1238: driver version is 1.0.
cs1238: min supply voltage is 3.0V.
cs1238: max supply voltage is 5.5V.
cs1238: max current is 2.34mA.
cs1238: max temperature is 85.0C.
cs1238: min temperature is -40.0C.
cs1238: start register test.
cs1238: cs1238_set_reference_voltage_output/cs1238_get_reference_voltage_output test.
cs1238: enable reference voltage output.
cs1238: check reference voltage output ok.
cs1238: disable reference voltage output.
cs1238: check reference voltage output ok.
cs1238: cs1238_set_adc_rate/cs1238_get_adc_rate test.
cs1238: set adc rate 10hz.
cs1238: check adc rate ok.
cs1238: set adc rate 40hz.
cs1238: check adc rate ok.
cs1238: set adc rate 640hz.
cs1238: check adc rate ok.
cs1238: set adc rate 1280hz.
cs1238: check adc rate ok.
cs1238: cs1238_set_pga/cs1238_get_pga test.
cs1238: set pga 1.
cs1238: check pga ok.
cs1238: set pga 2.
cs1238: check pga ok.
cs1238: set pga 64.
cs1238: check pga ok.
cs1238: set pga 128.
cs1238: check pga ok.
cs1238: cs1238_set_channel/cs1238_get_channel test.
cs1238: set channel short circuit.
cs1238: check channel ok.
cs1238: set channel temperature.
cs1238: check channel ok.
cs1238: set channel b.
cs1238: check channel ok.
cs1238: set channel a.
cs1238: check channel ok.
cs1238: cs1238_wake_up test.
cs1238: check wake up ok.
cs1238: cs1238_wake_up test.
cs1238: check power down ok.
cs1238: finish register test.
```

```shell
./cs1238 -t read --ref=3.3 --temp-raw=0xC2000 --temp-deg=25.0 --times=3

cs1238: chip is CHIPSEA CS1238.
cs1238: manufacturer is CHIPSEA.
cs1238: interface is GPIO.
cs1238: driver version is 1.0.
cs1238: min supply voltage is 3.0V.
cs1238: max supply voltage is 5.5V.
cs1238: max current is 2.34mA.
cs1238: max temperature is 85.0C.
cs1238: min temperature is -40.0C.
cs1238: start read test.
cs1238: set channel a.
cs1238: set pga 1.
cs1238: adc is 94.770966mV.
cs1238: adc is 92.094336mV.
cs1238: adc is 89.329192mV.
cs1238: set pga 2.
cs1238: adc is 86.066115mV.
cs1238: adc is 83.625126mV.
cs1238: adc is 81.191906mV.
cs1238: set pga 64.
cs1238: adc is 25.781250mV.
cs1238: adc is 25.781250mV.
cs1238: adc is 25.781213mV.
cs1238: set pga 128.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890035mV.
cs1238: set adc rate 10hz.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: set adc rate 40hz.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: set adc rate 640hz.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: adc is 12.890625mV.
cs1238: set adc rate 1280hz.
cs1238: adc is -0.004695mV.
cs1238: adc is -0.004764mV.
cs1238: adc is -0.004421mV.
cs1238: set channel b.
cs1238: adc is -12.720671mV.
cs1238: adc is -12.616803mV.
cs1238: adc is -12.504787mV.
cs1238: read temperature test.
cs1238: raw is 0xC1D40, temperature is 24.74C.
cs1238: raw is 0xC1CFD, temperature is 24.71C.
cs1238: raw is 0xC1CEC, temperature is 24.70C.
cs1238: finish read test.
```

```shell
./cs1238 -e read --ref=3.3 --times=3

cs1238: adc is 1.222429mV.
cs1238: adc is 1.222259mV.
cs1238: adc is 1.222230mV.
```
```shell
./cs1238 -e temperature --temp-raw=0xC2000 --temp-deg=25 --times=3

cs1238: temperature is 25.67C.
cs1238: temperature is 25.64C.
cs1238: temperature is 25.62C.
```
```shell
./cs1238 -h

Usage:
  cs1238 (-i | --information)
  cs1238 (-h | --help)
  cs1238 (-p | --port)
  cs1238 (-t reg | --test=reg)
  cs1238 (-t read | --test=read) [--ref=<voltage>] [--temp-raw=<hex>] [--temp-deg=<deg>] [--times=<num>]
  cs1238 (-e read | --example=read) [--ref=<voltage>] [--times=<num>]
  cs1238 (-e temperature | --example=temperature) [--temp-raw=<hex>] [--temp-deg=<deg>] [--times=<num>]

Options:
  -e <read | temperature>, --example=<read | temperature>
                                         Run the driver example.
  -h, --help                             Show the help.
  -i, --information                      Show the chip information.
  -p, --port                             Display the pin connections of the current board.
      --ref=<voltage>                    Set the reference voltage.([default: 3.3])
  -t <reg | read>, --test=<reg | read>   Run the driver test.
      --times=<num>                      Set the test times.([default: 3])
      --temp-raw=<hex>                   Set the temperature raw data.([default: 0x0000])
      --temp-deg=<deg>                   Set the temperature degree.([default: 0.0])
```
