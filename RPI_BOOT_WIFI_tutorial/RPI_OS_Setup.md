# Setting up dietpi on a Raspberry PI via wifi

## HARDWARE INFORMATION FOR THE SETUP

1. 32 GB SD CARD 
2. LENTION USB C Hub with 4K HDMI, 3 USB 3.0, SD 3.0 Card Reader Compatible 2022-2016 
3. RPI USB-C POWER SUPPLY BLACK US (5.1V 15 W AC/DC External Wall Mount (Class II) Adapter Fixed Blade Input)
4. Raspberry Pi solid case with fan of 3.3v power supply.
5. GL.iNet GL-MT300N-V2(Mango) Router

## STEP 1

To accomplish finishing the setup we need to perform this step and this particular step is very important
Prepare you laptop with a sd card writer such as: balenaEtcher https://www.balena.io/etcher/
1. Download and Install the Etcher flash burn software

## STEP 2

Download the Diet Pi Disc image from the link : https://dietpi.com/#download
1. Go to Rspberry Pi and select the compatible version for your raspberry pi 
2. I have downloaded this particular version : https://dietpi.com/downloads/images/DietPi_RPi-ARMv8-Bullseye.7z 
3. Extract the Disc image to a particular folder.
4. Insert your SD card to your laptop
5. open etcher software and upload the Disc image and select the target drive as the SD card you have connected to your laptop
6. Select the flash option to burn the Disc image to your SD card
7. After the installing and validation of the Disc Image into your SD card Unplug the SD card from the device.
8. Close the Etcher Software.

## STEP 3

1. copy dietpi.txt and dietpi-wifi.txt to a local folder in your laptop/computer they can be found in the SD card data.
2. edit dietpi-wifi.txt with your router ssid and credentials
               
               aWIFI_SSID[0]='YOUR_ROUTER_NAME'
               aWIFI_KEY[0]='PASSWORD OF YOUR ROUTER'

3.edit dietpi.txt with these following set ups

              AUTO_SETUP_LOCALE=en_US.UTF-8
              AUTO_SETUP_KEYBOARD_LAYOUT=us
              AUTO_SETUP_TIMEZONE=America/New_York
              AUTO_SETUP_NET_ETHERNET_ENABLED=0
              AUTO_SETUP_NET_WIFI_ENABLED=1
              AUTO_SETUP_NET_WIFI_COUNTRY_CODE=US
              AUTO_SETUP_DHCP_TO_STATIC=1
              AUTO_SETUP_NET_HOSTNAME=DietPi_{YOUR_INITIALS}
              AUTO_SETUP_HEADLESS=1
              AUTO_SETUP_AUTOSTART_TARGET_INDEX=1
              SURVEY_OPTED_IN=0
              CONFIG_SERIAL_CONSOLE_ENABLE=1
              
Make sure to change {YOUR_INITIALS} with a locally unique string for me I used MP so HOST_NAME will be like DietPi_MP

Look for each variable before the = symbol and change the data according to the above format.

## Save the changes !!! ( This is very very important )

## STEP 4

1.In this step we will Install SD card onto the PI and powerup the PI to run DietPI which is considered as the crucial step for the whole installation process.
2.You should see the red led turn on and the green led will start to flash as the install is running
3. Wait until the green light has finished flashing - could take 5-10 minutes

## STEP 5

Using the admin website of your router at check the CLIENTS page for the IPADDR of the pi that is booted up.

<img width="1250" alt="Client image" src="https://user-images.githubusercontent.com/107719838/190363774-059b087a-aa6c-4599-91f8-17b504c1c46a.png">

After Detection of the CLIENT in the router admin panel use SSH to login into your PI using these commands

                    ssh root@YOUR_RPI_IP_ADDRESS
                    password: dietpi

make sure to you change your root login during setup from this point

<img width="1440" alt="Installation" src="https://user-images.githubusercontent.com/107719838/190364793-b71a209f-ac9e-42de-b596-23b770364330.png">







<img width="590" alt="booting" src="https://user-images.githubusercontent.com/107719838/190365187-cbf79b69-4a9a-41b4-8205-89b3fb546c16.png">







<img width="1440" alt="deit pi ssh" src="https://user-images.githubusercontent.com/107719838/190364941-b9946838-4f35-44b4-9dbe-6741993dd4f4.png">







<img width="1440" alt="Installation" src="https://user-images.githubusercontent.com/107719838/190365309-0ae76d4a-16b7-4781-8233-f7689a1ec9bd.png">






## STEP 6 

Once you are logged into the pi finish setup and follow these particular steps 

## Using DietPi-Config

## Change software and user passwords using the "Security Options"



<img width="1416" alt="user password change" src="https://user-images.githubusercontent.com/107719838/190365702-1c7d9868-df06-4d7e-af05-a90e75811946.png">


## STEP 7

You are now ready to start install IoT platform software.

Continue with other installs such as: [IOT_Platform_Installation](https://github.com/mudith2497/VU_FALL22_IOT_CLASS/blob/main/RPI_BOOT_WIFI_tutorial/IOT_Platform_Install.md) mostly by using diepi-software setup.












