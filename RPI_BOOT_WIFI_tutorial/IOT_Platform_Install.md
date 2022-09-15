# How to Setup your software to run an specific IOT Platform on your RPI 

## STEP 1

Make sure your laptop is connected to your router and Raspberry Pi is able to access the Diet Pi Terminal in your computer/Laptop

## STEP 2 


1. SSH to the RPI using dietpi user
          
          ssh dietpi@[YOUR_RPI_IP_ADDRESS]
   
## When you run it Make sure you see the Main Menu after all the previous settings



<img width="1440" alt="Main Menu" src="https://user-images.githubusercontent.com/107719838/190369407-6a7ba522-29fa-4078-a202-380c14cef671.png">


## In this Menu select for Search Software option and toggle your arrows to select " OK " and press " Enter "


<img width="1440" alt="Search software" src="https://user-images.githubusercontent.com/107719838/190370748-57868eb9-1416-47b4-a2ee-4acfb8239b4b.png">



## STEP 3

1. Search for " mqtt " and select the " 123 MQTT " message and install by hitting the spacebar ( while hitting the spacebar we get the * symbol which means that particular package is selected.


<img width="1440" alt="mqtt" src="https://user-images.githubusercontent.com/107719838/190370523-327438c5-7ebd-4c08-b177-9a5feb0c5c80.png">





2. Search for " node-red " and select "122 Node-RED: tool for wiring devices, APIs and online services"message and install by hitting the spacebar ( while hitting the spacebar we get the * symbol which means that particular package is selected.



<img width="1440" alt="node red" src="https://user-images.githubusercontent.com/107719838/190371900-eec017bf-9f38-4bc8-ab04-8e1b959cfecd.png">






3. search for postgress and select "194 PostgreSQL: Persistent advanced object-relational database server" But That search Did not work Please search for the keyword " PostgreSQL " ( in the search software tab )and install by hitting the spacebar ( while hitting the spacebar we get the * symbol which means that particular package is selected.




<img width="1440" alt="post gresql" src="https://user-images.githubusercontent.com/107719838/190372643-fb7f164c-aa35-4e39-a7a7-2a47d01039c4.png">




4. After Selecting the above softwares the Installation Program should indicate these :




<img width="1440" alt="pre installation" src="https://user-images.githubusercontent.com/107719838/190373172-02534c14-a893-4b1f-9308-c9e142d30cec.png">





5. SELECT " OK " to continue the installation Process it might take sometime please be patient and wait for the Installation to be completed 




During the Installation it might look like this 



<img width="1440" alt="Installation" src="https://user-images.githubusercontent.com/107719838/190373678-4269beee-51be-477a-b7cc-30201f556c98.png">






## STEP 4

## Running the POSTGRES

1. run on your pi ssh session by this command " sudo su postgres" you can refer the image below



<img width="1440" alt="SUDO" src="https://user-images.githubusercontent.com/107719838/190374761-f080f6c5-2e47-434b-8ecb-3f9c08c2845d.png">




2. similarly type the following commands into the next steps 
            
                createuser pi -P --interactive ( this creates a user for SQL queries )
                (Enter a password after this step and remember that password)
                (select NO for superuser, and YES for the next two questions in the terminal itself.)
                
                psql
                
                create database test;
                
3. exit from the psql shell and again from the Postgres user by pressing Ctrl+D twice on your laptop and later on Type these commands 

              sudo su postgres ( Like previously )
              
              psql test
              
              create table people (name text, company text);
              

4. Now add data to the table you have created 

              
              insert into people values ('Ben Nuttall', 'Raspberry Pi Foundation');
              insert into people values ('Rikki Endsley', 'Red Hat');

5. Perform a test that the shows the data :

              select * from people; ( Type this command )
              



6. The Test result output would be something like this :



<img width="1440" alt="psql test output" src="https://user-images.githubusercontent.com/107719838/190377344-ca79cbab-052e-4add-b00a-1c598aa8a491.png">




## STEP 5 


This step is about how to link and perform actions on NODE RED on RPI

1. Connect to node-red to see that it is working by using your raspberry Pi {IP_ADRESS}

          http://YOUR_RPI_IP_ADDRESS:1880 ( Go to this link and see whether your IP ADDRESS is popping up in the browser )
          
 
 
 It looks something like this :
  
  
  
  <img width="1435" alt="node red output" src="https://user-images.githubusercontent.com/107719838/190379886-03ba4361-045a-48b2-a8b7-38b7580ff2bb.png">
  
  
  
  
  
  
  
  2. Install node-red-contrib-re-postgres in your ssh command line using: " npm install node-red-contrib-re-postgres "
 
     
     Restart node-red with the command :  " dietpi-services restart node-red " 
     
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  3. Go to Manage Pallet in your node-red browser and search for " install node-red-contrib-postgresql "  This particular Model must be downloaded in Node-red browser.
 
 
 
 
 

<img width="1440" alt="install node redpostgresql module" src="https://user-images.githubusercontent.com/107719838/190380877-758c0633-a321-4e71-87a0-75be9356deb8.png">










<img width="1249" alt="flow graphsheet" src="https://user-images.githubusercontent.com/107719838/190381354-4950c8ad-da5b-492d-a6c6-5f5569b7c516.png">






4.Install should note that it is working and later on on the top left corner you can search for the node tags or titles.


5.pull a postgres node into a flow from the search bar and pull it in the graph interface.



6. Pull in a trigger and template node and debug node and wire (  you can search all these titles in the top left search bar )


trigger->template->Postgres->debug


after dragging and dropping all the node titles into the graph we can connect each and every node as mentioned above

It looks something like this : 



<img width="1250" alt="final flowchart " src="https://user-images.githubusercontent.com/107719838/190382030-f389e747-8e2e-41c2-a667-5a6f3b9e8556.png">






     
     
     

  
  
  
  
  
  
  
  

  



                




























































