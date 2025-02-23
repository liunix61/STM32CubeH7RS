## <b>FMC_SDRAM Example Description</b>

- This project is targeted to run on STM32H7S7xx device on STM32H7RS_CUSTOM_HW board from STMicroelectronics.
  
-The SDRAM memory is MT48LC4M32B2B5-6A.
At the beginning of the main program, the HAL_Init() function is called to reset
all the peripherals and initialize the systick used as 1ms HAL timebase.
- This project runs from the external Flash memory. It is launched from a first boot stage and inherits from this boot project
configuration caches, system clock at 600 MHz and external memory interface at the highest speed).
Note that the boot part is automatically downloaded from the IDE environment via the board project Templates/Template_XIP/Binary/Boot_XIP.hex file.
   
  
-The project calls also SCB_EnableICache() and SCB_EnableDCache() functions in order to enable
  the Layer 1 Core Instruction and Data Caches.

-In this example, the SDRAM device is configured and initialized explicitly 
  following all initialization sequence steps. After initializing the device, user 
  can perform erase/read SDRAM ID/read data/write data operations on it. 
  A data buffer is written to the SDRAM memory, then read back and checked to verify its correctness.



#### <b>Notes</b>

 1. Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
    based on variable incremented in SysTick ISR. This implies that if HAL_Delay() is called from
    a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
    than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
    To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.

 2. The application needs to ensure that the SysTick time base is always set to 1 millisecond
    to have correct HAL operation.
	
### <b>Keywords</b>

FMC/FSMC, Memory, SDRAM, Read, Write, Access

### <b>Directory contents</b>


File                                                                                         | Description 

 --- | ---
  FMC/FMC_SDRAM/Boot/Inc/stm32h7rsxx_hal_conf.h                                              | HAL Configuration file
  FMC/FMC_SDRAM/Boot/Inc/main.h                                                              |Header for main.c module 
  FMC/FMC_SDRAM/Boot/Inc/stm32h7rsxx_it.h                                                    |Header for stm32h7rsxx_it.c  
  FMC/FMC_SDRAM/Boot/Src/main.c                                                              |Main program
  FMC/FMC_SDRAM/Boot/Src/stm32h7rsxx_hal_msp.c                                               |HAL MSP module
  FMC/FMC_SDRAM/Boot/Src/stm32h7rsxx_it.c                                                    |Interrupt handlers 
  FMC/FMC_SDRAM/Boot/Src/system_stm32h7rsxx.c                                                |STM32H7RSxx system clock configuration file 

### <b>Hardware and Software environment</b>

  - This example runs on STM32H7S7L8HxH devices.

  - This example has been tested with STM32H7RS_CUSTOM_HW board and can be
    easily tailored to any other supported device and development board.

  - User Option Bytes requirement (with STM32CubeProgrammer tool):

    - XSPI1_HSLV=1     I/O XSPIM_P1 High speed option enabled
    - XSPI2_HSLV=1     I/O XSPIM_P2 High speed option enabled
    - VDDIO_HSLV=0     I/O speed optimization enabled

### <b>How to use it ?</b>

In order to make the program work, you must do the following :
 
#### <b>IAR</b>
  1. Open your toolchain
  2. Open Multi-projects workspace file Project.eww
  3. Run the example
  #### <b>Limitation</b>
 - The first run generates a hardfault, click on the reset button and select “reset” to run the example