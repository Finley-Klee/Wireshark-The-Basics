# Wireshark-The-Basics
This is a walkthrough of my work on the TryHackMe Room (https://tryhackme.com/r/room/wiresharkthebasics) 

<h2>Description</h2>
This project is designed to become familiar with navigating Wireshark including how to load packet capture files into Wireshark, where to find detailed information about the files, understanding the information provided in the packet details section and how it relates to the different layers of the OSI model, searching for packets either by the number assigned by Wireshark or by information found within the packets, and filtering and following packet exchanges.

<h2>Utilities Used</h2>

- <b>Wireshark</b> 
- <b>Linux Terminal</b>

<h2>Environments Used </h2>

- <b>Linux Ubuntu</b>

<h2>Project walk-through:</h2>

- <b>Tool Overview</b>
<p>This TryHackMe room includes two packet capture files already on the desktop: http1.pcapng and Exercise.pcapng.</p>
<p></p>The http1 packet capture file was used to create the screenshots found in the tutorial, and the questions can be answered by analyzing the Exercise packet capture file.</p>
<br>
<p align="center">I began by opening the Exercise.pcapng file in Wireshark: <br/>
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/d3af1e58-4a3d-4182-af2e-e7d0b75f6625" height="80%" width="80%" alt="The home page of Wireshark showing two file options with exercise.pcapng highlighted in blue"/>
  <br />
  <br />
  Then I opened the capture file properties to find the first flag in the file comment: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/fb33b95c-e818-496b-86d5-66cbf2e27d13" height="80%" width="80%" alt="The flag reading TryHackMe_Wireshark_Demo is highlighted in the file comment section of the capture file properties window"/>
  <br />
  <br />
  The next question asks for the total number of packets, which is found in the bottom of the Wireshark window: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/38f8b01e-ceb3-494c-8f90-3efc63d81972" height="80%" width="80%" alt="at the bottom of the main wireshark window a red rectangle surrounds the words packets: 58620 and above that a red arrow points to the box"/>
   <br />
  <br />
  Lastly for the tool overview task, I went back to the capture file properties to locate the SHA256 hash value of the packet capture file: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/633817ec-afd5-4017-add6-05ae4b86bbd5" height="80%" width="80%" alt="the Wireshark capture file properties window is shown with the hash value highlighted in light blue"/>
</p>
<br />
<br />
- <b>Packet Dissection</b>
<p>In the next task I drilled down into the individual packets.</p>
<br>
<p align="center">I opened packet 38 and found that eXtensible markup language was used: <br/>
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/7027a0cf-c6e0-447b-b4b8-aa5a46791ff5" height="80%" width="80%" alt="The packet detail view in wireshark of the 38th packet in the capture. In the bottom left details pane eXtensible markup language is selected in blue"/>
  <br />
  <br />
  In the frame details, which correspond to the physical layer (OSI layer 1), I found that the packet arrived on May 13th, 2004: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/b05740cd-d86e-4126-abba-f682c6642f09" height="80%" width="80%" alt="under the dropdown for frame 38 the arrival time line is highlighted in blue"/>
  <br />
  <br />
  Next, in the internet protocol layer (OSI layer 3) I found the time to live value: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/7c637571-8191-4ba0-927d-005fdc4b3a1b" height="80%" width="80%" alt="under the internet protocol dropdown the time to live value of 47 is highlighted in blue"/>
   <br />
  <br />
  Then I found the TCP payload size at the bottom of the transmission protocol section (OSI layer 4): <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/312d0a0b-6b5f-4b00-ad33-9bf1efded284" height="80%" width="80%" alt="under the transmission control protocol dropdown the tcp payload 424 bytes is highlighted in blue"/>
   <br />
  <br />
  Finally, I found the e-tag value for the packet under the application protocol section (OSI layer 5): <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/a42ea6fe-aa5e-4d15-aaa7-cd5e7b71cbbb" height="80%" width="80%" alt="under the hypertext transfer protocol dropdown the etag is highlighted in blue"/>
</p>
<br />
<br />
- <b>Packet Navigation</b>
<p>In this task I used the search bars to find packets containing specific strings and also exported an image and a text file to further analyze.</p>
<br>
<p align="center">I searched for the string "r4w" in the packet details of the capture file and found that the name of artist 1 is r4w8173: <br/>
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/549709d4-7736-4765-a575-4591509085a8" height="80%" width="80%" alt="the search bar is surrounded by a red rectangle with a speech bubble reading string entered into the search and below the artist name is also within a red rectangle with a red arrow and the words artist 1s name in the html between the h3 tag opening and closing"/>
  <br />
  <br />
  The next question sends us on a bit of a hunt. First, we use the "go to packet" function to find the comment on packet 12: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/3bd18f9e-6671-41c9-b32f-7397f3c48ef4" height="80%" width="80%" alt="A red rectangle surrounds the comment which reads go to packet number 39765, look at the packet details pane. Right-click on the JPEG section and Export packet bytes. This is an alternative way of extracting data from a capture file. What is the MD5 hash value of extracted image?"
/>
  <br />
  <br />
  The comment directed me to find the jpeg section of packet 39765, export those packet bytes, and then calculate the MD5 hash value of the extracted image: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/ae32a325-95d8-4556-acca-af25f9742297" height="80%" width="80%" alt="the desktop of ubuntu linux with terminal open. On the desktop is seen a file named wireshark_image with a comment reading exported jpeg image from wireshark. On the terminal are commands navigating to the desktop and running md5sum on the wireshark_image file. The output is highlighted with a comment that reads hash value calculated using md5sum"/>
   <br />
  <br />
  Next, I used the export objects feature to find the text file that was sent over the wire, exported it to the desktop, and opened it to discover that the Alien's name is PACKETMASTER: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/34955e8a-7c22-4142-8f7e-66a623ec7d21" height="80%" width="80%" alt="the export http object list window is shown with the string .txt in the search bar resulting in on item"/>
   <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/7d643468-7003-4db9-b184-f4909a57ad88" height="80%" width="80%" alt="a text file with a graphic of an alien made out of dots and slashes with large bold lettering reading PACKETMASTER"/>
   <br />
  <br />
  For the final question in this section I opened the expert information window by clicking on the red circle in the bottom left corner. I found that there were 1636 warnings, marked in yellow in the list: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/43530ea4-dbfd-4163-8dc4-054e8b98c145" height="80%" width="80%" alt="the expert information window is shown and the yellow highlighted line called warning at the middle has a red oval around the number 1636 at the right hand side"/>
</p>
<br />
<br />
- <b>Packet Filtering</b>
<p>For this last task I worked on filtering through the packet capture file by selecting protocol type and following the packets in a conversation.</p>
<br>
<p align="center">I started by applying the filter http by right clicking on the hypertext transfer protocol in packet 4 and choosing apply filter. This resulted in 1089 packets being shown out of the total 58620 in the capture file.: <br/>
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/0ab138f7-5b03-4537-94ab-80b071668bea" height="80%" width="80%" alt="the wireshark window with a green bar at the top reading http and a red arrow pointing to that with the words filter query in red. At the bottom a red rectangle surrounds the words displayed: 1089 and a red arrow points to this section."/>
  <br />
  <br />
  To answer the last two questions I used the follow stream feature to inspect the http traffic starting with packet 33790. In this conversation I searched for the nubmer of artists by using find, and discovered that there are 3 artists, and the name of the second artist is Blad3: <br />
  <img src="https://github.com/Finley-Klee/Wireshark-The-Basics/assets/171582741/c6bd2a0c-2d58-4fce-a683-b05b0a44ca50" height="80%" width="80%" alt="in the follow http stream window can be seen html text and artist=1, artist=2, and artist=3 are underlined in red. There is a red rectangle around the text Blad3 which is the name of artist 2"/>
</p>

