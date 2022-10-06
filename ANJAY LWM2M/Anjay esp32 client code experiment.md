# Building an LWM2M clients on RPI for ESP32

## now to build a LWM2M Device using idf and the ANJAY Libraries

## Install C compiler

Test to see if the c compiler is already installed using

                gcc -v
              
               If installed then go to the next step if not then use 'sudo dietpi-software'  on the PI to install gcc 
               

<img width="1438" alt="gcc -v" src="https://user-images.githubusercontent.com/107719838/192058607-5573400e-1a64-4353-910c-57f4b7137686.png">

                
                cd ~/projects git clone https://github.com/AVSystem/avs_commons
                
<img width="576" alt="git avs systems" src="https://user-images.githubusercontent.com/107719838/192058724-f4bc8ac7-d4d0-4c1a-bdd8-6d1eda23a199.png">



2. Build and install the avs_commons library

                  cd ~/projects/avs_commons cmake . && make && sudo make install
                  
                  
  <img width="558" alt="avs commons git" src="https://user-images.githubusercontent.com/107719838/192059526-4f79e059-1ad0-4e4a-b138-a959ca9130af.png">

  
   
3. Build Anjay code    
   
                    cd ~/projects git clone https://github.com/AVSystem/Anjay
                    
                    
<img width="353" alt="CD ANJAY" src="https://user-images.githubusercontent.com/107719838/192059188-24b2ea4c-8f5b-4449-89cf-61a9ab1cc974.png">



                    cd ~/projects/Anjay git submodule update --init cmake . -DDTLS_BACKEND="mbedtls" make -j
                    
                    
 
 <img width="1294" alt="ANjay cmake" src="https://user-images.githubusercontent.com/107719838/192059508-79c2b62f-f7c8-4cd2-9315-bae057767b32.png">

                    

try the anjay demo

-- view the leshan test server at https://leshan.eclipseprojects.io/#/clients
-- run the demo and see your machine listed in the leshsn server   

          
          
            output/bin/demo --endpoint-name $(hostname) --server-uri coap://leshan.eclipseprojects.io:5683
            
            
<img width="1440" alt="$hostname" src="https://user-images.githubusercontent.com/107719838/192059817-5fd59ae3-283f-433e-98a5-0f3fab65cb3a.png">            





            
   
            
<img width="590" alt="booting" src="https://user-images.githubusercontent.com/107719838/192059906-bde5fb22-7d81-4165-9cd7-ed421accaf6e.png">
   
            
 
            
<img width="1387" alt="public leshan server my diet pi " src="https://user-images.githubusercontent.com/107719838/192059609-a86a67e9-4fd9-4375-9cd2-5f79272195ac.png">


## I FOUND MY DIETPI INN PUBLIC LESHAN SERVER 

  
  
  

  
  
 <img width="1440" alt="build target anjay" src="https://user-images.githubusercontent.com/107719838/192059933-c230fd1e-cb16-4783-b186-5185cc8044e5.png">
  
  
  
  
  
       cd ~/projects/Anjay cmake -DCMAKE_INSTALL_PREFIX=/home/dietpi/projects/Anjay-esp32-client . && make && make install


  
              
 <img width="1294" alt="ANjay cmake" src="https://user-images.githubusercontent.com/107719838/192059883-34022201-929f-4337-b429-b54dcf57a7f4.png">

 
 
 
 
                    cd ~/projects/Anjay-esp32-client
 
<img width="1440" alt="Build target download" src="https://user-images.githubusercontent.com/107719838/192059970-920e5399-17db-4d2c-ac9a-9b819f576d50.png">





        cd ~/projects/Anjay-esp32-client . $HOME/esp/esp-idf/export.sh idf.py set-target esp32


<img width="686" alt="esp idf" src="https://user-images.githubusercontent.com/107719838/192060076-54a139d5-63d3-4de8-a53a-38b59f2dbdb4.png">



## NEXT STEP IS TO INITIATE THE MENUCONFIG FOR THE ANJAY ESP32 CLIENT FOR LED EXPERIMENT 


   setup the device requirements
   
      cd ~/projects/Anjay-esp32-client
      idf.py menuconfig
      


## Test the Leshan server
                 
                 cd ~/projects/leshan
                 java -jar leshan-server-demo/target/leshan-server-demo-*-SNAPSHOT-jar-with-dependencies.jar &
                 
                 http://{RPI-IP_ADDRESS}:8080
                 
                 
                 java -jar leshan-client-demo/target/leshan-client-demo-*-SNAPSHOT-jar-with-dependencies.jar
                 

These commands will start the leshan server 




 Give it sometime and later on we may see the screen like this :
 
 
 <img width="564" alt="Screen Shot 2022-10-06 at 12 33 55 AM" src="https://user-images.githubusercontent.com/107719838/194393526-362fb851-bde6-4329-a0a7-76c2b176da79.png">

### Follow these steps carefully 

1. navigate to "Component configuration ->" and select config/anjay-esp32-client :

2. After selecting the Anjay ESP32 client in the which is available in the last of the list 


