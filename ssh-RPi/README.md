#ansluta via ssh till RPi

ssh -> https://sv.wikipedia.org/wiki/Secure_Shell

Med ssh kan vi alltså ansluta till ett terminalgränssnitt till vår RPi.
Innan vi kan göra det måste vi veta om den ip-adress vår RPi har. Exekvera kommandot ifconfig på din RPi och leta upp raden där `inet address` listas.

Exempel;
```
$ ifconfig <RET>
wlan0      Link encap:Ethernet  HWaddr 04:01:b8:08:58:01
          inet addr:41.131.259.82  Bcast:46.101.255.255  Mask:255.255.192.0
          inet6 addr: fe80::601:b8ff:fe08:5801/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1578231 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1642914 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:447187498 (447.1 MB)  TX bytes:295438488 (295.4 MB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:4570782 errors:0 dropped:0 overruns:0 frame:0
          TX packets:4570782 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:1111739966 (1.1 GB)  TX bytes:1111739966 (1.1 GB)
          
$ _
```
          

I exemplet ovan ser vi att vår ip-adress är 41.131.259.82 - den ska vi använda i t ex Putty för att ansluta.
