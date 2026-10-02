### 1. Chip

#### 1.1 Chip Info

Chip Name: STM32F407ZGT6.

Extern Oscillator: 8MHz.

UART Pin: TX/RX PA9/PA10.

GPIO Pin: SCLK/DIO PA0/PA8.

### 2. Development and Debugging

#### 2.1 Integrated Development Environment

LibDriver provides both Keil and IAR integrated development environment projects.

MDK is the Keil ARM project and your Keil version must be 5 or higher.Keil ARM project needs STMicroelectronics STM32F4 Series Device Family Pack and you can download from https://www.keil.com/dd2/stmicroelectronics/stm32f407zgtx.

EW is the IAR ARM project and your IAR version must be 9 or higher.

#### 2.2 Serial Port Parameter

Baud Rate: 115200.

Data Bits : 8.

Stop Bits: 1.

Parity: None.

Flow Control: None.

#### 2.3 Serial Port Assistant

We use '\n' to wrap lines.If your serial port assistant displays exceptions (e.g. the displayed content does not divide lines), please modify the configuration of your serial port assistant or replace one that supports '\n' parsing.

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
cs1238 -i

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
cs1238 -p

cs1238: GPIO interface SCLK connected to GPIOA PIN0.
cs1238: GPIO interface DIO connected to GPIOA PIN8.
```

```shell
cs1238 -t reg

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
cs1238 -t read --ref=3.3 --temp-raw=0xC2000 --temp-deg=25.0 --times=3

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
cs1238: adc is 0.022030mV.
cs1238: adc is -0.225610mV.
cs1238: adc is -0.069827mV.
cs1238: set pga 2.
cs1238: adc is -0.092644mV.
cs1238: adc is -0.051731mV.
cs1238: adc is -0.061172mV.
cs1238: set pga 64.
cs1238: adc is -0.007978mV.
cs1238: adc is -0.009113mV.
cs1238: adc is -0.006851mV.
cs1238: set pga 128.
cs1238: adc is -0.006119mV.
cs1238: adc is -0.005856mV.
cs1238: adc is -0.007193mV.
cs1238: set adc rate 10hz.
cs1238: adc is -0.007616mV.
cs1238: adc is -0.005912mV.
cs1238: adc is -0.006950mV.
cs1238: set adc rate 40hz.
cs1238: adc is -0.005391mV.
cs1238: adc is -0.008300mV.
cs1238: adc is -0.007673mV.
cs1238: set adc rate 640hz.
cs1238: adc is -0.006800mV.
cs1238: adc is -0.007991mV.
cs1238: adc is -0.008882mV.
cs1238: set adc rate 1280hz.
cs1238: adc is -0.008278mV.
cs1238: adc is -0.006840mV.
cs1238: adc is -0.007722mV.
cs1238: set channel b.
cs1238: adc is 0.859597mV.
cs1238: adc is 0.552181mV.
cs1238: adc is 0.240697mV.
cs1238: read temperature test.
cs1238: raw is 0xC2125, temperature is 25.11C.
cs1238: raw is 0xC1B53, temperature is 24.55C.
cs1238: raw is 0xC1C67, temperature is 24.65C.
cs1238: finish read test.
```

```shell
cs1238 -e read --ref=3.3 --times=3

cs1238: adc is 1.220608mV.
cs1238: adc is 1.222999mV.
cs1238: adc is 1.222683mV.
```
```shell
cs1238 -e temperature --temp-raw=0xC2000 --temp-deg=25 --times=3

cs1238: temperature is 24.92C.
cs1238: temperature is 25.14C.
cs1238: temperature is 24.97C.
```
```shell
cs1238 -h

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
