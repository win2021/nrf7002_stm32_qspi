# nrf7002_stm32_qspi

The repo hosts resources for running nRF7002 on STM32 platform.

## Contents
### HW
SCH_Schematic1_2023-11-27.pdf - The schematic of adaptor

Gerber_PCB1_2023-10-26.zip - Gerber file of adaptor PCB

### SW 
0001-qspi.patch - patch file to add STM32 QSPI driver

shell.zip - modified shell project to enable STM32 as host

## Test
1. Connect nRF7002-EK and NUCLEO-H7A3ZI-Q. The mapping is
   
   nRF7002-EK < ---------------> STM32 Board
   
   CLK        < ---------------> CN10, Pin15 (PB2)
   
   CS         < ---------------> CN10, Pin13 (PG6)
   
   IO0        < ---------------> CN10, Pin23 (PD11)
   
   IO1        < ---------------> CN10, Pin21 (PD12)
   
   IO2        < ---------------> CN10, Pin25 (PE2)
   
   IO3        < ---------------> CN10, Pin19 (PD13)
   
   BUCKEN     < ---------------> CN10, Pin14 (PB6)
   
   IOVDD      < ---------------> CN10, Pin16 (PB7)
   
   IRQ        < ---------------> CN10, Pin2  (PG12)

     Other pins of nRF7002EK are floating.

2. Apply patch to nrf@e4f142f2a19df51b9ae9ff0c32c6a196ced6b25b.

3. Run **west update** to pull STM32 HAL.

4. Build shell example. If you are using nRF connect VS code extension, it should detect the build configuration from **build** folder automatically. Otherwise, manually select **dts32.overlay** and **prj.conf**.

5. In console, use shell command to launch zperf test.

## Known issues
1. The configuration is optimized for UDP TX. Other test cases may yield poor performance.
