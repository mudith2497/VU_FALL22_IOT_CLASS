# Temperature & Humidity sensor (DHT11) set up on Raspberry Pi

## Required Equipment

1. DHT11 Temperature Humidity Sensor
2. Bread Board
3. 10 kilo Ohm resisitor.
4. Raspberry Pi 4 B+
5. Male to Female Jump Wires

# Specifications of The Required Equipment 

## DHT11 Temperature Humidity Sensor

<img width="460" alt="Screen Shot 2022-09-29 at 2 53 43 PM" src="https://user-images.githubusercontent.com/107719838/193118439-69efe8bb-7322-4baa-a2fa-bd9464fdcf7d.png">

<img width="216" alt="Screen Shot 2022-09-29 at 2 54 39 PM" src="https://user-images.githubusercontent.com/107719838/193118505-f44e0a18-d11d-4e13-8c02-3184a3d31dca.png">

 3 to 5V power and I/O
 2.5mA max current use during conversion (while requesting data)
 Good for 20-80% humidity readings with 5% accuracy
 Good for 0-50 °C temperature readings +-2 °C accuracy
 No more than 1 Hz sampling rate (once every second)
 Body size 15.5mm x 12mm x 5.5mm
 4 pins with 0.1" spacing
 Adafruit Learning Documentation for DHTxx Sensors
 RoHS compliant
 
 For Further Documentation Please follow : https://learn.adafruit.com/dht
 
 ## Bread Board
 
 <img width="545" alt="Screen Shot 2022-09-29 at 3 00 52 PM" src="https://user-images.githubusercontent.com/107719838/193119656-928d1055-7138-4dc3-b0a7-69e0e58dd279.png">

This is a 'full-size' premium quality breadboard, 830 tie points. Good for small and medium projects. It's 2.2" x 7" (5.5 cm x 17 cm) with a standard double-strip in the middle and two power rails on both sides. You can pull the power rails off easily to make the breadboard as thin as 1.4" (3.5cm). You can also "snap" these breadboards together, either way, to make longer and/or wider breadboards. The back is made of foam double-sided tape, if you remove the protective paper you can attach it to a flat clean surface.

 For Further Documentation Please follow : https://www.adafruit.com/product/239
 
 ## Raspberry Pi 4 B+
 
<img width="640" alt="Screen Shot 2022-09-29 at 3 05 40 PM" src="https://user-images.githubusercontent.com/107719838/193120594-2aed14e6-9bcc-46e0-9f7e-b4c9ee0c5726.png">

<img width="310" alt="Screen Shot 2022-09-29 at 3 06 11 PM" src="https://user-images.githubusercontent.com/107719838/193120602-ba0b9180-fc96-4ef1-b5dc-e94320fcca43.png">



Broadcom BCM2711, Quad core Cortex-A72 (ARM v8) 64-bit SoC @ 1.5GHz
1GB, 2GB, 4GB or 8GB LPDDR4-3200 SDRAM (depending on model)
2.4 GHz and 5.0 GHz IEEE 802.11ac wireless, Bluetooth 5.0, BLE
Gigabit Ethernet
2 USB 3.0 ports; 2 USB 2.0 ports.
Raspberry Pi standard 40 pin GPIO header (fully backwards compatible with previous boards)
2 × micro-HDMI ports (up to 4kp60 supported)
2-lane MIPI DSI display port
2-lane MIPI CSI camera port
4-pole stereo audio and composite video port
H.265 (4kp60 decode), H264 (1080p60 decode, 1080p30 encode)
OpenGL ES 3.1, Vulkan 1.0
Micro-SD card slot for loading operating system and data storage
5V DC via USB-C connector (minimum 3A*)
5V DC via GPIO header (minimum 3A*)
Power over Ethernet (PoE) enabled (requires separate PoE HAT)
Operating temperature: 0 – 50 degrees C ambient

 For Further Documentation Please follow : https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-datasheet.pdf
 
 
 ## Wires and Resistors
 
<img width="327" alt="Screen Shot 2022-09-29 at 3 08 39 PM" src="https://user-images.githubusercontent.com/107719838/193121202-35af665b-fee9-4aac-8b63-ff2d567294f9.png">


 
 
<img width="382" alt="Screen Shot 2022-09-29 at 3 09 29 PM" src="https://user-images.githubusercontent.com/107719838/193121207-aabc27ae-474e-48dc-aa55-217c88b3f66b.png">



# Circuit diagram of microcontroller to analog device

