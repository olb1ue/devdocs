# Heltec CubeCell Board

![](../../.gitbook/assets/cubecell-board.png)

## Introduction

This guide will show you step by step how to transmit LoRaWAN packets using a longfi-arduino sketch on a [Heltec CubeCell Board](https://heltec.org/project/htcc-ab01/).

{% hint style="warning" %}
Before we begin, please make sure you've followed the steps from this [guide](https://developer.helium.com/console/quickstart), which goes over some initial steps to add your device to Console.
{% endhint %}

Our Helium community member @suprnrdy has a store set up in the US at [https://parleylabs.com/shop/](https://parleylabs.com/shop/) where you can find multiple variants of the CubeCell boards.

## Objective and Requirements

In this guide, you will learn:

* How to setup your environment
* How to program a basic application that will send packets over the Helium Network
* Verify real-time packets sent to the Helium Console via Hotspot that's in range

For this example, you will need the following:

### Hardware

*  [Heltec CubeCell Board](https://heltec.org/project/htcc-ab01/)
* Micro USB Type B Cable - [Example](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0719H12WD/ref=sr_1_2_sspa?)

### Software

* [Arduino software \(IDE\)](https://www.arduino.cc/en/Main/Software) 
* [Helium Console](https://console.helium.com/) 

## Hardware Setup <a id="hardware-setup"></a>

### Adding the Antenna <a id="adding-the-antenna"></a>

Your board should have come with a U.FL antenna. All you have to do is attache it to the U.FL port as shown in the image at the top of the guide.

### Connect Board <a id="connect-board"></a>

Next, lets connect our board to our computer with a USB 2.0 A-Male to Micro B cable.

## Software Setup <a id="software-setup"></a>

### Getting the Arduino IDE <a id="getting-the-arduino-ide"></a>

Download and install the latest version of [Arduino IDE](https://www.arduino.cc/en/Main/Software) for your preferred OS.

* ​[Windows](https://www.arduino.cc/en/Guide/Windows)​
* ​[Linux](https://www.arduino.cc/en/Guide/linux)​
* ​[Mac OSX](https://www.arduino.cc/en/Guide/MacOSX)​

### Arduino Board Support <a id="arduino-board-support"></a>

The Heltec CubeCell Board requires one Arduino board support package. Follow the instructions below to install.

#### CubeCell Dev-boards <a id="arduino-esp32"></a>

To install, open your Arduino IDE:

1. Navigate to **\(File &gt; Preferences\), \(Arduino &gt; Preferences\) on MacOS.**
2. Find the section at the bottom called **Additional Boards Manager URLs:**

![](../../.gitbook/assets/cubecell-board-support-json.png)

3.  Add this URL in the text box:

```text
http://resource.heltec.cn/download/package_CubeCell_index.json
```

4. Close the Preferences windows

Next, to install this board support package:

1. Navigate to \(**Tools &gt; Boards &gt; Boards Manager...\)**
2. Search for  **CubeCell Dev-boards**
3. Select the newest version and click Install

![](../../.gitbook/assets/cubecell-board-support-search.png)

### Install Serial Driver

Find Directions on Heltec's website [here](https://heltec-automation-docs.readthedocs.io/en/latest/general/establish_serial_connection.html).

### Select Board

Arduino IDE:

1. Select Tools -&gt; Board: -&gt;CubeCell-Board

### Select Region

Arduino IDE:

1. Select Tools -&gt; LoRaWAN Region: -&gt; REGION\_US915

### Select **Uplink Mode**

The last step before we upload our sketch is to select the LoRaWAN Uplink Mode, navigate to **\(Tools &gt; LoRaWAN Uplink Mode:  &gt; UNCONFIRMED\).**

### Programming **Example Sketch**

Now that we have the required Arduino board support and library installed, lets program the board with the provided example sketch.

To create a new Arduino sketch, open your Arduino IDE, \(**File &gt; New\).** Next, replace the template sketch with the sketch found [here](https://github.com/helium/longfi-arduino/blob/master/Heltec-CubeCell-Board/longfi-us915/longfi-us915.ino), copy and paste the entirety of it. 

Next we'll need to fill in the AppEUI\(msb\), DevEUI\(msb\), and AppKey\(msb\), in the sketch, which you can find on the device details page on Console. Be sure to use the formatting buttons to match the endianess  and formatting required for the sketch, shown below.

![](../../.gitbook/assets/cubecell-console-details.png)

At the top of the sketch, replace the three **FILL\_ME\_IN** fields, with the matching field from Console, example shown below.

![](../../.gitbook/assets/cubecell-console-keys.png)

### Upload Sketch

We're finally ready to upload our sketch to the board. In the Arduino IDE, click the right arrow button, or navigate to \(**Sketch &gt; Upload\),** to build and upload your new firmware to the board. You should see something similar to the image below at the bottom of your Arduino IDE, when the upload is successful.

![](../../.gitbook/assets/cubecell-arduino-upload.png)

### Viewing Serial Output <a id="viewing-serial-output"></a>

When your firmware update completes, the board will reset, and begin by joining the network. Let's use the Serial Monitor in the Arduino IDE to view the output from the board. We first need to select the serial port again, but this time it will be a **different port** than the one we selected to communicate with the bootloader. Once again, navigate to \(**Tools &gt; Port: COM\#/ttyACM\#**\), but make sure the serial device, either COM\# or ttyACM\#, is different! Next navigate to \(**Tools &gt; Serial Monitor**\), you should begin to see output similar to below.

![](../../.gitbook/assets/cubecell-arduino-serial.png)

Now let's head back to [Helium Console](https://console.helium.com/) and look at our device page, you should see something similar to the screenshot below.  


![](../../.gitbook/assets/heltec-wifi-lora-console-events.png)

Congratulations! You have just transmitted data on the Helium network! The next step is to learn how to use your device data to build applications, visit our Integrations docs [here](../../console/integrations/).

