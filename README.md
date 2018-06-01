Just getting started with Azure Afloat? Start here. Looking for in-depth help and explanations on how it works? Yeah, that's here too.

Azure Afloat is a Microsoft intern project. The project implements a robust and modern digital system for a boat. It starts with a network of IoT devices and one larger, more capable device that acts as the server. There's an adapter too from the boat's existing data systm (NMEA), so that everything that happens on the boat can be measured, and all of that data can go to the cloud.

A boat is a perfect test bed for an IoT project too, because sometimes it has a high-speed connection to the cloud (at the dock), sometimes it has a very low speed connection (over something like a satellite phone), and often it has no connection at all. Regardless of the connection status, though, the entire system must keep working - measuring, recording, and reporting data.

Besides just measuring data, there are a few opportunities for the system to interact with the boat, the passengers, the environment, and other systems as well. It can steer the boat by sending signals to the autopilot, it can unlock the cabin door when a well-known face is recognized, or it can raise an alert to people on board when a whale is spotted!

The project consists of a core component and a number of electives. The core component is the IoT backbone for interacting with devices and their sensors as well as a web based user interface for interacting with the humans on board.

This project uses a data protocol called Signal K. It's a schema for the standardization of all of the boat data, and it includes a server (written in Node.js) that that handles the flow of all of that data. It's a very cool project.

# Getting Started

If you want to get started playing with Azure Afloat, use the repositories in this GitHub organization. Here's how...

1. First clone the following repositories: `ikmock`, `server-signalk`, and `device-node`. I recommend you clone all three of those projects into a top-level folder called `AzureAfloat`.

    The `ikmock` project simulates the device on the boat that translates all of the legacy boat data. It actually replays a bunch of real chatter generated from a real boat trip.

    The `server-signalk` project is the main data server. It pulls in the data from `ikmock` and merges all data streams into one master stream.

    The `device-node` project is a simulator for the devices that will be deployed throughout the boat. It's a monolithic code base and can act as any one of the devices by passing it a command line argument (i.e. `-d rpz-cockpit` to simulate the cockpit device).

1. Next, create a file inside the ikmock folder called `.env` and use this for its contents...
    ``` bash
    PORT=3001
    NMEA0183PORT=10111
    TCPSTREAMPORT=3859
    ```

    This tells the ikmock to make all of its data available on port 3001. The main stream will connect to this.

1. Next, still inside the `ikmock` folder, run `npm install`. Make sure you have a modern version of Node.js installed on your system.

1. Run the ikmock project using `npm start`. It should say that it's running at `0.0.0.0:3001`.

1. Now, we're going to work on the `server-signalk` project, so leave ikmock running in its console window and open a new one. First, you need to make sure you have Python installed on your system. Python 2.7 or 3.6 should suffice. Also, you need something called the Bonjour SDK for Windows. You have to register with Apple to download this, and you can find it [here](https://developer.apple.com/download/more/?=Bonjour%20SDK%20for%20Windows).

1. Now, from inside the `server-signalk` folder, you can do `npm install` and hopefully see it all work.

1. Now, run this project using `npm start`. This one should say that it's running at `0.0.0.0:3000`. So that's the primary data endpoint. Note that `0.0.0.0` is a _loopback_ and points to your machine. It's functionally equivalent to `localhost`.

1. When you started that second server `server-signalk`, it was configured to pull in the data from the `ikmock` project, so data is actually flowing, but you'd like to be able to see that. So open your browser and visit Signal K's admin portal at http://localhost:3000.

1. Now it's time to add some custom data using device simulators. Open another console window and go to the `device-node` project and run `npm install`. Then run `node . -d rpz-cockpit`. That fires off the device code and runs the code specific to the device we'll have installed in the boat's cockpit. If you look back at the admin portal, you'll see a new data source called "ws".

1. Now start a second device with a different role. Open a new console window, go back to the `device-node` project and try `node . -d rpz-masthead`. These are all of the devices we've defined so far: `rpz-cockpit`, `rpz-masthead`, `rpz-engine`, `rpz-master`, `rpz-aftport`, `rpz-aftstar`, and `rpz-cabin`.

Please let us know if you have feedback on the project by submitting an issue to the appropriate repository.