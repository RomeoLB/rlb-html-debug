# rlb-html-debug

This repo allows the user to setup their Brightsign player to debug a HTML application. 

The below workflow was tested on a Mac system so it may need to be adjusted slightly for a Windows based system.

## Pre requistes:

1. Update player OS 
    - Series 5 players install OS 9.0.145.1+
    - Series 4 players install OS 8.5.47+

2. Install vscode (https://code.visualstudio.com/download)      

3. Install nvm (https://github.com/nvm-sh/nvm) then install node version v14.17.6

## Let's start

1. Download and clone the rlb-html-debug repo
```bash
git clone https://github.com/RomeoLB/rlb-html-debug.git
```
2. Change directory inside the rlb-html-debug folder
```bash
cd rlb-html-debug
```
3. Copy the content of the "copy-to-brightsign-player-storage" folder to a blank SD card and insert that into the Brightsign player then Power ON the Brightsign player

4. Wait for the player to playback the the video file and display its IP address on screen

5. Once you see the IP address of the player displayed on screen, Open a telnet session - assuming that my test player IP address is 192.168.1.34 and that I have telnet installed on my system, I would enter the below:
   <img width="888" alt="image" src="https://github.com/user-attachments/assets/574c8e0e-1ead-4064-a3dd-64d0560fc57f">

```bash
telnet 192.168.1.34 23
``` 
6. In the player telnet output look for a line that contains "nvm use v14.17.6 &&" and copy the entire line all the way to the player IP address, as per the below example:

   <img width="911" alt="image" src="https://github.com/user-attachments/assets/e4d6103b-d332-456b-9362-045fa66b201f">

```bash
nvm use v14.17.6 && npm install && export HOST=192.168.1.34 && export DEVICE_NAME=XT1145-0018 && export INDEXFILE=./copy-to-brightsign-player-storage/index-autoplay.html && export AUTORUNFILE=./copy-to-brightsign-player-storage/autorun.brs && export FOLDER=./copy-to-brightsign-player-storage/ && bsc addplayer XT1145-0018 192.168.1.34
```
7. Paste this line as is, in the VS code terminal. This dynamically generated string contains the relevant parameters to set up the project environment variables and configures the bsc CLI tool for files and folder uploads to the player using the REST API. If all goes well, you should see a message confirming that "Player added successfully" in the VS code terminal after hiting the "Return" key.

## File(s) / Folder upload and autorun restart

You are now ready to upload some files to the player and restart the Brightsign application using simple npm scripts!

To upload both the autorun.brs and the index-autoplay.html and then restart the Brightsign application, you can do so by entering in the VS Code terminal 

```bash
npm run upload-scripts-restart
```

To upload the entire foder then restart the autorun use:

```bash
npm run upload-folder-all-restart
```




