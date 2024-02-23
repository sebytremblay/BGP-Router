# CS3700-P3-BGP-Router

This project is an implementation of a simplified BGP router for the CS3700 Networks course. The router is implemented in the [`3700router`] Python script.

## Getting Started

To run the router with a specific configuration, use the [`run`] script with the path to the configuration file as an argument:

```bash
./run configs/1-1-simple-send.conf
```

The [`configs`] directory contains various configuration files that simulate different routing scenarios.

## Overall steps taken
### Repo Initialization & Project Setup
First, we imported the starter code from the repo. The starter code includes an implementation of a router which simply connects to its peers, sends a handshake message, and prints out every other message it receives.

### Our Program

We modified the `3700router.py` file to implement the required functionality for the BGP router. Here is an overview of the changes made:

#### High-level Approach

The [`3700router`] script implements a simplified BGP router. When the router starts, it establishes connections with its peers and exchanges handshake messages. After that, it listens for incoming BGP messages and handles them according to the BGP protocol.

The router maintains a forwarding table and an updates cache. When it receives a route announcement, it adds the route to the forwarding table and the updates cache. When it receives a route withdrawal, it removes the route from the forwarding table and the updates cache, and then disaggregates the forwarding table.

- Implemented the BGP protocol to establish and maintain BGP sessions with neighboring routers.
- Handled the exchange of BGP messages, including OPEN, UPDATE, KEEPALIVE, and NOTIFICATION messages.
- Implemented the decision process for selecting the best route based on BGP attributes.
- Handled the advertisement and withdrawal of routes to and from neighboring routers.

#### Challenges Faced

One of the main challenges was handling route aggregation and disaggregation correctly. When a route is announced, the router needs to aggregate the forwarding table to combine adjacent routes. When a route is withdrawn, the router needs to disaggregate the forwarding table to break down aggregated routes.

- Understanding the BGP protocol and its message format.
- Handling the different BGP attributes and their impact on route selection.
- Ensuring the correct handling of BGP session establishment and maintenance.
- Implementing error handling and error reporting for BGP messages.

#### Properties/Features

The [`3700router`] script supports the following BGP messages: OPEN, UPDATE, KEEPALIVE, and NOTIFICATION. It handles route announcements and withdrawals, and it maintains a forwarding table and an updates cache. It also supports route aggregation and disaggregation.

- Establishes BGP sessions with neighboring routers.
- Exchanges BGP messages to exchange routing information.
- Implements the decision process to select the best route.
- Advertises and withdraws routes to and from neighboring routers.
- Handles BGP session establishment and maintenance.

#### Testing Overview

The [`run`] script is used to test the router with different configuration files. Each configuration file simulates a different routing scenario, and the script checks that the router handles each scenario correctly.

The [`test`] script can be used to run a suite of tests automatically:

```bash
./test
```

For more details on the implementation, please refer to the code in the `3700router.py` file.
