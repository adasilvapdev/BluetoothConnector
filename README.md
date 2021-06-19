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

**If we break down the example above into smaller pieces:**

![image](https://user-images.githubusercontent.com/20091777/122649989-7fd70280-d0fe-11eb-9ab9-46a02ebe319e.png)

_Image by [Stormotion](https://stormotion.io/blog/what-to-consider-when-integrating-ble-in-your-react-native-app/)._

_You can read a bit more on GATT, Profile, Services and Characteristics [here](https://learn.adafruit.com/introduction-to-bluetooth-low-energy/gatt), and on Notifications & Indications — [here](https://community.nxp.com/docs/DOC-328525)._
____________________________________________________________________________________________________________________________________________

**About the library I'm going to use**
 [react-native-ble-plx](https://openbase.com/js/react-native-ble-plx)

**This is React Native Bluetooth Low Energy library wrapping [Multiplatform Ble Adapter](https://github.com/gkapusta/MultiPlatformBleAdapter).**

It supports:
- [Observing device's Bluetooth adapter state](https://github.com/dotintent/react-native-ble-plx/wiki/Bluetooth-Adapter-State)
- [Scanning BLE devices](https://github.com/dotintent/react-native-ble-plx/wiki/Bluetooth-Scanning)
- [Making connections to peripherals](https://github.com/dotintent/react-native-ble-plx/wiki/Device-Connecting)
- [Discovering services/characteristics](https://github.com/dotintent/react-native-ble-plx/wiki/Device-Service-Discovery)
- [Reading](https://github.com/dotintent/react-native-ble-plx/wiki/Characteristic-Reading)/[writing](https://github.com/dotintent/react-native-ble-plx/wiki/Characteristic-Writing) characteristics
- [Observing characteristic notifications/indications](https://github.com/dotintent/react-native-ble-plx/wiki/Characteristic-Notifying)
- [Reading RSSI](https://github.com/dotintent/react-native-ble-plx/wiki/RSSI-Reading)
- [Negotiating MTU](https://github.com/dotintent/react-native-ble-plx/wiki/MTU-Negotiation)
- [Background mode on iOS](https://github.com/dotintent/react-native-ble-plx/wiki/Background-mode-(iOS))
- Turning the device's Bluetooth adapter on

It does NOT support:
- Bluetooth classic devices.
- Communicating between phones using BLE (Peripheral support)
- [Bonding peripherals](https://github.com/dotintent/react-native-ble-plx/wiki/Device-Bonding)
____________________________________________________________________________________________________________________________________________

**✅ Apps to Test BLE Devices**

When developing a React Native mobile app with BLE integration, we will need to test probably need to test how it really works such devices. The Stormotion team used the following apps:
- nRF Connect for Mobile ([Android](https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=uk))
- BLE Scanner ([Android](https://play.google.com/store/apps/details?id=com.macdom.ble.blescanner&hl=uk) | [iOS](https://apps.apple.com/ru/app/ble-scanner-4-0/id1221763603))

_The tools are quite similar and provide many options to test different features of BLE devices._
____________________________________________________________________________________________________________________________________________
**⚠️ Possible Pitfalls when Integrating BLE Devices**

During the integration of BLE, some difficulties may arise that can complicate the development process. 
Here are some recommendations on how you can make the development go smoother:

# 1: Turn on geolocation 🌍
If you’re developing an Android application, this one will be important. As written in documentation: “Starting from Android API 23+, to access the hardware identifiers of nearby external devices via Bluetooth and Wi-Fi scans, your app must now have the geolocation enabled”.

To check whether geolocation is enabled and turn it on in case its not, we recommend using the [react-native-android-location-enabler](https://github.com/Richou/react-native-android-location-enabler) library.

# 2: Turn on Bluetooth 📳
We need to turn on Bluetooth on the device before scanning. For this purpose I'm going to use: [react-native-ble-plx](https://github.com/dotintent/react-native-ble-plx)

# 3: Change device name 📱
When using react-native-ble-plx we may stumble upon a bug when the device name wouldn’t change. That happens because name is cached. This issue is tracked [here](https://github.com/dotintent/react-native-ble-plx/issues/230).

# 4: Keep code quality high 🏆

Finally, here are few general tips to improve code quality:

- Keep all the characteristics and services UUID in one place.
- Avoid magic numbers in characteristic. Instead, use constants.
- Organize the logic structure into 2 separate files:
  * One file to keep logic that contains code that is not related to communication with a specific device (e.g. scanning, connection, disconnection);
  * Another file for code that contains communication with a specific device — discovering services/characteristics, observing notifications/indications, reading/writing characteristics and others.
