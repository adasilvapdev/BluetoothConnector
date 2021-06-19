# :small_blue_diamond: Bluetooth Connector :iphone: :small_blue_diamond:
**Bluetooh Connector - React Native App**
____________________________________________________________________________________________________________________________________________

***📳 Bluetooth Low Energy: Main Concepts and Difference from Classic Bluetooth***

Bluetooth is a short-range wireless networking protocol to quickly connect devices. Currently, it has 2 versions: Bluetooth Classic and Bluetooth Low Energy.

- Bluetooth Classic is often referred to as just Bluetooth. This technology can support continuous connections and transfer big amounts of data. This may include phone calls, audio streaming, data.

- Bluetooth Low Energy is also known as BLE. This is a version of Bluetooth that is adapted to low power sensors and accessories. Such devices don’t require continuous connection but depend on long battery life. They are especially popular in fitness, healthcare, security, home entertainment industries, and beacons.
____________________________________________________________________________________________________________________________________________
***Key concepts for BLE 📖***
- GATT stands for Generic Attribute Profile that defines how BLE-devices transfer data. To make data transfer possible, devices should have a dedicated connection.

_BLE-devices are often referred to as peripheral devices, while smartphones, tablets, and other similar gadgets — as central devices. 
Every peripheral device can have an exclusive connection with one central device at a time, while the central device can be simultaneously connected to multiple peripherals:_

![image](https://user-images.githubusercontent.com/20091777/122648996-bcecc600-d0f9-11eb-8818-6a725adf99c5.png)

_Connection between a central and peripheral devices (image by [Kevin Townsend](https://learn.adafruit.com/users/ktownsend))_.

____________________________________________________________________________________________________________________________________________
Since we’re talking about GATT, let’s take a bit closer look at the server/client relationship:
- From that perspective, a peripheral device is known as the GATT Server that contains data.
- A central device acts as the GATT Client that sends requests to this server.

**Peripheral -> GATT Server**

**Central Device -> GATT Client**
____________________________________________________________________________________________________________________________________________
The Client initiates all the transactions by asking the Server for data. 

**There are 2 ways to transfer data from the Server to the Client: Notifications and Indications.**

- Notification is a one-way message. It goes faster since it doesn’t ask the Client whether it has received the message or not.

- Indication describes a system of two-way communication. 
The Server sends a message ➡️ the Client receives the message and sends a confirmation message back to the Server ➡️ the Server knows that the initial message has reached the Client.
____________________________________________________________________________________________________________________________________________
**Data transfer itself is based on a few high-level objects: Profiles, Services, and Characteristics.**

![image](https://user-images.githubusercontent.com/20091777/122649427-cecf6880-d0fb-11eb-9a70-ab6e8b2998aa.png)

_The hierarchy of Profiles, Services and Characteristics (image by [Kevin Townsend](https://learn.adafruit.com/users/ktownsend))._

- Profile is a predefined set of Services.
- Services break data up into logic blocks that consist of Characteristics.
- Characteristic is a single data point, including an array of related data like X/Y/Z values from a 3-axis accelerometer.

**Here's an example of how it may look for a fitness tracking device:**

![image](https://user-images.githubusercontent.com/20091777/122649567-66cd5200-d0fc-11eb-8281-d39bb080e01d.png)

_Example of Profile structure (image by [Mohammad Afaneh](https://www.novelbits.io/author/mafaneh/))._

If we break down the example above into smaller pieces:

