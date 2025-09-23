# OpenVAS (Open Vulnerability Assessment System)

OpenVAS is free software used to detect and manage vulnerabilities in computer systems and networks. It provides various services and tools for vulnerability assessment such as identifying and analyzing security issues including misconfigurations, outdated software, and weak passwords that could be exploited by attackers.

## Working of OpenVAS

OpenVAS consists of a server and various client-side tools for scanning and reporting. It uses a regularly updated database of known vulnerabilities and checks systems against these to detect potential weaknesses. The tool performs a comprehensive scan of the specified targets, identifying potential vulnerabilities and generating detailed reports with recommendations for remediation.

### Steps of Vulnerability Assessment

1. Classifies the system resources.  
2. Allocates enumerable values to the classified resources.  
3. Detects possible threats (vulnerabilities) in each resource.  
4. Eliminates vulnerabilities on a priority basis.  

## Components of OpenVAS Architecture

### 1. OpenVAS Scanner
- The primary engine that performs the actual scanning of target systems.  
- Uses *Network Vulnerability Tests (NVTs)* to detect security vulnerabilities.  

### 2. OpenVAS Manager
- Manages scan configurations, schedules, and stores scan results.  
- Acts as an intermediary between the scanner and user interfaces, handling scan requests and processing results.  

### 3. Greenbone Security Assistant (GSA)
- A web-based *graphical user interface (GUI)* for managing scans, configuring settings, and viewing scan results.  
- Provides an easy-to-use platform for interacting with OpenVAS.  

### 4. OpenVAS CLI
- A *command-line interface* for users who prefer scripting and command-line operations.  
- Enables management of scans, targets, and results through commands and scripts.  

### 5. Greenbone Security Feed (GSF)
- A continuously updated feed providing the latest *NVTs* and security information.  
- Ensures OpenVAS can detect the most recent vulnerabilities.  

### 6. OpenVAS Libraries
- Provide essential functionalities for the scanner and manager, such as network communication, data storage, and cryptographic operations.  

### 7. Database
- Stores scan results, configurations, and other essential data.  
- Ensures data persistence and retrieval for analysis and reporting.
