## What is a Command and Control Framework

![661abd734022d8a1f3050e90d3fb6861](https://user-images.githubusercontent.com/95729902/214460378-b4909d32-6bf9-4cfe-bbcf-79de3a883c4c.png)

## Comamnd and Control Structure

#### C2 Server

 The C2 Server serves as a hub for agents to call back to. Agents will periodically reach out to the C2 server and wait for the operator’s commands.

![5de5e62c5ba37013302790062b6b429e](https://user-images.githubusercontent.com/95729902/214460538-7efae58a-82ea-4967-a410-d803ff0bfe8a.png)

#### Agents/Payloads

An agent is a program generated by the C2 framework that calls back to a listener on a C2 server. Most of the time, this agent enables special functionality compared 
to a standard reverse shell. Most C2 Frameworks implement pseudo commands to make the C2 Operator’s life easier. Some examples of this may be a pseudo command to Download 
or Upload a file onto the system. It’s important to know that agents can be highly configurable, with adjustments on the timing of how often C2 Agents beacon out to a Listener on a C2 Server and much more.

#### Listeners

A listener is an application running on the C2 server that waits for a callback over a specific port or protocol. Some examples of this are DNS, HTTP, and or HTTPS.

#### Beacon

A Beacon is the process of a C2 Agent calling back to the listener running on a C2 Server.

## Obfuscating Agent Callbacks

#### Sleep Timers

One key thing that some security analysts, anti-virus, and next-generation firewalls look for when attempting to identify Command and Control traffic is beaconing and the rate at which a device beacons out to a C2 server. Let’s say a firewall observed traffic that looks like so

- TCP/443 - Session Duration 3s, 55 packets sent, 10:00:05.000
- TCP/443 - Session Duration 2s, 33 packets sent, 10:00:10.000
- TCP/443 - Session Duration 3s, 55 packets sent, 10:00:15.000
- TCP/443 - Session Duration 1s, 33 packets sent, 10:00:20.000
- TCP/443 - Session Duration 3s, 55 packets sent, 10:00:25.000

A pattern is starting to form. The agent beacons out every 5 seconds; this means that it has a sleep timer of 5 seconds.

#### Jitter

Jitter takes the sleep timer and adds some variation to it; our C2 beaconing may now exhibit a strange pattern that may show activity that is closer to an average user:

TCP/443 - Session Duration 3s, 55 packets sent, 10:00:03.580
TCP/443 - Session Duration 2s, 33 packets sent, 10:00:13.213
TCP/443 - Session Duration 3s, 55 packets sent, 10:00:14.912
TCP/443 - Session Duration 1s, 33 packets sent, 10:00:23.444
TCP/443 - Session Duration 3s, 55 packets sent, 10:00:27.182