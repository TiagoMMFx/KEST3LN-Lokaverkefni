# KEST3LN-Lokaverkefni
Repository fyrir Linux Lokaverkefni

1. Install and configure the server1, client1 and client2 with hostnames and domain as ddp.is

We start by accessing server1 and modifying the configuration files "/etc/hosts" and "/etc/hostname." In these files, we make the necessary changes as follows:

![Client1-Hosts](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/6185e7cb-098a-456f-9d28-95dcf88f416d)
![Client2-Hosts](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/42f6ed58-af68-452a-ba87-3867d8326d61)

2. Configure server1 with static IP Address, from the IP Address block 192.168.100.0/24.
   The server must be configured with the 10th usable IP Address

The initial step involves configuring the "01-network-manager" YAML file in a specific manner.

![server_network](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/49dbc465-598b-4735-b209-c6ae203295fa)

Following this, the next action is to execute the command "netplan apply" and subsequently reboot. Upon returning to our machine, we can use the "ip address" command to check if our server has been configured correctly, as demonstrated below.

![ip-address-command](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/3f2c72e0-b47e-406b-89df-ad05123a6d71)

3. Install and configure DHCP on server1, so both clients get an IP Addresses, Gateway, DNS IP address and domain name automatically via HDCP.

The initial step is to install the ISC DHCP server by executing the command "sudo apt install isc-dhcp-server." The subsequent step involves editing the DHCP configuration file, which can be accomplished using the command "sudo nano /etc/dhcp/dhcpd.conf." Within this file, we proceed to create a subnet in the following manner:

![dhc-server1](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/aff641ff-a825-421a-ba69-e3142be6214e)

Following that, we proceed to designate the interface to which we want the DHCP to be allocated, specifying it as "ens33" as illustrated below:

![dhc-ens33](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/634f5517-215e-4edb-bdf6-ae865a25e986)

Now, we restart the DHCP service and verify its status, as shown below:

![dhcp-active](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/865677ae-5027-40d6-a006-b7a4e988b207)

4. Install and configure DNS server on server1, so Hostnames are resolved to IP Addresses.

To set up and configure DNS, the first step is installing DNS using the command "sudo apt install -y bind9 bind9-utils." Afterward, specific files, such as "/etc/bind/named.conf.local," need to be modified. The content of this file should resemble the following:

  ![dns-bind](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/b6da36b6-fe9c-4eb3-9021-ad5d93858f26)

Next, we create the forward zones, such as "/etc/bind/server1.ddp.is.db," and replicate the process for the reverse lookup. The configuration files for both should resemble the following:

![dns-server-bind](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/da83ef4d-02f6-49b5-8587-8d7370b2e4c7)

And our reverse zone file:

![dns-r-server-bind](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/6df55f5c-4889-48e0-b45f-21b73dbbba26)

Afterward, we can perform a double-check to ensure everything is running smoothly, as demonstrated below:
(Please note that we get two Ip Addresses & Mac Addresses, 1 from the server and 1 from the local pc where the server is running on)

![nslookup-dns](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/3b4dd309-34b2-4380-9a09-0e8cbd7a39be)

5. Create the users accounts using a script, see the Users file

I've crafted a straightforward bash script for this purpose. Here's a snippet:

![user-scripts](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/41c01975-4713-4ab9-bc63-ed46045da119)

Consequently, our users and groups are established in the following manner:

![Users](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/ef8fef43-c8e6-4499-9cdb-4b935dbc8774)

![Deildir](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/ceed780a-c190-47e4-ae3e-c217ccfb9c72)

6. Install and configure MySQL on server1 and create Human Resource database.

Initially, we install the MySQL server using the command "sudo apt install mysql-server." Subsequently, we access MySQL with "mysql -u root -p." Within the MySQL terminal, we execute "show databases;" to display our databases and create a new database using "create database Human_Resources;". We can then verify the existence of the database as follows:

![Database](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/9e7d69af-ddaa-48ab-a1d2-a22b3671cad0)

Now, we proceed to create the tables by executing the command "use Human_Resources;" followed by "CREATE TABLE (TableName)" Subsequently, we can verify the existence of our tables:

![Human-Resource_Database](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/0506a6a6-cbe0-4f8a-80ed-9ff23836ba22)

To view the details within our tables, we can use the command "DESCRIBE TableName" as follows:

![Table-Employees](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/ec9fe644-afd9-48bc-957c-4478efb188a4)

![Table-Locations](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/8710dcb5-7f42-4570-a4ea-0ccf6b4140d8)

![Table-Jobs](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/e3688d47-e5c6-46ec-afd1-d5367eac29ae)

![Table-Department](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/162c187d-abfe-4418-8484-0318cb9d3e4b)

7. Due to data loss the company policy requires taking backups weekly, as system engineer you are required to schedule backups of home directories to run weekly at midnight each Friday.

First, what we'll do is modify the crontab file as follows:

![Backup_Weekly](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/56cc6a64-b127-492b-969d-0116045094ea)

Next, we aim to create our bash backup script that backs up each user directory on the server. Here is an example of how it could be structured:

![Backup_Script](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/6d058baf-688f-4645-a6b5-467e99b17275)

8. Install and configure NTP on the server and clients, server1 must be master server to synchronize the time of the clients.

The first step is to install NTP by using the command "sudo apt install ntp." Following that, we will edit the ntp.conf file on our server in the following manner:

![ntp-server1](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/7fc084ec-4681-4261-910e-8413a27b6d3a)

Following that, we'll use the command "sudo apt install ntpdate" & "ntp" on our clients to install NTPdate and NTP. Prior to syncing the time with our server, it's essential to edit the configuration file to match the following:

![Ntpdate_client1](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/74132157-35cd-4928-a684-bd62a6bfd8c6)

Afterward, we can verify whether our client has successfully synchronized with our server.

![ntp_synced](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/07622439-da6c-4f7d-80f4-eda9edad8ecb)

9. Install and configure syslog server on server1, server1 should get logs from both the clients for proactive management and monitoring.

On our server, we need to modify the rsyslog.conf file, and this can be achieved as follows:

![syslog_server](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/d045404d-7859-4aec-a4ca-eb2028355be1)

Next, we aim to edit the rsyslog.conf file on our clients, and the process is outlined as follows:

![rsyslog_clients](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/bb94a6ec-6005-40a0-9ff6-bff010c8ae5a)

And then we can see in our syslog files whether it worked or not.

(picture of it working)

10. Install and configure Postfix on server1, so users can send and receive emails using Round Cube open-source software.

I won't be concluding this task.

11. Install and configure shared printers for each group, only users that belong to the group should print only, accept IT and Management groups should print and manage the printers.

I won't be concluding this task.

12. For security reasons, install and configure SSH on the server and clients, SSH login should use RSA keys instead of the password authentication.

On the server, we'll have to use "sudo apt install openssh-server" and execute the following commands after generating an RSA key.




13. All unused ports should be closed, use NMAP for testing.

On the server, execute the command sudo apt install nmap to install Nmap. To assess the status of our ports, use the following command: nmap 192.168.100.10, where 192.168.100.10 represents the IP address of our server.

![nmap](https://github.com/TiagoMMFx/KEST3LN-Lokaverkefni/assets/80530415/bcbbfa49-2790-48fd-a4cf-834d43b87ac2)

As evident, our server maintains security by having only the necessary ports open as required.






