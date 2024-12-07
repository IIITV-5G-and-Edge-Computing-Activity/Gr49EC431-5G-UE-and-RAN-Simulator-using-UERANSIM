# 5G UE and RAN Simulator with Open5GS and UERANSIM

## Overview
This project demonstrates the simulation of a 5G network using Open5GS as the 5G core and UERANSIM for User Equipment (UE) and Radio Access Network (RAN) emulation. It includes configurations for deploying a fully functional 5G setup, testing connectivity, and analyzing network performance.

## Features
- **5G Core Simulation**: Implemented using Open5GS.
- **UE and RAN Emulation**: Managed with UERANSIM.
- **Subscriber Management**: Configured via Open5GS WebUI.
- **Testing Tools**: Ping and iperf for validating network performance.
- **Automated Configuration**: Scripts and configuration files for seamless setup.

## Technologies Used
- **Open5GS**: Open-source implementation of 5G core.
- **UERANSIM**: Open-source 5G UE and RAN simulator.
- **Ubuntu VirtualBox**: Virtualized environment for the deployment.
- **iperf**: Bandwidth testing.

## Getting Started

### Prerequisites
- Ubuntu VirtualBox installed.
- Basic knowledge of networking and 5G concepts.
- Dependencies installed:
  - Open5GS
  - UERANSIM
  - MongoDB
  - NodeJS

### Installation

1. **Update System Packages**:
   ```bash
   sudo apt-get update
   sudo apt-get install -y gnupg wget curl
   ```

2. **Install MongoDB**:
   ```bash
   wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
   sudo apt update
   sudo apt install -y mongodb-org mongodb-org-database
   sudo systemctl start mongodb
   sudo systemctl enable mongodb
   ```

3. **Install Node.js**:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt install nodejs
   ```

4. **Install Open5GS**:
   ```bash
   add-apt-repository ppa:open5gs/latest
   apt-get install -y software-properties-common
   apt-get -y update && apt install -y open5gs
   ```

5. **Install the WebUI**:
   ```bash
   curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -
   ```

6. **Install UERANSIM**:
   ```bash
   sudo apt install make gcc g++ libsctp-dev lksctp-tools iproute2 git
   sudo snap install cmake --classic
   git clone https://github.com/aligungr/UERANSIM
   cd UERANSIM
   make
   ```

7. **Add Subscriber in Open5GS WebUI**:
   - Access the WebUI at `http://<server-ip>:3000`.
   - Add a new subscriber with the appropriate IMSI, Key, and OP/OPc values.

8. **Configure gNodeB and UE**:
   - Place the configuration files (`gnb.yaml`, `ue.yaml`) in the respective directories.

9. **Start the Simulation**:
   ```bash
   ./nr-gnb -c gnb.yaml
   ./nr-ue -c ue.yaml
   ```

### Usage

1. **Ping Test**:
   Verify connectivity between the UE and gNodeB:
   ```bash
   ping -I <ue-ip> <gNodeB-ip>
   ```

2. **Iperf Test**:
   Measure bandwidth between UE and gNodeB:
   - Start iperf server on the gNodeB:
     ```bash
     iperf3 -s -B <gNodeB-ip>
     ```
   - Run the iperf client on the UE:
     ```bash
     iperf3 -c <gNodeB-ip> -B <ue-ip>
     ```

### Architecture

- **Core Network**: Open5GS handles Authentication, Session Management, and Data Network communication.
- **RAN Simulation**: UERANSIM provides NR gNodeB and NR UE functionalities.

## Project Structure
```
5g-simulator/
├── config/
│   ├── gnb.yaml
│   ├── ue.yaml
├── build/
│   ├── nr-gnb
│   ├── nr-ue
.
.
.
```

## Testing Scenarios
- **Basic Connectivity**: Ping test between UE and gNodeB.
- **Bandwidth Analysis**: Iperf tests under varying configurations.
- **Subscriber Variants**: Test with different subscriber profiles in MongoDB.

## Future Enhancements
- Integration of additional 5G features like slicing.
- Automated deployment scripts for multi-node setups.
- Performance benchmarking for various test scenarios.

## Contributions
Contributions are welcome!

## Acknowledgments
- [Open5GS](https://open5gs.org/)
- [UERANSIM](https://github.com/aligungr/UERANSIM)

---
Feel free to explore, test, and contribute to this project!
