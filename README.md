# tuyaDAEMON - An IoT Framework Empowering Project Development

[tuyaDAEMON is an IoT framework](https://github.com/msillano/tuyaDAEMON) that provides users with a comprehensive set of resources to leverage in their projects. While each project is unique, tuyaDAEMON offers reusable solutions that facilitate the development process. 

### Enhanced IoT Project Development
tuyaDAEMON serves as a powerful toolset for creating IoT projects, offering a wide range of features and resources. Whether you are developing a smart home system, industrial automation solution, or a wearable device, tuyaDAEMON provides a solid foundation to build upon. Its open and extensible nature allows developers to integrate various devices, sensors, and protocols seamlessly, ensuring compatibility and interoperability.

### Key Features and Capabilities

1. Device Management: tuyaDAEMON simplifies device management by providing a unified interface for controlling and monitoring connected devices. This includes device registration, authentication, and status monitoring, enabling efficient management of a diverse range of IoT devices.

1. Data Collection and Analysis: With tuyaDAEMON, collecting data from connected devices becomes effortless. The framework offers powerful data collection mechanisms, enabling users to gather valuable insights for decision-making, optimization, and predictive maintenance.

1. Interoperability: tuyaDAEMON supports a wide range of communication protocols, ensuring interoperability with different devices and platforms. This allows seamless integration of devices from various manufacturers, making it easier to create interconnected IoT systems.


1. Scalability and Flexibility: tuyaDAEMON is designed to support projects of all scales, from small prototypes to large-scale deployments. Its flexible architecture allows users to expand and customize their solutions as per their specific requirements, accommodating future growth and innovation.

1. Reuse of Solutions: While every IoT project is unique, there are often common challenges and requirements across different use cases. tuyaDAEMON acknowledges this and offers reusable solutions that can be leveraged to accelerate development. These solutions encompass pre-built modules, libraries, and code snippets that address common functionalities, such as data management, data visualization, user interfaces, and tasks management. By reusing these solutions, developers can save time, reduce development costs, and focus on adding value to their projects.

### Conclusion:
tuyaDAEMON empowers IoT project development by providing a comprehensive framework with versatile features and resources. Its capabilities span device management, data collection, interoperability, security, and scalability. Furthermore, tuyaDAEMON promotes the reuse of solutions, enabling developers to leverage pre-built modules and libraries to expedite development while maintaining flexibility. With tuyaDAEMON, IoT enthusiasts and professionals can create innovative and robust solutions, unlocking the full potential of the Internet of Things.

----------------------------
### tuyaDEAMON model for applications
<table border=0>
<tr>
<td>
<img src='https://github.com/msillano/tuyaDAEMON/blob/main/pics/daemon_0B.png?raw=true' width="850px"   />
<BR CLEAR=”left” /></td><td>
When designing applications, the TuyaDEAMON model simplifies as in the figure (in green the data, in black the commands). This doesn't mean that when developing an application one shouldn't sometimes intervene at a low level, to adapt some properties. Still, the application project is logically 'above' this simplified model of TuyaDAEMON.

The two most essential interfaces for applications are highlighted: REST and database.

The [REST](https://github.com/msillano/tuyaDAEMON/wiki/tuyaDAEMON-REST) interface allows us to send any command (SET) and to send requests to know the last value of each property (GET). The format is straightforward and above all the same for all devices: `device[, property[, value]]`.
</td></tr></table>

- The device's know-how is crystallized in [documentation datasheets](https://github.com/msillano/tuyaDAEMON/tree/main/devices),  which are generated by [tuyadaemon.toolkit](https://github.com/msillano/tuyaDAEMON/wiki/tuyaDAEMON-toolkit), with information on `DPs` (device's attributes or methods), valid values, any quirks.<br>
Some activities are handled by TuyaDAEMON with the _Tuya-cloud_ collaboration: in this case, the two-way communication takes place via [TuyaTRIGGER](https://github.com/msillano/tuyaDAEMON/tree/main/tuyaTRIGGER), but in a completely transparent way for the user, and the documentation is always in the datasheets of the devices, [e.g. Smoke_Detector](https://github.com/msillano/tuyaDAEMON/blob/main/devices/Smoke_Detector/device_Smoke_Detector.pdf).

- Of the [DataBase](https://github.com/msillano/tuyaDAEMON/tree/main#database-interface), only one table affects the applications and contains the historical log (commands and events) of TuyaDAEMON: `tuyathome.messages`. The record comprises complete information: 

`   id |           timestamp |  daemon |action|    device-id |device-name|dps| dp-name|             data | value`<br>
example:<br>
`45276 | 2023-05-28 07:33:32 | MACTEST | RX | 1234569b99a78mkj6 | mainAC | 6 | phaseA | CYgAAlgAADMACw== | {"V":244,"Leack":0.002,"A":0.67584,"W":51}`.

-----------------
## Programmer's notes 
>  1. purging db `tuyathome.messages`   

