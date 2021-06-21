# CSI_Data_Gathering
In this repository, we look at a variety of common solutions for CSI data gathering.
Channel State Information (CSI)
Channel State Information (CSI) is a property of a communication link that attracts a lot of attention in recent years. CSI data shows how the signal propagates from transmitter to receiver and based on the propagation patterns, researchers achieve lots of information about the propagation environment. For example, the human body is one of the objects in the environment that can reflect the received signal (propagation). So, based on the difference of propagated data, we can decide which activities or gestures the user had done. You can learn more about this property from its page in wikipedia.

# Data Gathering
As you probably know, for gathering this data we need at least two devices: one transmitter and one receiver. The transmitter is the device that sends the Wi-Fi signal and the receiver is the device that receives the sent signal (We can use transceivers instead of each of them. transceivers are devices that can transmit and receive at the same time). These devices could be commercial devices like laptops, personal computers, mobile phones, routers, and so on, or any chipsets with a Wi-Fi antenna.

# Tools
There are many tools developed for gathering CSI data using different hardware. You must know that each tool only works on some specific hardware not all of them. You can see some popular ones as follow:

1. Intel 5300: For using this tool you need to have the Intel 5300 NIC at least on one of your devices (transmitter or receiver). You can read more about this tool here. I didn't find a step-by-step installation guide for this tool.
2. Atheros: For using this tool, you should have an Atheros NIC on your device. They believe that it works on all Atheros NICs but only some of them are tested. You can find the details of this tool here. There is a step-by-step installation guide for this tool.
3. Wi-ESP: This tool was presented in 2020. For using this tool you don't need to have a specific network card on your laptop or PC but you only need to buy at least one ESP 32 chipset which is around $15. Although there is a paper, and a Github for this tool, I couldn't find a specific step-by-step installation guide for it. There is some code in their Github about udp_server, udp_client, and so on but there is no detailed guideline to show how it should be installed.
4. ESP32 CSI Toolkit: For using this toolkit like the previous one, you need at least one ESP32 chipset. This toolkit contains a detailed installation guide and is easy to use. You can find the details about this toolkit here.
You can see the summary of the explanation as follow:

* Intel 5300 a device with specific hardware, a step-by-step guideline X
* Atheros a device with specific hardware, a step-by-step guideline ✓
* Wi-ESP ESP32 microcontroller, a step-by-step guideline X
* ESP32 CSI Toolkit ESP32 microcontroller, a step-by-step guideline ✓

I installed 3 of them (except Intel 5300) and couldn't reach the result except in the last one. For using the ESP32 CSI toolkit you only need to follow the steps of this link. I only used their active_ap project to create an access point using ESP32. After I set the configuration in make menuconfig I build it on the ESP32 by make flash monitor. It creates an access point (AP) by my preset SSID and password. Then connected to the access point using another device (my mobile phone) and the results appear on the AP console. The AP will receive the CSI data dynamically until my device is connected to it. After you received this data you can save it into the file and do your analysis (Machine Learning or etc) on it. CSI Data

# ESP32 CSI Toolkit
The details of the implementation of this toolkit are available at this link. I did the following steps one-by-one and reach the CSI data:

1. Download and Install ESP: You can download the ESP zip file using this link. After downloading this file, I created a folder in C: drive, named esp, and another folder inside that named esp. then extract the zip file in this folder: C:\esp\esp

2. Install ESP-IDF v3.3.1: After installing ESP, you need to install ESP-IDF. For using this toolkit you need v3.3.1 of ESP-IDF. Detail instructions of this step are available at this link. You only need to open a cmd on windows and enter the following lines to clone the esp-idf from its git repository: cd ~/esp then git clone -b v3.3.1 --recursive https://github.com/espressif/esp-idf.git

3. Download ESP32 CSI Toolkit: Now, we should download the toolkit from this link. We need to extract this zip file into a folder. There is a tricky step here. You should not extract this file into a folder under C:\esp\esp. It can cause some errors in the next step. So, I extracted this zip file into the example folder of esp-idf in this path: C:\esp\esp-idf\examples.

4. Connect ESP32 Device: In this step, you only need to connect the ESP32 device to your computer and do some configuration. For this task, you need a micro USB to USB cable. Each USB port in your laptop has a name. After connecting the device to your laptop you can open Device Manager on Windows and find the name of your connected USB port. In my case this name is COM3. You need to run the mingw32.exe command line from the C:/esp/esp/msys32 folder. navigate to the C:\esp\esp-idf\examples\ESP32-CSI-Tool-master\active_ap and run make menuconfig. In the configuration menu, you need to set some configuration that was mentioned in this link.

5. Flash and Monitor: Finally, in the mingw32 command line, you only need to run make flash monitor in the active_ap project. After few minutes you can see the access point is running but not receiving any data. because there is no device connected to it as a station. Now, if you didn't change the SSID and Password in the ESP32 configuration your access point name would be "myssid". You can find a network by this name on all of your devices (laptops, smartphones, etc). You only need to connect one of those devices to this network. The password of this network was set in step 4. By doing this, you can see the CSI data on your access point console. You will receive new data almost after each second.
