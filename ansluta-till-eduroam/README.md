### Ansluta till eduroam med WiFi
För att ansluta till eduroam via WiFi från din RPi krävs lite konfiguration. Följande guide gäller uppkoppling mot eduroam på BTH (Blekinge tekniska högskola).

1. Se till att din WiFi dongel fungerar med drivrutin etc.
2. Ta reda på namnet på ditt nätverkskort (dongel). Vanligen: wlan0
3. Nu ska du lägga till certifikatfilen - spara filen `eduroam_bth.pem`, som finns i detta repot i din hemmakatalog (eller annat valfritt ställe).

4. Redigera filen /etc/wpa_supplicant/wpa_supplicant.conf med en texteditor (exemplen nedan använder vim och nano). Tänk på att du måste göra detta med "super user"-rättigheter (sudo)

    `sudo vi /etc/wpa_supplicant/wpa_supplicant.conf`  
     eller  
    `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

4. Skriv följande i filen

      `network={`  
      `ssid="eduroam"`  
      `key_mgmt=WPA-EAP`  
      `eap=PEAP`  
      `pairwise=CCMP`  
      `group=CCMP TKIP`  
      `ca_cert="/home/pi/eduroam_bth.pem"`  
      `identity="ditt användarnamn"`  
      `domain_suffix_match="radius.bth.se"`  
      `phase2="auth=MSCHAPV2"`  
      `password="ditt lösenord"`  
      `}`

5. Redigera filen /etc/networks/interfaces och skriv in följande i filen (om det inte redan står).  Innan du redigerar bör du nu enligt punkt 2 veta vad ditt nätverkskort heter. Nedan används `wlan0`, men det kan heta något annat t ex `wlp1s0`. För att ta reda på vad ditt heter kan du kolla output från ifconfig eller iwconfig. Om det heter något annat, byt ut wlan0 till aktuellt namn.

    `auto wlan0`  
    `allow-hotplug wlan0`  
    `iface wlan0 inet manual`  
    `wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf`  

6. Till sist - boota om din RPi eller starta om nätverkskortet för att kolla så att allt funkar. Med kommandot ifconfig kan du kolla om ditt nätverkskort har fått en IP-adress. Leta efter "wlan0" (eller vad ditt nätverkskort heter) i outputen.Aktivera konfigurationen och testa om det funkar.  
    Antingen omstart: `sudo reboot` eller starta om nätverkskortet: `sudo ifdown wlan0 && ifup wlan0`.  
    Kolla om du fått ett IP: `ifconfig`.  
    Testa att pinga: `ping -c3 www.google.com`. 
