# Azure Afloat - Concept
git
## Project Summary
---
The project consists of a core component and several electives. The core component is the IoT backbone for interacting with devices and their sensors as well as a web-based user interface for interacting with the humans on board. The core functionality of this project is to allow a user to gather data from their IoT devices and send that data to the Azure IoT Hub. 

Besides just measuring data, there are a few opportunities for the system to interact with the boat, the passengers, the environment, and other systems as well. It can steer the boat by sending signals to the autopilot, it can unlock the cabin door when a well-known face is recognized, or it can raise an alert to people on board when a whale is spotted!

One of our projects focus is to allow the user easy access to all the data through Azure services and visual displays via the web-UI. This project uses a data protocol called Signal K. It is a schema for the standardization of all the boat data, and it includes a server (written in Node.js) that handles the flow of all that data. 

## Technologies
---
+ Raspberry Pi3 
+ Raspberry Pi Zero
+ IoT Hub
+ Angular
+ TypeScript
+ Node
+ Cognitive Services
+ SignalK
+ Git
+ GitHub
+ RXJS

## Connecting Everything
---
The device messages go to the SignalK server and then to the Edge Hub using the plugin. That indirection is a design decision that allows us to embrace the SignalK community and possibly bring other SignalK users into Azure with an easy plugin. The device messages are not only being used by our server but also by our UI. We use a simple Angular table to display all the messages that are being transmitted by our devices.

## Server-SignalK
---
We are currently using SignalK as a node module in our server. We created a simple server and use the signal project as a dependency. This allows us a more flexibility within our code.

## Device-Node
---
Currently we have the device-node application sending mock data to both the UI and the server. The device-node is configured in such a way that the user can specify which device they want to relay messages from. If the server is disconnected, each message will be stored in its own file, then once the server reconnects those messages would be sent to the Azure IoT Hub.   

## Server-UI
---
We have designed our UI in such a way that it interacts with the data that is being sent to the server. The data is simultaneously being sent to the server and the UI. In the UI portion we created a table to display all the data flow. A compass-rose displays the wind direction and speed. The vessel diagram will alert the user of any issues that may arise. If something out of the ordinary happens and our devices catch this irregularity, the diagram will light up red and show the user exactly where the irregularity is coming from.

## Ikmock
---
This is a mock of the Ikommunicate that turns NMEA data into readable data using SignalK. It is a fork of the signal repository on GitHub. We just configured it to send NMEA 0183 data to our server with mock data.

## SignalK-iothub-plugin
---
This plugin allows for the data received by the server via the device-node application to be sent to the Azure IoT Hub. This allows the user to configure as many devices as they like and add their own device-keys used by Azure services. We will also be contributing this to NPM and the SignalK community.

## SignalK-websocket-provider
---
This allows the Ikmock to reconnect to the server after the server has been started. It will try to reconnect to the server every 5 seconds if the server is disconnected. We published this WebSocket provider on NPM and contributed it to the SignalK community.

## Future
---
As we move forward with the project, we'd like to create a critter detection application that would alert passengers of critters nearby. We also want to keep contributing to the SignalK community through PRs and our SignalK-iothub-plugin. We would also like to make the vessel diagram into an interactive experience by using three.js.

