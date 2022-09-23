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






         ls -l /dev/ttyUSB*



<img width="470" alt="ttyusb*" src="https://user-images.githubusercontent.com/107719838/192060164-d9cb26bf-9fd7-4165-93ed-49a8baeb19d6.png">


                    
                    
    

