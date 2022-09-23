# Install software to build ESP32 code


## Instructions



1. Clone Anjay-esp32-client repo to raspberry pi


        cd projects

        git clone --recurse-submodules --remote-submodules https://github.com/pschragger/Anjay-esp32-client

should take less then a minute

Install build tools for ESP-IDF

       sudo apt-get install git wget flex bison gperf python3 python3-pip python3-setuptools cmake ninja-build ccache libffi-dev libssl-dev dfu-        util libusb-1.0-0
       
 <img width="690" alt="sudo 1 " src="https://user-images.githubusercontent.com/107719838/192062904-58930f6e-d9e2-4632-9f1b-504945682937.png">

       
       
       
             mkdir -p ~/esp
             cd ~/esp
             git clone -b v4.4 --recursive https://github.com/espressif/esp-idf.git
             
   <img width="1440" alt="anjay download" src="https://user-images.githubusercontent.com/107719838/192062285-d64ee910-4a01-48bb-b8d8-e1d4c6e10e9b.png">


<img width="686" alt="esp idf" src="https://user-images.githubusercontent.com/107719838/192062327-d2ee4abc-153f-46a0-890b-a2ebcec731c7.png">




               cd ~/esp/esp-idf
               ./install.sh all
               
               
 Setting up Environment Variables 
 
                . ~/esp/esp-idf/export.sh
                
                cd ~/esp
                cp   -r $IDF_PATH/examples/get-started/hello_world .
                
                 ~/esp/esp-idf/export.sh
              
              cd $IDF_PATH/examples/get-started/hello_world 
              idf.py set-target esp32
              idf.py fullclean
              idf.py menuconfig
              
  <img width="566" alt="5000-1" src="https://user-images.githubusercontent.com/107719838/192062551-f31cec26-a8a1-4902-a404-41c7e1a59b3a.png">
  
               
               idf.py build
               
               find the usb that the esp is connected to
               
               by using lusb
               
  <img width="548" alt="USB PORT DETAILS" src="https://user-images.githubusercontent.com/107719838/192062725-ca1dbb62-e8db-4dd2-9559-fe295e12c9d3.png">
  
         
           
             ls -l /dev/ttyUSB*
      
 <img width="470" alt="ttyusb*" src="https://user-images.githubusercontent.com/107719838/192062803-386bca6c-a6b0-410e-a406-a5690412d4bb.png">
 

  <img width="415" alt="FLASH" src="https://user-images.githubusercontent.com/107719838/192063002-3bd0e94c-a209-437f-8655-79d96a27ac7b.png">
  
  
             idf.py -p /dev/ttyUSB0 monitor
             

 <img width="1440" alt="Hello world " src="https://user-images.githubusercontent.com/107719838/192063075-b52b9315-c20d-4e22-a2dc-000f06c95a2e.png">
 
                   . ~/esp/esp-idf/export.sh
                   cd ~/esp
                   cp   -r $IDF_PATH/examples/get-started/blink .
                   
                   
                    ~/esp/esp-idf/export.sh
                    cd $IDF_PATH/examples/get-started/blink 
                    idf.py set-target esp32
                    idf.py fullclean
                    idf.py menuconfig
                    
                    
                    
                cd $IDF_PATH/examples/get-started/blink idf.py build  
                
                cd ~/esp/esp-idf/examples/get-started/blink/main
                
                nano blink_example_main.c
                    
   <img width="1440" alt="NANO C program" src="https://user-images.githubusercontent.com/107719838/192063362-ebcb0668-c508-4594-a9a6-7c762348414b.png">
   
   
   
                   cd ~/esp/esp-idf/examples/get-started/blink
                   idf.py menuconfig
                   

1. navigate to the "Example Configuration" and hit enter
2. . there are two settings Blink GPIO number and Blink Perion in ms
3. change the blink period in ms to 5 seconds ( 5000 ) 
4. save the results to the sdkconfig (S then Q )
     
                    
 <img width="566" alt="5000-1" src="https://user-images.githubusercontent.com/107719838/192063206-e459ed85-eee5-4e96-a373-ecfd169c1456.png">
   
   
                 
<img width="561" alt="5000-2" src="https://user-images.githubusercontent.com/107719838/192063216-dba8d50a-62e6-42de-8650-d20d6ca0631f.png">

 
 
  
               
               
               
               
               
       

               



               
