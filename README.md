# Electric Imp library for nRF24L01+ 2.4GHz Wireless Transceiver

### Description:
* <b>Author:</b> Sinan B.
* <b>Code Repo:</b> `git@github.com:sbolel/nrf24_imp.git`
* <b>GitHub Home:</b> https://github.com/sbolel/nrf24_imp

### Design Goals:
* This library is intended to be:
    * Functionally equivalent to [Maniacbug's original nRF24 library](https://github.com/sbolel/nrf24_imp#documentation) for the Arduino.
    * Able to support all standard functions of the RF24 transceiver.
    * Easily modifiable to match non-standard settings

## External Content

### Documentation:
* [Electric Imp API Documentation](http://devwiki.electricimp.com/doku.php)
* [nRF24L01+ Datasheet (v2.0)](http://www.nordicsemi.com/files/Product/data_sheet/nRF24L01_Product_Specification_v2_0.pdf)
* [Sparkfun nRF24L01+ product page](https://www.sparkfun.com/products/691)
    * V.1 of the datasheet can be found [on SparkFun's website](http://www.sparkfun.com/datasheets/Wireless/Nordic/nRF24L01P_Product_Specification_1_0.pdf).
* [Maniacbug's Source Code for Arduino](https://github.com/maniacbug/RF24)
    * This is the original library released by [Maniacbug](https://github.com/maniacbug) for the Arduino environment (Atmel Microcontrollers).
    * This library is the one being ported over to the Imp.
* [Maniacbug's nRF24L01 Documentation](http://maniacbug.github.com/RF24)
* [Maniacbug's RF24 Class Documentation](http://maniacbug.github.com/RF24/classRF24.html)

### Resources:
* [DIYEmbedded Tutorial for nRF24L01+](http://www.diyembedded.com/tutorials/nrf24l01_0/nrf24l01_tutorial_0.pdf)
    * Good tutorial on how the nRF24L01+ actually operates. Not code specific - outlines the actual harware operation.
    * Good resource for understanding SPI communication with the RF24.
* [CC1101 Library for Electric Imp](http://pastebin.com/4v5ntaK2)
    * This is another RF module that uses the Imp. jwjames83 has released an SPI library for interfacing with the CC1101 and its very similar to the RF24 and makes a good resource for comparing functions.
    * Author: [jwjames83](http://forums.electricimp.com/profile/13/jwjames83) Thank you for your work!
    * [Original thread on the Imp forums](http://forums.electricimp.com/discussion/168#Item_2)

## Current Progress

### Information:
* Only minimal functions have been ported thus far.
* Written functions have NOT been tested to the fullest extent.
* Use library at your own risk.
* PLEASE review the datasheet and the hard-coded configuration instructions to ensure that the configs match your intended features.

### Functions:
* <b> Implemented nRF24l01 Class Functions </b>
    * Constants for registry addresses & bit flags
    * Data pipe addresses
    * `csn(state)`: Chip select not
        * Active Low
    * `ce(state)`: Chip enable
        * When RF24 is in RX mode:
        * When RF24 is in TX mode:
    * `spi_setup()`: Establish SPI communication on the Electric Imp
        * SPI mode used: `SPI_189`
        * SPI clock speed used: `100`
    * `pin_setup()`: Configure Imp pins for RF24
    * `read_register(regAddr)`: Read a register from the RF24
        * Input argument: `regAddr` = address of the register to be read in hex
        * Returns: Register contents
    * `write_address(regAddr, data)`: write data to a register
        * Arguments:
            * `regAddr`: Address of the register to be written to
            * `data`: Data to be written to the register (1-5 bytes, depending on the register)
        * Returns: none
    * `instructByte(instruction)`: send an instruction byte to the RF24
        * Argument: `instruction` = one byte instruction data in hex
    * `pwrDn()`: send a power-down command to the RF24
    * `pwrUp()`: send a power-up command to the RF24
    * `flush_rx()` & `flush_tx()` = flush rx/tx buffers
    * `get_status()`: read the status register
    * `set_channel(ch)`: set radio frequency channel
    * `openWritingPipe()`: open writing pipe
        * Use pipe 1 (address: `0xD2F0F0F0F0`)
    * `openReadingPipe()`: open reading pipe
        * Use pipe 0 (address: `0cE1F0F0F0F0`)
    * `stopListening()`: Instruct radio to stop listening for packets
    * `startListening()`: Instruct radio to start listening air for packets
    * `startRadio()`: start radio monitoring
        * open reading pipe
        * open writing pipe
        * start listening air for packets

### To-Do:
  * payload read and write
  * radio status checking