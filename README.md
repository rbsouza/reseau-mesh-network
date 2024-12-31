# Reseau Mesh Network

This repository contains the configuration files and Ansible playbooks for my home mesh network, based on OpenWrt and B.A.T.M.A.N.

## Goals

The goal of this project is to create a robust, scalable, and secure home network with the following features:

*   **Mesh Network:** Using B.A.T.M.A.N. to provide seamless Wi-Fi coverage throughout the house.
*   **Redundancy:** Employing two internet gateways with automatic failover.
*   **VLAN Segmentation:** Isolating different types of traffic for improved security and performance.
*   **VPN:** Allowing secure remote access and anonymous browsing.
*   **Automation:** Using Ansible to automate the configuration and management of the network devices.
*   **Monitoring:** Using Zabbix to monitor the network's health and performance.

## Network Architecture

The network is built around the following components:

*   **Main Gateway:** Xiaomi AX3000T running OpenWrt.
*   **Backup Gateway:** Deco M5 running OpenWrt. This gateway will provide failover capabilities, taking over if the main gateway goes down.
*   **Mesh Nodes:** Multiple Deco M5 devices running OpenWrt, connected to the main gateway via B.A.T.M.A.N.
*   **VPN Gateway:** Deco M4R running OpenWrt, dedicated to VPN connections.
*   **Server 1:** Orange Pi running Zabbix, a database, and a web interface for management.
*   **Server 2:** Orange Pi used for network storage.

The network will be initially setup with a single internet gateway, with the second added later. The mesh network will be configured using the `reseau` SSID, with fast roaming enabled.

**Future implementations:**

*   A dedicated VPN SSID will be configured (`reseau-VPN`).
*   Multiple VLANs will be created to segment the network:
    *   VLAN 1: Main network (SSID: `reseau`)
    *   VLAN 10: VPN network (SSID: `reseau-VPN`)
    *   VLAN 20: IoT devices
    *   VLAN 30: Guest network
    *   VLAN 40: Servers
    *   VLAN 50: Security cameras
    *   VLAN 60: Multimedia (with QoS)

## Repository Structure

*   `/ansible`: Contains Ansible playbooks, inventory, and configuration files.
*   `/templates`: Contains Jinja2 templates for generating configuration files.
*   `/scripts`: Contains any helper scripts used in the project.
*   `README.md`: This file, providing an overview of the project.

## Getting Started

**Prerequisites:**

*   Ansible installed on your local machine or a dedicated server.
*   SSH access to all OpenWrt devices.
*   OpenWrt installed on all network devices (Xiaomi AX3000T, Deco M5, Deco M4R).

**Instructions:**

1.  Clone this repository to your local machine:

    ```bash
    git clone [URL inválido removido]
    ```

2.  Update the `ansible/inventory/hosts.ini` file with the correct IP addresses and credentials for your devices.

3.  Define your desired network configuration in `ansible/group_vars/all.yml`.

4.  Run the Ansible playbooks to configure the network:

    ```bash
    cd ansible
    ansible-playbook -i inventory/hosts.ini playbooks/update_openwrt.yml --ask-pass
    ansible-playbook -i inventory/hosts.ini playbooks/setup_network.yml --ask-pass
    ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
