---
name: Grove - 8-Channel Solid State Relay
category: Sensor
bzurl: 
oldwikiname: 
prodimagename:
surveyurl: 
sku: 103020136
tags:
---

![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/main.jpg)

固态继电器不使用线圈，而是使用功率半导体器件，如晶闸管和晶体管，其开关速度相较于机械式继电器快得多。**Grove - 8通道固态继电器** 基于高品质的 **G3MC-202P** 模块所设计，可以使用5VDC控制最大240VAV。在Grove接口的帮助下,与Arduino一起使用固态继电器将变的十分简便。 



我们使用板载[STM32F030F4P6](https://github.com/SeeedDocument/Grove-4-Channel_SPDT_Relay/raw/master/res/STM32F030F4P6.pdf)分别控制各个通道。从Arduino或者其他的板子指令通过IIC接口传输，板载 STM32F030F4P6 将会解析指令，因此您可以根据需要控制开关。


根据不同的使用场景，我们为您提供了一系列的固态继电器。


[Grove - 固态继电器 V2](http://wiki.seeedstudio.com/Grove-Solid_State_Relay_V2)

[Grove - 2通道固态继电器](http://wiki.seeedstudio.com/Grove-2-Channel_Solid_State_Relay)

[Grove - 4通道固态继电器](http://wiki.seeedstudio.com/Grove-4-Channel_Solid_State_Relay)

[Grove - 8通道固态继电器](http://wiki.seeedstudio.com/Grove-8-Channel_Solid_State_Relay)



<p style="text-align:center"><a href="https://www.seeedstudio.com/Grove-8-Channel-Solid-State-Relay-p-3131.html
" target="_blank"><img src="https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/300px-Get_One_Now_Banner-ragular.png" /></a></p>


## 产品特点

+ 低功耗
+ 持久耐用
+ IIC地址可选

- 相对于机械式继电器的优点：

    - 相较于机电继电器，固态继电器具有更快的开关速度，并且没有物理接触磨损
    - 全静音操作
    - 没有物理接触意味着没有火花，在开关过程中没有火花产生使得其可以被应用于易爆环境中
    - 使用寿命增加
    - 整体结构紧凑


- 缺点：

    - 当关闭时，阻抗较高（发热），电噪声较大
    - 当打开时，阻抗较低，存在漏电流
    - 只能使用在AC电路中

## 产品规格

|**项目**|**参数**|
|:----:|:----:|
|工作输入电压|4~6V|
|额定输入电压|5V|
|额定负载电压|100 ~  240 VAC 50/60 Hz|
|负载电压范围|75 ~  264 VAC 50/60 Hz||
|负载电流|0.1 ~  2 A |
|漏电流|1.5 mA max. (at 200 VAC)|
|绝缘电阻|1,000 MΩ min. (at 500 VDC)|
|操作时间|最大为 负载电源周期的1/2 + 1ms|
|释放时间|最大为 负载电源周期的1/2 + 1ms|
|存储温度|-30°C ~ 100°C (无结冰、结露)|
|工作温度|-30°C ~  80°C (无结冰、结露)|
|工作湿度| 45% ~  85%RH|
|输入接口|IIC|
|默认 IIC地址|0x11 或者 0x12|
|输出接口|2引脚直插式蓝色端子x8 |
|Zero Cross（过零控制）|支持|
|认证|UL / CSA|


!!!**注意**

您也许注意到了 **漏电流** , 1.5mA 足以驱动一个低功耗的LED，所以当继电器处于关闭状态时，LED也许仍然会发出微弱的光。



## 产品应用

- 需要低延迟切换的操作，例如， 舞台灯光控制
- 要求高稳定性的设备，例如 医疗设备，交通信号
- 防爆，防腐，防潮的情况，例如： 煤炭，化学工业


## 硬件概述

### 引脚映射


![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/pin_map.jpg)

![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/pin_map_back.jpg)


!!!**注**

- 开关1-8具有相同的引脚功能，因此对于其他开关，您可以参考 **LOAD1** / **LOAD2**。
- 在PCB的背面，有两个接口：SWD和IIC。在编程烧写固件时，默认使用SWD接口。如果要使用IIC接口（实际用作引导UART），则应将 **BOOT** 置高。



### 原理图

**继电器控制**



![](https://github.com/SeeedDocument/Grove-Solid_State_Relay_V2/raw/master/img/schematic_.jpg)

**K1** 是继电器模块，当在 **INT+** 和 **INT-** 之间施加5V时，继电器将打开。然后 **LOAD1**将会连接到 **LOAD2**。我们使用一个NPN型三极管 **Q1**(BC817-40)来控制 **INT+** 和 **INT-** 之间的电压。


 **CTR** 是来自Arduino或者其他板子的控制信号。它通过一个10K电阻R2被拉低，如果没有信号，**Q1**的基极为0V，Q1处于关闭状态，那么K1将被关断。如果 **CTR** 为 5V, Q1将会开启。K1的 **INT-** 将会被连接到系统的GND， **INT+** 和 **INT-** 之间会产生5V压降，因此K1将被打开，**LOAD1** 与 **LOAD2**连接。



**双向电平转换电路**

![](https://github.com/SeeedDocument/Grove-4-Channel_SPDT_Relay/raw/master/img/schematic_1.jpg)

这一个连接在IIC总线差分电压部分的典型双向电平转换电路。传感器的IIC总线使用3.3V，而Arduino的IIC总线使用的是5V，因此这个电路是必须的。如上面的原理图所示，**Q17** 和 **Q18** 是作为双向开关的N沟道场效应管[2N7002A](https://github.com/SeeedDocument/Grove-I2C_High_Accuracy_Temperature_Sensor-MCP9808/raw/master/res/2N7002A_datasheet.pdf)。为了更好地理解这一部分，您可以参考[AN10441](https://github.com/SeeedDocument/Grove-I2C_High_Accuracy_Temperature_Sensor-MCP9808/raw/master/res/AN10441.pdf)

!!!**提示**

在这一部分我们仅仅展示了部分原理图，完整的原理图文件请您参考 [资源下载](/#resources)

## 兼容平台


| Arduino                                                                                             | Raspberry Pi                                                                                             | BeagleBone                                                                                      | Wio                                                                                               | LinkIt ONE                                                                                         |
|:-:|:-:|:-:|:-:|:-:|
| ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/arduino_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/raspberry_pi_logo_n.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/bbg_logo_n.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/wio_logo_n.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/linkit_logo_n.jpg)  |

!!!**注意**

以上所提到的兼容平台指的是硬件模块在理论上可以兼容。然而在大多数情况下，我们仅仅为Arduino平台提供软件库或者代码示例。无法为所有的MCU平台提供提供库/代码示例。因此，用户在使用其他平台时需要自己编写软件库。




## 入门指导


### 使用Arduino

#### 硬件连接

**材料需求**

| Seeeduino V4.2 | Base Shield| Grove - 8通道固态继电器|
|:-:|:-:|:-:|
|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_1.jpg)|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_4.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/thumbnail.jpg)|
|<a href="http://www.seeedstudio.com/Seeeduino-V4.2-p-2517.html" target="_blank">点击购买</a>|<a href="https://www.seeedstudio.com/Base-Shield-V2-p-1378.html" target="_blank">点击购买</a>|<a href="https://www.seeedstudio.com/Grove-8-Channel-Solid-State-Relay-p-3131.html" target="_blank">点击购买</a>| 



!!!**注**

  **1** 请轻轻地插入USB线缆，否则可能会损坏端口。请使用内部有4根线的USB线缆，2根线的无法传输数据。如果你无法确认你的线缆类型，请点击[这里](https://www.seeedstudio.com/Micro-USB-Cable-48cm-p-1475.html)进行选购。
    
  **2**  购买时，每个Grove模块都配有Grove线缆。如果您不慎丢失了Grove线缆，可以点击[这里](https://www.seeedstudio.com/Grove-Universal-4-Pin-Buckled-20cm-Cable-%285-PCs-pack%29-p-936.html)选购。




- **步骤 1.** 将 Grove - 8通道固态继电器 连接到Base Shield的 **I^2^C** 端口。

- **步骤 2.** 将Base Shield插到Seeeduino上。

- **步骤 3.** 通过USB线缆将Seeeduino连接到PC端。



![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/connect.jpg)


!!!**注**

如果没有Grove Base Shield，我们可以直接按照下面引脚定义将模块连接到Seeeduino上。

| Seeeduino     |  Grove - 8通道固态继电器|
|:-:|:-:
| 5V            | 红 |
| GND           | 黑 |
| SDA           | 白  |
| SCL           | 黄  |






#### 软件代码


如果这是您第一次使用Arduino，我们强烈建议您先看一下[Arduino 入门指导](http://wiki.seeedstudio.com/Getting_Started_with_Arduino/).


- **步骤 1.** 从Github上下载[多通道继电器Arduino库](https://github.com/Seeed-Studio/Multi_Channel_Relay_Arduino_Library) 。

- **步骤 2.** 请参考如何为Arduino安装库[如何安装库文件](http://wiki.seeedstudio.com/How_to_install_Arduino_Library)。

- **步骤 3.** 重启Arduino IDE。通过路径：**File --> Examples --> Multi Channel Relay Arduino Library --> eight_channel_relay_control**打开示例程序。


![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/path.jpg)


或者，您可以点击这个位于代码块右上方的图标![](https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/copy.jpg)将以下代码拷贝进Arduino IDE。
```c++
#include <multi_channel_relay.h>

#define USE_8_CHANNELS (1)

Multi_Channel_Relay relay;

void setup()
{
  Serial.begin(9600);
  while(!Serial);   

   /* Scan I2C device detect device address */
  uint8_t old_address = relay.scanI2CDevice();
  if((0x00 == old_address) || (0xff == old_address)) {
    while(1);
  }

  Serial.println("Start write address");
  relay.changeI2CAddress(old_address, 0x11);  /* Set I2C address and save to Flash */  
  Serial.println("End write address");

  /* Read firmware  version */
  Serial.print("firmware version: ");
  Serial.print("0x");
  Serial.print(relay.getFirmwareVersion(), HEX);
  Serial.println();
}

void loop()
{

  /** 
   *  channle: 8 7 6 5 4 3 2 1
   *  state: 0b00000000 -> 0x00  (all off)
   *  state: 0b11111111 -> 0xff  (all on)
  */  

  /* Begin Controlling Relay */ 
  Serial.println("Channel 1 on");
  relay.turn_on_channel(1);  
  delay(500);
  Serial.println("Channel 2 on");
  relay.turn_off_channel(1);
  relay.turn_on_channel(2);
  delay(500);
  Serial.println("Channel 3 on");
  relay.turn_off_channel(2);
  relay.turn_on_channel(3);  
  delay(500);
  Serial.println("Channel 4 on");
  relay.turn_off_channel(3);
  relay.turn_on_channel(4);  
  delay(500);
#if(1==USE_8_CHANNELS)  
  Serial.println("Channel 5 on");
  relay.turn_off_channel(4);
  relay.turn_on_channel(5);  
  delay(500);
  Serial.println("Channel 6 on");
  relay.turn_off_channel(5);
  relay.turn_on_channel(6);  
  delay(500);
  Serial.println("Channel 7 on");
  relay.turn_off_channel(6);
  relay.turn_on_channel(7);  
  delay(500);
  Serial.println("Channel 8 on");
  relay.turn_off_channel(7);
  relay.turn_on_channel(8);  
  delay(500);
  relay.turn_off_channel(8);
#endif

  relay.channelCtrl(CHANNLE1_BIT | 
                    CHANNLE2_BIT | 
                    CHANNLE3_BIT | 
                    CHANNLE4_BIT | 
                    CHANNLE5_BIT | 
                    CHANNLE6_BIT |
                    CHANNLE7_BIT |
                    CHANNLE8_BIT);
  Serial.print("Turn all channels on, State: ");
  Serial.println(relay.getChannelState(), BIN);
  
  delay(2000);

  relay.channelCtrl(CHANNLE1_BIT |                   
                    CHANNLE3_BIT | 
                    CHANNLE5_BIT | 
                    CHANNLE7_BIT);
  Serial.print("Turn 1 3 5 7 channels on, State: ");
  Serial.println(relay.getChannelState(), BIN);

  delay(2000);

  relay.channelCtrl(CHANNLE2_BIT | 
                    CHANNLE4_BIT | 
                    CHANNLE6_BIT |
                    CHANNLE8_BIT);
  Serial.print("Turn 2 4 6 8 channels on, State: ");
  Serial.println(relay.getChannelState(), BIN);
  
  delay(2000);


  relay.channelCtrl(0);
  Serial.print("Turn off all channels, State: ");
  Serial.println(relay.getChannelState(), BIN);
  
  delay(2000);
}
```

- **步骤 4.** 上传代码。如果您不知道如何上传代码，请点击[如何上传代码](http://wiki.seeedstudio.com/Upload_Code/)。
- **步骤 5.** 通过点击 **Tool-> Serial Monitor** 打开Arduino IDE的 **Serial Monitor** 。或者同时按下 **ctrl+shift+m**。如果一切运行正常，您将会看到以下运行结果。

!!!**成功**

如果一切运行正常，您将会看到以下运行结果。同时，您也会看到板载LED灯交替闪烁。

```c++
Scanning...
I2C device found at address 0x11 !
Found 1 I2C devices
Start write address
End write address
firmware version: 0x1
Channel 1 on
Channel 2 on
Channel 3 on
Channel 4 on
Channel 5 on
Channel 6 on
Channel 7 on
Channel 8 on
Turn all channels on, State: 11111111
Turn 1 3 5 7 channels on, State: 1010101
Turn 2 4 6 8 channels on, State: 10101010
Turn off all channels, State: 0
Channel 1 on
Channel 2 on

```


![](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/img/gif.gif)



!!!**注**

在这个例程里我们没有添加负载，如果您想要知道如何添加负载请参考[Grove - 2通道固态继电器](http://wiki.seeedstudio.com/Grove-2-Channel_Solid_State_Relay).


#### 功能说明


<table style="undefined;table-layout: fixed; width: 749px">
<colgroup>
<col style="width: 233px">
<col style="width: 516px">
</colgroup>
  <tr>
    <th>功能</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><span style="font-weight:bold">changeI2CAddress(uint8_t old_addr, uint8_t new_addr)</span></td>
    <td>改变设备地址， <span style="font-weight:bold">old_addr </span>是当前地址；<span style="font-weight:bold">new_addr </span>是您想要使用的新地址。只有当输入正确的旧地址，新地址才能够被成功设置。</td>
  </tr>
  <tr>
    <td><span style="font-weight:600">scanI2CDevice()</span></td>
    <td>获得 <span style="font-weight:700">old_addr </span>(当前地址)</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">getChannelState()</span></td>
    <td>获得每个通道的状态，例如"State: 1111", 表示所有继电器都是开通状态</td>
  </tr>
  <tr>
    <td><span style="font-weight:600">getFirmwareVersion()</span></td>
    <td>获得板载MCU的固件版本</td>
  </tr>
  <tr>
    <td><span style="font-weight:600">channelCtrl(uint8_t state)</span></td>
    <td>立即更改您所选择的通道状态，<span style="font-weight:600">状态参数列表：</span><br> <br>  <span style="font-weight:bold">CHANNLE1_BIT  </span>或者  <span style="font-weight:bold">0x01</span><br>  <span style="font-weight:bold">CHANNLE2_BIT</span>  或者  <span style="font-weight:bold">0x02</span><br>  <span style="font-weight:bold">CHANNLE3_BIT</span>  或者  <span style="font-weight:bold">0x04</span><br>  <span style="font-weight:bold">CHANNLE4_BIT</span>  或者  <span style="font-weight:bold">0x08</span><br><br>例如： <br><span style="font-weight:600">        channelCtrl(CHANNLE2_BIT|CHANNLE3_BIT),</span>将会打开通道2和通道3<br><span style="font-weight:600">        channelCtrl(01|02|08), </span>将会打开通道1、通道2和通道4<br><span style="font-weight:600">        channelCtrl(0), </span>将会关闭所有通道.</td>
  </tr>
  <tr>
    <td><span style="font-weight:600">turn_on_channel(uint8_t channel)</span></td>
    <td>打开单个通道<br>例如：<br>        <span style="font-weight:600">turn_on_channel(3), </span>将会打开通道3</td>
  </tr>
  <tr>
    <td><span style="font-weight:600">turn_off_channel(uint8_t channel)</span></td>
    <td>关闭单个通道<br>例如：<br><span style="font-weight:600">       turn_off_channel(3), </span>将会关闭通道3</td>
  </tr>
</table>

如果您想更改地址，则需要在使用前设置地址。 例如，我们想将其更改为0x2f。 我们可以使用以下代码。

```C++
#include <multi_channel_relay.h>

Multi_Channel_Relay relay;

void setup()
{
  Serial.begin(9600);
  while(!Serial);   

   /* Scan I2C device detect device address */
  uint8_t old_address = relay. ;
  if((0x00 == old_address) || (0xff == old_address)) { 
    while(1);
  }

  Serial.println("Start write address");
  relay.changeI2CAddress(old_address,0x2f);  /* Set I2C address as 0x2f and save it to the EEPRom */  
  Serial.println("End write address");

  /* Read firmware  version */
  Serial.print("firmware version: ");
  Serial.print("0x");
  Serial.print(relay.getFirmwareVersion(), HEX);
  Serial.println();
}


```

## FAQ

**Q1: 如何烧写固件？**

**A1:** 我们建议您使用J-LINK下载器通过SWD接口烧写固件。

您可以点击下载[出厂固件](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/res/Grove-8-Channel-Solid-Relay-Firmware.bin)

我们建议您使用
[J-flash](https://www.segger.com/downloads/jlink#J-LinkSoftwareAndDocumentationPack)软件。


![](https://github.com/SeeedDocument/Grove-4-Channel_SPDT_Relay/raw/master/img/J-flash.jpg)


## 原理图在线预览


<div class="altium-ecad-viewer" data-project-src="https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/res/Grove%20-%208-Channel%20Solid%20State%20Relay.zip" style="border-radius: 0px 0px 4px 4px; height: 500px; border-style: solid; border-width: 1px; border-color: rgb(241, 241, 241); overflow: hidden; max-width: 1280px; max-height: 700px; box-sizing: border-box;" />
</div>


## 资源下载

- **[Zip]** [Grove-8通道固态继电器eagle文件](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/res/Grove%20-%208-Channel%20Solid%20State%20Relay.zip)
- **[Zip]** [多通道继电器Arduino库](https://github.com/Seeed-Studio/Multi_Channel_Relay_Arduino_Library/archive/master.zip)
- **[Bin]** [出厂固件](https://github.com/SeeedDocument/Grove-8-Channel_Solid_State_Relay/raw/master/res/Grove-8-Channel-Solid-Relay-Firmware.bin)
- **[PDF]** [G3MC-202P数据手册](https://github.com/SeeedDocument/Grove-Solid_State_Relay_V2/raw/master/res/G3MC202p.pdf)
- **[PDF]** [STM32数据手册](https://github.com/SeeedDocument/Grove-4-Channel_SPDT_Relay/raw/master/res/STM32F030F4P6.pdf)


## 技术支持
请您不要犹豫，来我们的[论坛](https://forum.seeedstudio.com/)提出问题吧！

