

![image](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/49fb0a2f-13c8-4842-8e99-271f90f5629f)





<h1>Using a Raspberry Pi 4 as an at-home Print Server via Linux</h1>

<h2>Project Summary</h2>
This project involves the utilization of a Raspberry Pi as a print server via the Linux command line. For those who may not know, a Raspberry Pi is a single-board computer that can be used to surf the web, code with Python, practice Linux commands, and build many home-lab projects. While many devices at home or work can easily communicate with their printer wirelessly, sometimes the connection is not reliable. Therefore, a Raspberry Pi can function as a server, serving as the intermediary between a device and a printer. If your printer only works through a wired USB connection, the Raspberry Pi print server project will allow wireless printing from any device. This is because the server (Raspberry Pi) is working on our behalf to communicate with the printer. 
<h2>Platforms and Technologies Used</h2>

- Raspberry Pi (8 GB or more micro SD card)
- USB Cable (Connect Raspberry Pi to Printer)
  - * Not required (Can work wirelessly)  
- Working Printer
- Bash Terminal (How we communicate with our Linux OS)
- CUPS (Open-Source Unix interface that communicates with our printer)
  - * This will be downloaded onto our Raspberry Pi)  
- Wi-Fi or Ethernet Cable 
- Mouse 
- Keyboard

<h2>Operating System Used </h2>

- Raspbian OS
  - * There are a multitiude of different Linux distributions that can be installed on a Pi (Kali Linux, etc.)
    * However, the installation of this project will be on Raspbian OS


<h2>Sources and Credit </h2>

- https://www.tomshardware.com/how-to/raspberry-pi-print-server (Les Pounder)
- https://pimylifeup.com/raspberry-pi-print-server/ (Gus)


<h2>Project Installation Steps</h2>

- Step 1
  - Open the bash terminal by clicking on the icon to the right of the folders (black box with blue streak on top)
![Photo1](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/61759084-f118-45a0-8fb6-7fd0f3e26b5b)


- Step 2  - Before we download anything, we need to make sure that our Pi is up to date. 
  - Input the sudo apt update && sudo apt upgrade commands in the terminal
    - The apt update command will update all of our repositories, while the apt upgrade command will actually download these latest updates to our system
  - * IMPORTANT - in order to run these commands, you will need to type in sudo (superuser do)
    * To run these commands you will need to add yourself to the sudo group, which can be done by inputting sudo usermod -aG sudo username
    * When you are asked whether you will like to download the lastest packages/updates, input "Y" in the terminal
 ![Photo2](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/e10eb2d5-fc9b-4bb6-bd58-0c08f26d4e9d)


- Step 3
  - Input the command sudo apt install cups into the bash terminal
    - This will install CUPS onto our Pi
   
  
![Photo3](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/3f0f04d9-1079-468f-bbdd-019a4801bef7)




- Step 4
  - Now, we need to add ourself to the list of users that can access printers
    - Input the command sudo usermod -a -G lpadmin (username)

![Photo4](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/40c89552-4510-4f65-8c7a-4d1edcde67f7)



- Step 5
  - Since our Raspberry Pi will serve as a print server, we are going to want the device to have a static IP address
    - This is typical for different kinds of servers - you want to know the IP address of the server to get it up and running
  - Type in the command "sudo nano /etc/dhcpcd.conf" - nano is a text editor and we will configure our static IP within this file
   ![Photo5](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/06ae8dd2-6136-4fb6-a922-eb0c834526be)


- Step 6
  - At the bottom of the file, under "Static CUPS ip address", we can enter in the following as shown below
   ![Photo6](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/b88c8b43-a2fa-4280-a31a-b23d5931de75)

    - To find the IP address of your Pi, type the command "sudo hostname -I" or "ifconfig | grep inet"
  
   ![Photo8](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/c2205b38-e504-4202-b8bd-7b7daceb876b)
  - To find the gatway address or IP address of your router, enter the "ip route | grep default" command into the terminal
  - To find your DNS server, enter the "sudo cat /etc/resolv.conf" command into the terminal 


- Step 7
  - We also want to make sure that we can access our Pi print server from any device in our home or work setting
    - To do this, we will enter the "sudo cupsctl --remote-any" command into our terminal 
![Photo7](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/3cf40a25-f0b2-4a7a-9baa-a4182517088c)


- Step 8
  - On our Pi, we will now go to the internet and type some information into our web browser
    - In the web browser, we will type in the IP address of our Pi, followed by a colon with the port number 631
    - Port 631 is the port number for IPP (Internet Printing Protocol), which is how CUPS communicates with our printer
     * IMPORTANT - our web browser says "not secure" because we have not established a certificate that uses https instead of http
        * We are communicating directly with our device and are not communicating over the internet
        * I strongly recommend that any information entered into this web page, such as the username and password of your device needs to be changed after this project
        * Even though this is over your home network, information entered into this web browser is not encrypted, but in plain text
        * If someone is snooping network traffic on your home network, they will be able to see this information - make sure your network is secure and PROCEED AT YOUR OWN RISK
      
          
  ![Photo9](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/60bcfa12-0183-4633-9312-a89a54fa0126)



- Step 9
  - Select the "Administration" tab at the top of the page
   ![Photo10](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/6effe027-316a-44d1-b812-19f41854d2e4)



- Step 10 
  - Under the Printer section, we want to select the "Add Printer" option
   ![Photo11](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/07a15074-3c1c-47fa-b262-7ec32b301507)



- Step 11
  - You should see a list of printers that are available (Network and Local printers)
    - I selected "Network Printers" since my printer does not have any USB connection
  - From there, you can choose to share your printer, meaning, when your computer is on, other users can print to your printer
    - However, we already entered a command to make our print server accessible to any device, so this does not matter
     ![Photo12](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/605cd668-2f12-4454-9042-c884c96689be)



  - Step 12
    - Once you select continue, you should see the different drivers listed for your printer
    - Usually the one selected is what matches your printer, however, the driver selected may not be the right one
    - Once you have found the correct driver, select "Add Printer"
     ![Photo13](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/59cc5b3b-98ea-4cad-966e-13d69c2553bd)
   


- Step 13
  - I did not need any banners, so I selected "none" and pressed "set deafult options"
   ![Photo14](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/f3090069-0ca3-42e0-89ac-72ee95d09904)
 


- Step 14
  - Under the "Printers" tab, you should see your newly installed printer
  - Click on your printer under "Queue Name"
   ![Photo15](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/deec7956-1804-4f66-8072-804a774cdfc5)



Step 15 
- Navigate to the "Maintenance Tab" and change it to "Print Test Page"
  ![Photo16](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/f6c30392-2257-4362-a6b0-269750306fee)
 


Step 16 
- Look at our test page below

  ![IMG_2507](https://github.com/chriskhawaja/PiPrintServer/assets/153021794/2637c8d6-0914-4fa3-88c0-5c54590eef18)



- We have now created turned our Raspberry Pi into a working print server!
  - * IMPORTANT - It is essential to secure any server you have working on your system
    * I recommend downloading a firewall onto your Pi such as UFW (Uncomplicated Firewall) and an Anti-Malware program such as Clam AV
      * I hold no responsibility for any print server that is unsecure, make sure to secure your server!
  

**** Picture used at the top of personal project is not mine (taken from Google)