<img width="1440" alt="Screen Shot 2022-09-29 at 8 28 17 PM" src="https://user-images.githubusercontent.com/107719838/194398033-6fd5aaca-f482-4e81-95b0-0311d67a1726.png">



3. navigate to "Board options - > " and select the * Light control enable with your spacebar


<img width="559" alt="Screen Shot 2022-10-06 at 12 41 34 AM" src="https://user-images.githubusercontent.com/107719838/194394959-6fa06559-f69d-4296-81fd-ca1a34a103f1.png">



4. After enabling the light control later go to light control settings and set up ur desired LED and mention pin number as per ESP32 CIRCUIT


<img width="565" alt="Screen Shot 2022-10-06 at 1 32 43 AM" src="https://user-images.githubusercontent.com/107719838/194395064-6445663a-830f-4cfd-8fb1-631ab6c86946.png">

5. navigate to "Client options ->"

Change Server URI from coaps://try-anjay.avsystem.com:5684 to coaps://YOUR_LESHAN_SERVER_IP_ADDR:5684 I used coap://192.168.8.214:5683 which is my unique raspberry pi IP address.

6. SET your end point name which will be reflected in the Leshan server


<img width="559" alt="Screen Shot 2022-10-06 at 12 36 36 AM" src="https://user-images.githubusercontent.com/107719838/194395624-e88e25d6-5146-4a03-9ab0-35f622e2f423.png">


7. navigate to "WiFi ->" To enter your IOT ROUTER WIFI SSID and key to allow the esp32 acccess to your router and PI.

<img width="563" alt="Screen Shot 2022-10-06 at 12 37 47 AM" src="https://user-images.githubusercontent.com/107719838/194395929-e4c9e4e5-b5bc-4f9d-b158-94a99a329ab8.png">


8. Dont Forget to save the settings press " S " and save all the changes you've made 

9. Build the code for the device using

                    cd ~/projects/Anjay-esp32-client
                    idf.py build
 
10. find the port and flash the device

    find port number by using

                    ls -l /dev/ttyUSB*

11. change the port number in this line to load the code idf.py -p port_number flash with port nubmer = 0 I used:

            cd ~/projects/Anjay-esp32-client
            sudo chmod 666 /dev/ttyUSB0
            idf.py -p 0 flash 
            
12.   In leshan server check your endpoint name and go to the settings of " mpotta " which is my endpoint name and select light control enter         the boolean values like " True " " False " to turn the light ON and OFF. 


<img width="1440" alt="Screen Shot 2022-10-06 at 2 04 33 AM" src="https://user-images.githubusercontent.com/107719838/194398404-4bb8f125-47f0-4399-a74e-d54ad1c60e8f.png">

13. Here is my working image and video of the led experiment :


