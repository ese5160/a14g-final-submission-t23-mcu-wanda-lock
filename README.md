[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/kzkUPShx)
# a14g-final-submission

    * Team Number: 23
    * Team Name: MCU - Wanda Lock
    * Team Members: Tao Liu & Chihan Zheng 
    * Github Repository URL: https://github.com/ese5160/a14g-final-submission-t23-mcu-wanda-lock.git
    * Description of test hardware: embedded hardware, Windows laptop, IR sensor, QR code reader, LCD screen, servo, battery, etc

## 1. Video Presentation

## 2. Project Summary

> ## Device Description
> **Wanda Lock is an intelligent door lock which is easy-to-use, cheap but still maintains security.**
> 
> Wanda Lock is focusing on realizing common functions of door locks, but ensuring a lower price and is still capable of avoiding security issues.
>
> Wanda Lock requires user to provide email to receive a key of QR code. This helps to avoid the situation where people steal the name and password and can also open the lock. Using personal email for identification and security is a common strategy on the market, so using this instead of camera is an effective and much cheaper way to ensure both functionality and secuirty.
>
> **Internet Usage**
> Wanda Lock has 3 different interfaces for 3 kinds of users: Guests, Owner, Administrators
> 
> a. Guests
>  Guests can send personal information to owner's interface such as name, password and email.
>
> b. Owner
>  Owner can see guests information, then can decide whether to open the lock and whether to store guests information into local database. Owner can be notified by sound when guests are coming and the lock is open/closed. The lock status is also indicated by a LED on the interface in case owner is not capable getting access to the sound notification.
>
> c. Administrators
> Administrators can use their interface to realize On-The-Air-Firmware-Update by simply pressing a button on the website. The update progress is shown on real time.
 
> ### Inspiration
> There are so many smart lock on the markets, why do we want to design another one? 
>
> **Price and Potential Customers Are What We Focus on**
> 
> Firstly, many smart locks on the market are over $200 just because they use cameras. Then, why not use email and QR code reader to create a cheap and secure lock?
>
> Secondly, do many people really need our lock? Absolutely! Nowadays, people especially businessmen spend much time working outside. They need a way to monitor their door on real time and let their guests to come in when they are not at home. 
> 
> Besides, in a modern world, everything is driven to be controlled remotely and everybody will use smart devices. Thus, since people need it, we build it.

> ### Device Functionality
> 

> ### Challenges
>
> **Firmware**
> 1. When we tested the QR code reader, the reader always returned 0s to MCU even if the I2C communication is normal. Later, we found although manufacturer says a register can be written to control the LED, the read-back data will be all 0 if we write to the register before we read from the reader.
> Besides, the interval that the reader reads QR code also matters. If we uses 400ms instead of 200ms, the read-back data is also 0.
>
> 2. We store a large QR code into a 2D array. However, If we define the array as a global variable, the memory is not enough. Thus, we moved it into a function so that it can be in the stack, then the stack has enough space to store the array.
>
> 3. When integrating all peripheral drivers together, the FreeRTOS stack always overflows. Thus, we had to adjusted the task size for each task. We should've used High WaterMark function to estimate the size of each task instead of just trying random task sizes.
> 
> **Hardware**
> 1. We didn't assign the SPI LCD screen pins to the Sercom specifically, so latrer our LCD cannot have normal communication between MCU. Thus, we rearranged the pin assignment for LCD and did rewirein work using unused test points of MCU pins.
>
> 2. We planned to use PA21 to generate PWM through TCC0, but it didn't give any output. Thus, we had to changed PA21 to PA10 which generated correct PWM pulse using TCC0.

>### Prototype Learnings
> 1. We did many rework and rewire. It resulted from many reasons. The first reason is that we didn't consider much about the functions of each pin when we did pin assignment. If we want to use I2C peripherals, we need to find Sercom pins instead of other random pins. Some pins have specific functionality so we need to do every single pin assignment according to what we want the pin to do.
>
> 2. Even if we assigned correct pins, sometimes they don't work correctly either. Thus, route every unused pins to testpoints! You don't want to stare at the MCU when you want to rewire but there is not testpoints on the board.
Even if you already have jumpers for the power circuits, add test points as well! If the jumper pads are ruined, you still have testpoints! Adding testpoints not only helps test signals, but also help you much when you want to do rewiring work.
> 
>3. Please use tapes to fix the test wires onto the board, or you will 100% pull the pads off your board. Sometimes, you don't even know when the pads disappear. Therefore, use insulated tape to fix test wires onto the board in case the wires are pulled up with pads accidentally! After you don't need the test wires, just desolder them off the board.
>
>4. Arrange the locations of connectors on your PCB with deep consideration. You don't want the situation where you connect the peripheral into the connector and can never pull it out because another connector block the way that there is not space for your little fingers.
Take us as an example, our QR code reader sometimes goes wrong, so we have to replug it into the connector. However, there is another LCD connector right next to it blocking our way, so we can hardly pull the QR code reader connector out after we plug it into the connector designed for it on the board. This time we are lucky, because we can replug the connector on the QR code reader itself instead of the one on the board, but what if the connector on the QR code is soldered so that we can only replug the connector to the board?
>
>5. Download the documentations you need from Microchip in case the website crashes for weeks!



## 3. Hardware & Software Requirements

## 4. Project Photos & Screenshots