<img width="1197" alt="Screen Shot 2022-09-29 at 1 11 11 PM" src="https://user-images.githubusercontent.com/107719838/193121613-fba2c7e9-c1d5-478d-88cb-d701a23b2226.png">

First step is to connect The Power input Vcc Pin to Vout pin in the raspberry pi 

Later on Insert the 10 k ohm Resistor to the same line and Insert The other resistor end parallel to the Second Pin of the Sensor. 

The Ground connection is given to the Raspberry Pi ground And The GPIO pin to the Second Pin in the sensor. Later On The circuit should be in the Closed Loop. 


![IMG_4436-min](https://user-images.githubusercontent.com/107719838/193123596-5c160b3b-c678-4dfb-be2b-9ff181384ad0.PNG)


Hence all The connections are Made Lets Write A Program To execute the Readings captured by the DHT11 sensor.

# Installing Wiring Pi 

WiringPi is now maintained under GIT for ease of change tracking, however there is a Plan B if you’re unable to use GIT for whatever reasons (usually your firewall will be blocking you, so do check that first!)

If you do not have GIT installed, then under any of the Debian releases (e.g. Raspbian), you can install it with:

                   
                   sudo apt-get install git-core

If you get any errors here, make sure your Pi is up to date with the latest versions of Raspbian:

                  sudo apt-get update
 
                  sudo apt-get upgrade
                  
To obtain WiringPi using GIT:

          git clone https://github.com/WiringPi/WiringPi
          
          git pull origin
          
          
After Cloning The Repository 

          cd WiringPi
          
          sudo nano ( your file name ) .C 
          
          In my case it was sudo nano temperature.c 
          
          
 
 <img width="1440" alt="Screen Shot 2022-09-29 at 3 37 18 PM" src="https://user-images.githubusercontent.com/107719838/193126235-d1aed65b-6912-471f-86e4-8a51b5ca9a8f.png">

 By these commands we can Write the C program in the Terminal 
 
 
 You can Follow This C Program : 
 
                            #include <wiringPi.h>
                            #include <stdio.h>
                            #include <stdlib.h>
                            #include <stdint.h>
                            #define MAXTIMINGS	85
                            #define DHTPIN		7
                            int dht11_dat[5] = { 0, 0, 0, 0, 0 };

                            void read_dht11_dat()
                            {
                             uint8_t laststate	= HIGH;
                             uint8_t counter		= 0;
                             uint8_t j		= 0, i;
                             float	f; 

                             dht11_dat[0] = dht11_dat[1] = dht11_dat[2] = dht11_dat[3] = dht11_dat[4] = 0;

                             pinMode( DHTPIN, OUTPUT );
                             digitalWrite( DHTPIN, LOW );
                             delay( 18 );
                             digitalWrite( DHTPIN, HIGH );
                             delayMicroseconds( 40 );
                             pinMode( DHTPIN, INPUT );

                             for ( i = 0; i < MAXTIMINGS; i++ )
                             {
                              counter = 0;
                              while ( digitalRead( DHTPIN ) == laststate )
                              {
                               counter++;
                               delayMicroseconds( 1 );
                               if ( counter == 255 )
                               {
                                break;
                               }
                              }
                              laststate = digitalRead( DHTPIN );

                              if ( counter == 255 )
                               break;

                              if ( (i >= 4) && (i % 2 == 0) )
                              {
                               dht11_dat[j / 8] <<= 1;
                               if ( counter > 50 )
                                dht11_dat[j / 8] |= 1;
                               j++;
                              }
                             }

                             if ( (j >= 40) &&
                                  (dht11_dat[4] == ( (dht11_dat[0] + dht11_dat[1] + dht11_dat[2] + dht11_dat[3]) & 0xFF) ) )
                             {
                              f = dht11_dat[2] * 9. / 5. + 32;
                              printf( "Humidity = %d.%d %% Temperature = %d.%d C (%.1f F)\n",
                               dht11_dat[0], dht11_dat[1], dht11_dat[2], dht11_dat[3], f );
                             }else  {
                              //printf( "Data not good, skip\n" );//
                             }
                            }

                            int main( void )
                            {
                             printf( "Raspberry Pi wiringPi DHT11 Temperature test program\n" );

                             if ( wiringPiSetup() == -1 )
                              exit( 1 );

                             while ( 1 )
                             {
                              read_dht11_dat();
                              delay( 1000 ); 
                             }

                             return(0);
                            }
 
 
 It might Look something Like This : 
 
 
 <img width="1440" alt="Screen Shot 2022-09-29 at 3 40 36 PM" src="https://user-images.githubusercontent.com/107719838/193126677-eb40cba2-c169-4a99-801d-a17f7a3759eb.png">
 
 
 
 To Execute the Program : 
 
 Run the following command :                      
                             
                              gcc -o temparature temperature.c -lwiringPi -lwiringPiDev
                              
                              
 If You get any Error at This point 
 
                            
                            sudo Dietpi-Software
 
 

  And search for the Wiring Pi software :
  
  
 <img width="566" alt="Screen Shot 2022-09-29 at 3 29 03 PM" src="https://user-images.githubusercontent.com/107719838/193127678-ebdcfe0a-b5b1-45ea-9ade-c441297e9025.png">
 
 
 Install the Wiring Pi Software and run the same gcc command again : 
 
                             gcc -o temperature temperature.c -lwiringPi -lwiringPiDev
                             
 
 To execute The program 
 
                            ./ temperature


We get the Output something like this :



<img width="1440" alt="Screen Shot 2022-09-29 at 11 35 45 AM" src="https://user-images.githubusercontent.com/107719838/193128499-af967959-ae4f-4061-9f5a-a2ee4b65cb44.png">


![IMG_4436-min](https://user-images.githubusercontent.com/107719838/193128950-cd76ea78-bdb1-470b-842f-c4badc3745c7.PNG)


# VIDEO OF THE WORKING ENVIRONMENT 


https://user-images.githubusercontent.com/107719838/193129252-e1ed669c-9d8d-4c01-bcee-1dc8c0a370f2.mp4





# PERFORMING THE TUTORIAL IN THE ARDUINO IDE 


1. Download and install the Arduino IDE from:

                       https://www.arduino.cc/en/software

2. In Arduino IDE, go to 

                       File -> Preferences.

3. Add the below url to the Additional boards manager Urls:

                        https://dl.espressif.com/dl/package_esp32_index.json
                        

4. Go to Tools -> Board -> Boards Manager. Search for esp32 and install the “ESP32 by Espressif Systems”


5. Select the relevant board. Tools -> Board -> esp32 -> ESP32 Wrover Module.


<img width="218" alt="Screen Shot 2022-09-29 at 4 03 49 PM" src="https://user-images.githubusercontent.com/107719838/193131133-c767bafc-12da-46fb-9b8c-d17e1a26e111.png">


<img width="277" alt="Screen Shot 2022-09-29 at 4 02 56 PM" src="https://user-images.githubusercontent.com/107719838/193131143-1735e112-0433-46ff-8d54-92e8975c79dd.png">



<img width="951" alt="Screen Shot 2022-09-29 at 4 02 25 PM" src="https://user-images.githubusercontent.com/107719838/193131187-f11f39fc-8089-41ab-8205-e1263693c5d2.png">

# Test the ESP32 circuit

1. Connect the ESP32 board to your laptop/computer with the USB cable provided with the Freenove kit

2. Go to Tools -> Port. Select the COM4 port.

3. Download the Zip file of the external library from: https://github.com/beegee-tokyo/DHTesp

4. Go to Sketch -> Include Library -> Add .ZIP Library…. Select the .zip file from your computer.

5. Copy the code from page 271 of the C_Tutorial and paste in a .ino file. You can save the file as a new sketch.

I've taken Code from the freenove Kit Tutorial Pdf : 

                    
                    #include "DHTesp.h"
                    DHTesp dht; //Define the DHT object
                    int dhtPin = 13;//Define the dht pin
                    void setup() {
                     dht.setup(dhtPin, DHTesp::DHT11);//Initialize the dht pin and dht object
                     Serial.begin(115200); //Set the baud rate to 115200
                    }
                    void loop() {
                     flag:TempAndHumidity newValues = dht.getTempAndHumidity();//Get the Temperature and humidity
                     if (dht.getStatus() ! = 0) { //Judge if the correct value is 
                    read
                     goto flag; //If there is an error, go back to 
                    the flag and re-read the data
                     }
                     Serial.println(" Temperature:" + String(newValues.temperature) + 
                     " Humidity:" + String(newValues.humidity));
                     delay(2000);
                    }
                    
                    
6. Press the Upload button(right-arrow) at the top in Arduino IDE. Let the code compile and upload to your board.

7. After you see the ‘Done uploading’ message at the bottom, check the Serial Monitor tab.

8. Set the baud rate to be 115200 baud as per the C program.

9. You can see the temperature and humidity readings in the Serial Monitor.


<img width="358" alt="Screen Shot 2022-09-29 at 3 57 22 PM" src="https://user-images.githubusercontent.com/107719838/193131958-ab9fd41e-15e8-494c-b0bb-7324238c68d1.png">

There was a Fatal Head error in the intiall phase of compilation Later on I have used Other Desktop For the compilation of the Values with my equipment I have got the values for the sensor readings in the output.


# Comparision of how a different IDE would could be used for the same project ( comparing with Arduino and Pi ) 


Both Arduino and Raspberry Pi are good teaching tools for students, beginners and hobbyists. Let us see some of the differences between Raspberry Pi and Arduino.

The main difference between them is: Arduino is microcontroller board, while Raspberry Pi is a microprocessor based mini computer (SBC).
The Microcontroller on the Arduino board contains the CPU, RAM and ROM. All the additional hardware on Arduino Board is for power supply, programming and IO Connectivity. Raspberry Pi SBC has all features of a computer with a processor, memory, storage, graphics driver, connectors on the board.
Raspberry Pi needs an Operating System to run. Arduino doesn’t need any operating system. All you need is a binary of the compiled source code.
Raspberry Pi comes with a fully functional operating system called Raspberry Pi OS (previously known as Raspbian OS). Although Pi can use different operating systems, Linux is preferred by Raspberry Pi Foundation. You can install Android, if you want. Arduino does not have any operating system. You just need a firmware instructing the Microcontroller what task to do.
The clock speed of Arduino is 16 MHz while the clock speed of Raspberry Pi is around 1.2 GHz.
Raspberry Pi is good for developing software applications using Python, while Arduino is good for interfacing Sensors and controlling LEDs and Motors.
This doesn’t mean we cannot connect sensors and LEDs to Raspberry Pi. To encourage learning programming by controlling hardware, the Raspberry Pi consists of a 40-pin GPIO, through which you can connect different electronic components like LEDs, Buttons, Sensors, Motors etc. On Arduino, the GPIO is called as Digital IO (for digital Input and Output) and Analog IN (for Analog Input).
Using Arduino Shields, which plug into the Arduino Pin headers, you can add a dedicated feature or functionality like a Motor Driver, Ethernet Connection, SD Card Reader, Wi-Fi, Touchscreens, cameras etc. to Arduino. While Raspberry Pi is a self-contained board, you can add external hardware like Touchscreen, GPS, RGB panels etc. to Raspberry Pi. The Raspberry Pi Hardware Attached on Top or HAT Expansion Boards are inspired by Arduino Shields, using which you can add additional functionality to Raspberry Pi. They are connected to the GPIO Pins.
The power requirements of Raspberry Pi and Arduino are completely different. Even though they both are powered by USB (micro-USB or USB Type C for Raspberry Pi and USB Type B for Arduino), Raspberry Pi needs more more current than Arduino. So, you need a power adapter for Raspberry Pi but you can power Arduino from the USB port of a Computer.
Power interruption for Raspberry Pi may cause damage to the hardware, software or applications. In case of Arduino, if there is any power cut it again restarts. So, Raspberry Pi must be properly shutdown before disconnecting power.
Arduino uses Arduino IDE for developing the code. While Raspberry Pi can use Python IDLE, Eclipse IDE or any other IDE that is supported by Linux. You can also program using the terminal itself with any text editor like Vim.
Using the open-source hardware and software files of Arduino, you can essentially create your own Arduino board. This is not possible with Raspberry Pi as it is not open-source.



<img width="1061" alt="Screen Shot 2022-09-29 at 4 18 56 PM" src="https://user-images.githubusercontent.com/107719838/193133687-4be29b19-7f16-4eab-99c7-3d99fdf50918.png">






# Additional URLS For this Experiment : 

https://www.thegeekpub.com/236867/using-the-dht11-temperature-sensor-with-the-raspberry-pi/

https://www.circuitbasics.com/how-to-set-up-the-dht11-humidity-sensor-on-the-raspberry-pi/

https://www.iotstarters.com/connecting-dht11-sensor-with-raspberry-pi-3-4-using-python/

https://www.theengineeringprojects.com/2022/04/interface-dht11-sensor-with-raspberry-pi-4.html







Hope This Tutorial Will Help to Git Users who are looking for this kid of experiment or the experiments similar to this ..                   
                    
                                     