![IMG_4484](https://user-images.githubusercontent.com/107719838/194399554-a5a2ad37-51c9-438e-a164-43e523336a54.jpg)



https://user-images.githubusercontent.com/107719838/194400433-fe979f7a-2cd6-4fbc-9c74-d84624b759f3.mp4




## Circuit diagram for this experiment 

<img width="1086" alt="Screen Shot 2022-10-06 at 3 23 43 PM" src="https://user-images.githubusercontent.com/107719838/194401246-0b3fc7a7-07dc-4c26-9a30-a1823d877d8a.png">



## NEXT STEP IS TO INITIATE THE MENUCONFIG FOR THE ANJAY ESP32 CLIENT FOR PUSH BUTTON EXPERIMENT 

setup the device requirements
   
      cd ~/projects/Anjay-esp32-client
      idf.py menuconfig
      


## Test the Leshan server
                 
                 cd ~/projects/leshan
                 java -jar leshan-server-demo/target/leshan-server-demo-*-SNAPSHOT-jar-with-dependencies.jar &
                 
                 http://{RPI-IP_ADDRESS}:8080
                 
                 
                 java -jar leshan-client-demo/target/leshan-client-demo-*-SNAPSHOT-jar-with-dependencies.jar
                 

These commands will start the leshan server 


 Menu config portal : 
 
 <img width="564" alt="Screen Shot 2022-10-06 at 12 33 55 AM" src="https://user-images.githubusercontent.com/107719838/194393526-362fb851-bde6-4329-a0a7-76c2b176da79.png">
 
 
 

### Follow these steps carefully 

1. navigate to "Component configuration ->" and select config/anjay-esp32-client :

2. After selecting the Anjay ESP32 client in the which is available in the last of the list 


<img width="1440" alt="Screen Shot 2022-09-29 at 8 28 17 PM" src="https://user-images.githubusercontent.com/107719838/194398033-6fd5aaca-f482-4e81-95b0-0311d67a1726.png">

3. navigate to "Board options - > " and select the * Push button enable with your spacebar



<img width="562" alt="Screen Shot 2022-10-06 at 2 23 52 AM" src="https://user-images.githubusercontent.com/107719838/194402264-2a637397-cd31-4e83-b6a5-a8af5b4ab66b.png">

4. After enabling the push button control later mention pin number as per ESP32 CIRCUIT I have taken pin number 35. 

5. navigate to "Client options ->"

Change Server URI from coaps://try-anjay.avsystem.com:5684 to coaps://YOUR_LESHAN_SERVER_IP_ADDR:5684 I used coap://192.168.8.214:5683 which is my unique raspberry pi IP address.

6. SET your end point name which will be reflected in the Leshan server


<img width="559" alt="Screen Shot 2022-10-06 at 12 36 36 AM" src="https://user-images.githubusercontent.com/107719838/194395624-e88e25d6-5146-4a03-9ab0-35f622e2f423.png">


7. navigate to "WiFi ->" To enter your IOT ROUTER WIFI SSID and key to allow the esp32 acccess to your router and PI.

<img width="563" alt="Screen Shot 2022-10-06 at 12 37 47 AM" src="https://user-images.githubusercontent.com/107719838/194395929-e4c9e4e5-b5bc-4f9d-b158-94a99a329ab8.png">


8. Dont Forget to save the settings press " S " and save all the changes you've made 

9. Build the code for the device using

                    cd ~/projects/Anjay-esp32-client
                    idf.py build
 
10. find the port and flash the device

    find port number by using

                    ls -l /dev/ttyUSB*

11. change the port number in this line to load the code idf.py -p port_number flash with port nubmer = 0 I used:

            cd ~/projects/Anjay-esp32-client
            sudo chmod 666 /dev/ttyUSB0
            idf.py -p 0 flash 
            
12. In leshan server check your endpoint name and go to the settings of " mpotta " which is my endpoint name and select push button control press the push button in the circuit. The count of the number of times button pressed can be seen in the leshan server.


<img width="1190" alt="Screen Shot 2022-10-06 at 2 34 08 AM" src="https://user-images.githubusercontent.com/107719838/194403265-91845105-8022-498b-8ab3-c155e6c73f34.png">


13. Here is my working image and video of the push button experiment :

![IMG_4492](https://user-images.githubusercontent.com/107719838/194403824-7a08a35a-60bd-436e-8b18-923943f819a4.jpg)


https://user-images.githubusercontent.com/107719838/194404257-e61b7e14-b025-48b0-9bb5-3abe4ace35c7.mp4

### In the video you can see the previous count as '8' and later on after pressing the push button 5 times " 8+5 " it updates " 13 " as value 



## Circuit diagram of the Push button Experiment 


<img width="682" alt="Screen Shot 2022-10-06 at 4 01 03 PM" src="https://user-images.githubusercontent.com/107719838/194407405-b8af839a-150a-480a-8374-d5321b888501.png">





## OTHER EXPERIMENT USING DIETPI IN ECLIPSE PROJECTS IN PUBLIC LESHAN SERVER ( Additional Experiment )



## 1. START the Leshan server
                 
                 cd ~/projects/leshan
                 java -jar leshan-server-demo/target/leshan-server-demo-*-SNAPSHOT-jar-with-dependencies.jar &
                 
                 http://{RPI-IP_ADDRESS}:8080
                 
                 
                 java -jar leshan-client-demo/target/leshan-client-demo-*-SNAPSHOT-jar-with-dependencies.jar
                 
2. Go to the link you should be seeing your Diet pi 

3. Continue the Menu config Process and follow the above process and we should make a single change 

4. view the leshan test server at https://leshan.eclipseprojects.io/#/clients -- run the demo and see your machine listed in the leshsn server

5. Run this particular command 

              output/bin/demo --endpoint-name $(hostname) --server-uri coap://leshan.eclipseprojects.io:5683

6. We should change the server ID to public leshan server :


<img width="557" alt="Screen Shot 2022-09-29 at 8 37 41 PM" src="https://user-images.githubusercontent.com/107719838/194405692-ab4fb5e6-c085-48e1-8c44-022620713307.png">

7. Go to the https://leshan.eclipseprojects.io/#/clients in your Diet Pi Information we can fetch the Temperature Level of our Raaspberry Pi 


<img width="1199" alt="Screen Shot 2022-10-06 at 3 54 39 AM" src="https://user-images.githubusercontent.com/107719838/194406067-b81110ef-a175-4546-ac3e-7c2bb87f55a5.png">


### We can see reading of sensor value and MIN and MAX temperatures of the Diet Pi controller and also the Units of the temperature in Celsius.


8. We can Also configure the LWM2M DEVICE CONNECTED TO DIET PI " The ESP32 " Hardware information can be seen in the public leshan eclipse projects server I have fetched these values 

<img width="1181" alt="Screen Shot 2022-10-06 at 3 50 19 AM" src="https://user-images.githubusercontent.com/107719838/194406877-c2ced2db-cb2a-4b59-944c-a3124b3d84dc.png">

<img width="1187" alt="Screen Shot 2022-10-06 at 3 51 12 AM" src="https://user-images.githubusercontent.com/107719838/194406915-cce1e1b0-58cb-4188-bdc7-bd951e60def4.png">

Thus I have done Three different types of experiments and Here are the URLS for the Reference of the following experiments :

https://microcontrollerslab.com/push-button-esp32-gpio-digital-input/

https://esp32io.com/tutorials/esp32-led-blink

https://github.com/nikoshet/BPMS-Leshan-with-RPi

