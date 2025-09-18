# Pi-hole Setup
This is how I set up a Pi-Hole on my network to block unwanted ads. 
# Techology Used
## Devices: 
- Raspberry Pi 5
- Micro HDMI to HDMI Display Cable, 18Gbps High-Speed, 4K@60Hz, 2160p, 48-Bit Color, Ethernet Ready, 6 Foot
- Vilros 27W -5V/5A USB-C Power Supply Compatible with Raspberry Pi 5 & Apple Devices with USB-C Charging Port
## Other devices:
- OS: Raspberry Pi OS (Lite)
- DNS Provider: COX
- Network Setup: Router → Pi-hole → Client devices
- Operating System: Windows 11
# Acquire the necessary devices
1. Raspberry Pi 5 from https://www.raspberrypi.com/products/raspberry-pi-5/. It will look like this:

<img src="https://github.com/user-attachments/assets/b75244f7-b766-4ab0-8e2e-d43916a48b75" alt="Image" width="400" height="500">

2. Micro HDMI cable. Recommended: Micro HDMI to HDMI Display Cable, 18Gbps High-Speed, 4K@60Hz, 2160p, 48-Bit Color, Ethernet Ready, 6 Foot. 
Buy it at https://www.amazon.com/Amazon-Basics-Display-High-Speed-Ethernet/dp/B07KSDB25X/ref=sr_1_1?s=electronics&sr=1-1

3. Buy a Raspberry buy charger. Recommended: Vilros 27W -5V/5A USB-C Power Supply Compatible with Raspberry Pi 5 & Apple Devices with USB-C Charging Port. 
Buy it at https://www.amazon.com/Vilros-Raspberry-Compatible-USB-C-Supply/dp/B0CVJ7S3NF/ref=sr_1_1?s=electronics&sr=1-1

4. Samsung - Pro Plus 256GB microSDXC Memory Card
Buy it at https://www.bestbuy.com/product/samsung-pro-plus-256gb-microsdxc-memory-card/J3ZYG2PHHC

# Assemble Devices
1. Insert the SD card in the bottom of the Raspberry Pi.
(image placeholder)
2. Insert the micro HDMI cable and charger into the Raspberry Pi.
<img src="https://github.com/user-attachments/assets/c8c6a736-8e58-4391-b32e-e571a14c8c4e" alt="Raspberry Pi HDMI and charger" width="400" height="500">

  # Install Prerequisite programs
  1. Install Raspberry Pi imager from https://www.raspberrypi.com/software/.
  2. Configure the imager. Choose Device, OS, and Storage.
    
<img width="585" height="468" alt="raspberry pi image" src="https://github.com/user-attachments/assets/145ae700-8bef-4776-9274-80d80f81664c" />

3. Click "EDIT SETTINGS" when asked if you want to apply OS customisation settings.
4. Set hostname, username, wireless LAN, Locale Settings. 

<img width="677" height="592" alt="raspberry pi settings" src="https://github.com/user-attachments/assets/99a33ee3-4901-496e-95bd-d77194a7e677" />

5. Under Services, check Enable SSH and click "Use password Authentication."
<img width="677" height="485" alt="Image" src="https://github.com/user-attachments/assets/bfacebf9-00aa-4572-8f93-e6212f423f5d" />

  6. Install Real VNC Viewer. This will give you the ability to run Raspberry Pi on your computer. Download it here: https://www.realvnc.com/en/connect/download/viewer/?lai_vid=PXy6kmxlkhV5J&lai_sr=0-4&lai_sl=l

7. Once installed, search for raspberrypi.local in the search bar.

<img width="800" height="472" alt="real vnc viewer" src="https://github.com/user-attachments/assets/b56fd2bf-4e27-43f8-9726-b20525808e57" />



Open Raspberry Pi. It will look like this:


<img width="918" height="828" alt="Raspberry Pi Desktop" src="https://github.com/user-attachments/assets/5c3f7e32-85c1-4bb5-9d96-3e75fe820247" />

# Set Up Pi-Hole on Raspberry Pi
## Update Raspberry Pi
### Run these 2 commands:
<pre style="border:1px solid #ccc; padding:10px; border-radius:6px;">

sudo apt update && sudo apt full-upgrade -y
sudo apt install -y curl
  </pre>

  ## Confirm Raspberry Pi's address
  <pre style="border:1px solid #ccc; padding:10px; border-radius:6px;">

hostname -I
ip a
    </pre>
  ## Set Static IP Address for Pi
  Use this command if you need to find your Pi's address:
  <pre style="border:1px solid #ccc; padding:10px; border-radius:6px;">
sudo nano /etc/dhcpcd.conf
    </pre>

    
You can then enter the information. Example:
- interface eth0
- static ip_address=[enter info here]
- static routers=[enter info here]
- static domain_name_servers=[enter info here]
  
## Set the IP address of your computer to be the same as the IP address for your Pi. 
- Go to Control Panel\Network and Internet\Network and Sharing Center

<img width="893" height="642" alt="Network and Sharing Center" src="https://github.com/user-attachments/assets/7099884a-dc74-49aa-bb76-4399f42c0de8" />



- Click change adapter settings. Then right click Wi-Fi and click Properties.
  - Check Internet Protocol Version 4 (TCP/IPv4). Uncheck Internet Protocol Version 6 (TCP/IPv6).
 
  
<img width="453" height="580" alt="ipv4" src="https://github.com/user-attachments/assets/30e1c057-d88b-4718-b290-eabcc45a9e4b" />


  - Double click Internet Protocol Version 4 (TCP/IPv4). 
  - Click Use the following DNS server address and enter the address of your Pi for Preferred DNS server.

<img width="555" height="646" alt="Image" src="https://github.com/user-attachments/assets/806ba5cb-c3c1-43ee-96d7-a5e5e673e1d3" />

## Install Pi-Hole Using the Terminal
Use this command:

<pre style="border:1px solid #ccc; padding:10px; border-radius:6px;">
curl -sSL https://install.pi-hole.net
</pre>


This command starts the installation wizard.

- Confirm static IP
- Select upstream DNS provider

  # Use the Pi-Hole as an ad blocker.
  In your Raspberry Pi, open a browser and type the following in the address bar:
  
  http://[Your Pi IP address]/admin

  Log in using your username and password.

  
<img width="617" height="557" alt="Image" src="https://github.com/user-attachments/assets/373cab22-ccb3-4b79-8971-45f10824b44a" />
  
  ## Add domains to a blacklist
  This will put the Pi-Hole to work.

  Go to Lists and start adding URLs to the Address bar.

  
  <img width="1275" height="883" alt="pi hole list" src="https://github.com/user-attachments/assets/1af6970e-6e04-484f-a736-027f4e1292ec" />

  

  Search The Firebog https://firebog.net/ for a list of suspicious links you can add.

  ## Test the Pi's effectiveness

  We'll use the CNN website for our test.

  Here is the CNN homepage before the Pi-Hole is working:

  

  <img width="601" height="867" alt="cnn before pi hole" src="https://github.com/user-attachments/assets/b43d6f3f-bd11-4780-8ac5-6d5daaaa9a85" />

  

  Here is the CNN homepage after the Pi-Hole is working.

  

  <img width="1015" height="538" alt="cnn after pi hole" src="https://github.com/user-attachments/assets/968efab5-e522-4525-acca-8ab80d0bbc09" />

  

  Success!

  

