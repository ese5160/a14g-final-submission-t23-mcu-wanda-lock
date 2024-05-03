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
> 1. When we tested the QR code reader, the reader always returned all 0 data to MCU even if the I2C communication is normal. Later, we found although manufacturer says a register can be written to control the LED, the read-back data will be all 0 if we write to the register before.
> Besides, the interval that the reader reads QR code matters. If we uses 400ms instead of 200ms, the read-back data is also 0.
>
> 2. We store a large QR code into a 2D array. However, If we define the array as a global variable, the memory is not enough. Thus, we moved it into a function so that it can be in the stack, then the stack has enough space to store the array.
>
> 3. When integrating all peripheral drivers together, the FreeRTOS stack always overflows. Thus, we had to ajusted the task size for each task. We should've used High WaterMark function to estimate the size of each task instead of just trying random task sizes.
> 
> **Hardware**
> 1. 

## 3. Hardware & Software Requirements

## 4. Project Photos & Screenshots
