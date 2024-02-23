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

The router maintains a forwarding table and an updates cache. When it receives a route announcement, it adds the route to the forwarding table and the updates cache. When it receives a route withdrawal, it removes the route from the forwarding table. Then, we remove all updates that have the specified network, netmask, and source. We then delete the table and rebuild it from the new updates cache in order to account for the aggregation.

#### Challenges Faced

One of the main challenges was handling route aggregation and disaggregation correctly. When a route is announced, the router needs to aggregate the forwarding table to combine adjacent routes. When a route is withdrawn, the router needs to disaggregate the forwarding table to break down aggregated routes.

However, our biggest issue was that when we were rebuilding the table from the parsed updates cache after withdrawal, the table contained incorrect update information. We met with 4 different TA's about this issue, none of whom were able to figure out the bug in the code. We also consulted Professor Jackson. As such, we were unable to resolve the issue and commented out the rebuild_table method call when processing route withdrawals.

#### Properties/Features

The [`3700router`] script supports the following BGP messages: UPDATE, WITHDRAW, HANDSHAKE, DATA, and DUMP. It handles route announcements and withdrawals, and it maintains a forwarding table and an updates cache. It also supports route aggregation and disaggregation.

#### Testing Overview

The [`run`] script is used to test the router with different configuration files. Each configuration file simulates a different routing scenario, and the script checks that the router handles each scenario correctly.

We individually ran each of the configuration files and reviewed the output log for correctness.

```bash
./run config/x-x
```

The [`test`] script can be used to run a suite of tests automatically:

```bash
./test
```

For more details on the implementation, please refer to the code in the `3700router.py` file.
