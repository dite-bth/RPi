#ansluta via ssh till RPi

ssh -> https://sv.wikipedia.org/wiki/Secure_Shell


### ta reda på din RPI's ip
Med ssh kan vi alltså ansluta till ett terminalgränssnitt till vår RPi.
Innan vi kan göra det måste vi veta om den ip-adress vår RPi har. Exekvera kommandot ifconfig på din RPi och leta upp raden där `inet address` listas.

Exempel;
```bash
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

### anslut via Putty

Putty -> http://www.chiark.greenend.org.uk/~sgtatham/putty/

öppna Putty och skriv in ip-adressen i textfältet som heter "Host Name (or IP address)". Tryck <RET> eller klicka på knappen "Open" - se bilden putty.png i denna mappen.
Nu loggar du in med användarnamnet och lösenordet för din RPi i terminalen.


### anslut via annan terminal, t ex via Git bash

Med programmet Git bash (https://git-scm.com/downloads) har du en terminal installerad på din maskin (Windows m.fl). Med den terminalen följer ssh med, vilket gör att du kan ansluta till din RPi genom att starta Git bash och sedan skriva kommandot för att ansluta till en RPi.

Starta programmet Git bash och skriv följande kommando;

```
$ ssh pi@41.131.259.82
```

där pi är användarnamnet och ip-adressen till din RPI är angiven efter '@'.
Nu kan du logga in.

### anslut via ssh på Linux och OS X
Grattis. Dessa OS har redan en terminal med ssh inbyggt.
Starta en terminal och skriv kommandot `$ ssh pi@41.131.259.82` (där pi är användarnamn och ip-numret ska vara det som gäller för din RPi).
