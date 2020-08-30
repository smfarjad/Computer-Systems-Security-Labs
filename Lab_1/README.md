## Lab_1

I am using Seed Security Lab environment (Virtual Machine), which can easily be set up using VirtualBox. The virtual image of Seed Security Lab can be downloaded from [here](https://seedsecuritylabs.org/lab_env.html).

---
### Task 1: Writing Packet Sniffing Program

|   **Machine**    | **Assigned IP Address** |
|     :---:        |         :---:           |
| VM1              |  192.168.56.101         | 
| VM2              |  192.168.56.103         |
| VM3              |  192.168.56.104         |


#### Instructions

1. Open three virtual machines: VM1, VM2, and VM3

2. Set promiscous mode in each VM
```
sudo ifconfig eth0 promisc
```

2. Locate and compile the program sniffex.c on VM1
```
gcc -Wall -o sniffex sniffex.c -lpcap
```

3. Initiate ping session from VM2 to VM3
```
ping 192.168.56.104
```

4. Run sniffex program on VM1 for sniffing the packet transmission between VM2 and VM3
```
sudo ./sniffex eth13
```

5. Terminate the ping session on VM2 by issuing SIGTERM signal using Ctrl+C

> The commad `sudo ifconfig eth0 -promisc` can be used for unsetting the promiscous mode.

---
### Task 2: Spoofing

|   **Machine**    | **IP Address**                                          |
|     :---:        |         :---:                                           |
| VM1              |  Assigned: 192.168.56.101 **&** Spoofed: 192.168.56.104 |
| VM2              |  Assigned: 192.168.56.103                               |



#### Instructions

1. Open two virtual machines: VM1 and VM2

2. Locate and compile the program rawudp.c on VM1
```
gcc rawudp.c -o rawudp
```

3. Run rawudp program on VM1 (replace `192.168.1.103` with the IP address of VM2)
```
sudo ./rawudp 192.168.56.104 21 192.168.1.103 8080
```

4. On VM2, confirm the spoofing (IP of VM1 will be replaced by spoofed IP `192.168.56.104`) by using wireshark utility or `sudo tcpdump -vv` command.

5. Repeat the steps 2 to 4 with rawtcp.c program also, but on step 3 run following command:
```
sudo ./rawtcp 192.168.56.104 23 192.168.1.103 8008
```


---

