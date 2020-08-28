## Lab_1

I am using Seed Security Lab environment (Virtual Machine), which can easily be set up using VirtualBox. The virtual image of Seed Security Lab can be downloaded from [here] (https://seedsecuritylabs.org/lab_env.html).

---
### Task 1: Writing Packet Sniffing Program

#### Instructions

1. Open three virtual machines: VM1, VM2, and VM3

2. Set promiscous mode on each VM
```
sudo ifconfig eth0 promisc
```

2. Locate and compile the program sniffex.c on VM1
```
gcc -Wall -o sniffex sniffex.c -lpcap
```

3. Run sniffex program on VM1

4. Ping VM3 from VM2 and vice versa

The commad `sudo ifconfig eth0 -promisc` can be used for unsetting the promiscous mode.

---
### Task 2: Spoofing

#### Instructions

1. Open two virtual machines: VM1 and VM2

2. Locate and compile the program rawudp.c on VM1
```
gcc rawudp.c -o rawudp
```

3. Run rawudp program on VM1 (replace `192.168.1.102` with the IP address of VM2)
```
sudo ./rawudp 10.10.10.100 21 192.168.1.102 8080
```

4. On VM2, confirm the spoofing (IP of VM1 will be replaced by spoofed IP `10.10.10.100`) by using wireshark utility or `sudo tcpdump -vv` command.

5. Repeat the steps 2 to 4 with rawtcp.c program 

---

