# Networking Project for University Campus

This project outlines the design and configuration of a network for an academic campus, covering the IT and Department blocks, as part of the _EC4060 - Computer & Data Networks_ course. The project includes VLAN configuration, IP addressing, router and switch setup, and access restrictions.

## Project Overview

The project designs a network to support various blocks on campus, including the IT block and Department block, each with unique VLANs for different sections like offices, computer labs, and learning centers. The network is configured to provide security and efficient data routing across the campus.

## Network Design

### Main Routers

| Router Location           | Router Interface          | Interface Serial    | Needed Size | Allocated Size |
| ------------------------- | ------------------------- | ------------------- | ----------- | -------------- |
| University Main Router    | IT Block Router 0         | Interface serial2/0 | 2           | 4              |
| University Main Router    | Department Block          | Interface serial3/0 | 2           | 4              |
| IT Block Router 0         | IT Block Router 2         | Interface serial6/0 | 2           | 4              |
| IT Block Router 0         | IT Block Router 1         | Interface serial7/0 | 2           | 4              |
| Department Block Router 0 | Department Block Router 1 | Interface serial6/0 | 2           | 4              |
| Department Block Router 0 | Department Block Router 2 | Interface serial2/0 | 2           | 4              |

### IT Centre Block

| Block Name                        | Installed Devices   | VLAN | Needed Size | Allocated Size |
| --------------------------------- | ------------------- | ---- | ----------- | -------------- |
| Director Office                   | 2 PCs               | 4    | 9           | 16             |
| Network Manager Room              | 1 PC                | 4    | 9           | 16             |
| Technical Officer Room 1          | 1 PC                | 4    | 9           | 16             |
| Technical Officer Room 2          | 1 PC                | 4    | 9           | 16             |
| Meeting Room                      | 2 Data Points, WiFi | 5    | 8           | 16             |
| Staff Office                      | 5 PCs               | 5    | 8           | 16             |
| Printing Room                     | 2 Printers          | 5    | 8           | 16             |
| Computer Lab 1                    | 60 PCs              | 2    | 121         | 128            |
| Computer Lab 2                    | 60 PCs              | 2    | 121         | 128            |
| Digital Learning and Media Centre | 30 PCs, 1 Printer   | 3    | 33          | 64             |
| Lobby Area                        | WiFi                | 3    | 33          | 64             |

> **Note:** Staff rooms and printers in the printing room are restricted to access by staff only within the IT block.

### Department Block

| Block Name                               | Installed Devices                           | VLAN | Needed Size | Allocated Size |
| ---------------------------------------- | ------------------------------------------- | ---- | ----------- | -------------- |
| Lecture Hall 1 - 4                       | 1 PC per lecture hall, Multimedia Projector | 9    | 5           | 8              |
| Staff Room 1 - 14                        | 1 PC per staff room                         | 8    | 22          | 32             |
| Technical Officers Room 1 - 4            | 1 PC per room                               | 8    | 22          | 32             |
| Department Meeting Room                  | Video Conference Facility, WiFi             | 8    | 22          | 32             |
| Computer Lab 1                           | 50 PCs                                      | 6    | 101         | 128            |
| Computer Lab 2                           | 50 PCs                                      | 6    | 101         | 128            |
| Network Engineering Lab                  | 10 PCs                                      | 7    | 73          | 128            |
| Microprocessor Lab                       | 12 PCs                                      | 7    | 73          | 128            |
| Computer Vision and Machine Learning Lab | 50 PCs                                      | 7    | 73          | 128            |
| Department Office                        | 2 PCs, 1 Printer                            | 10   | 4           | 8              |

> **Note:** The Department Office and printers are accessible only to staff members within the department block.

## IP Address Range & Subnetting

### IT Centre Block

| VLAN | Allocated Size | Network ID  | Usable IP Address Range   | Broadcast ID | Default Gateway | Subnet Mask     | CIDR |
| ---- | -------------- | ----------- | ------------------------- | ------------ | --------------- | --------------- | ---- |
| 2    | 128            | 10.20.1.0   | 10.20.1.1 – 10.20.1.126   | 10.20.1.127  | 10.20.1.1       | 255.255.255.128 | /25  |
| 3    | 64             | 10.20.1.128 | 10.20.1.129 – 10.20.1.190 | 10.20.1.191  | 10.20.1.129     | 255.255.255.192 | /26  |
| 4    | 16             | 10.20.1.192 | 10.20.1.193 – 10.20.1.206 | 10.20.1.207  | 10.20.1.193     | 255.255.255.240 | /28  |
| 5    | 16             | 10.20.1.208 | 10.20.1.209 – 10.20.1.222 | 10.20.1.223  | 10.20.1.209     | 255.255.255.240 | /28  |

### Department Block

| VLAN | Allocated Size | Network ID  | Usable IP Address Range   | Broadcast ID | Default Gateway | Subnet Mask     | CIDR |
| ---- | -------------- | ----------- | ------------------------- | ------------ | --------------- | --------------- | ---- |
| 6    | 128            | 10.20.2.0   | 10.20.2.1 – 10.20.2.126   | 10.20.2.127  | 10.20.2.1       | 255.255.255.128 | /25  |
| 7    | 128            | 10.20.2.128 | 10.20.2.129 – 10.20.2.254 | 10.20.2.255  | 10.20.2.129     | 255.255.255.128 | /25  |
| 8    | 32             | 10.20.3.0   | 10.20.3.1 – 10.20.3.30    | 10.20.3.31   | 10.20.3.1       | 255.255.255.224 | /27  |
| 9    | 8              | 10.20.3.32  | 10.20.3.33 – 10.20.3.38   | 10.20.3.39   | 10.20.3.33      | 255.255.255.248 | /29  |
| 10   | 8              | 10.20.3.40  | 10.20.3.41 – 10.20.3.46   | 10.20.3.47   | 10.20.3.41      | 255.255.255.248 | /29  |

### Additional Router IP Assignments

- **IT Block Router 1 – interface serial 2/0**: `10.20.1.225/30`
- **IT Block Router 0 – interface serial 7/0**: `10.20.1.226/30`
- **IT Block Router 0 – interface serial 6/0**: `10.20.1.229/30`
- **IT Block Router 2 – interface serial 2/0**: `10.20.1.230/30`
- **Department Block Router 0 – interface serial 6/0**: `10.20.3.49/30`
- **Department Block Router 1 – interface serial 2/0**: `10.20.3.50/30`
- **Department Block Router 0 – interface serial 2/0**: `10.20.3.53/30`
- **Department Block Router 2 – interface serial 2/0**: `10.20.3.54/30`
- **University Main Router – interface serial 2/0**: `10.20.0.3/25`
- **University Main Router – interface serial 3/0**: `10.20.0.129/25`

```
For more information about this project and detailed configurations, please refer to the document ITandDeptBlockNetworking.pdf.
```
