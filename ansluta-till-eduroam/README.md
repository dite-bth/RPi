### Ansluta till eduroam med WiFi
För att ansluta till eduroam via WiFi från din RPi krävs lite konfiguration. Följande guide gäller uppkoppling mot eduroam på BTH (Blekinge tekniska högskola).

1. Se till att din WiFi dongel fungerar med drivrutin etc.
2. Ta reda på namnet på ditt nätverkskort (dongel). Vanligen: wlan0
3. Skapa en certifikatfil för att få ansluta till BTHs nätverk och spara den på lämplig plats. Exempelt nedan sparar filen i den förkonfigurerade användaren pi:s hemkatalog. Obs, det är viktigt att filens innehåll får radbrytningar precis som nedan.

    `echo "-----BEGIN CERTIFICATE-----  
    MIID+TCCAuGgAwIBAgIJAL1GWG15d5lpMA0GCSqGSIb3DQEBCwUAMIGSMQswCQYD
    VQQGEwJTRTERMA8GA1UECAwIQmxla2luZ2UxEzARBgNVBAcMCkthcmxza3JvbmEx
    IzAhBgNVBAoMGkJsZWtpbmdlIFRla25pc2thIEhvZ3Nrb2xhMRQwEgYDVQQDDAtC
    VEggQ0EgUm9vdDEgMB4GCSqGSIb3DQEJARYRaG9zdG1hc3RlckBidGguc2UwHhcN
    MTUwMzE3MTQxODU5WhcNMzUwMzEyMTQxODU5WjCBkjELMAkGA1UEBhMCU0UxETAP
    BgNVBAgMCEJsZWtpbmdlMRMwEQYDVQQHDApLYXJsc2tyb25hMSMwIQYDVQQKDBpC
    bGVraW5nZSBUZWtuaXNrYSBIb2dza29sYTEUMBIGA1UEAwwLQlRIIENBIFJvb3Qx
    IDAeBgkqhkiG9w0BCQEWEWhvc3RtYXN0ZXJAYnRoLnNlMIIBIjANBgkqhkiG9w0B
    AQEFAAOCAQ8AMIIBCgKCAQEA1OTVBSi/gbtr6WD5J72bxEmWYyOiB+Go2PoRwxXM
    H0gAzRgAazWbdR+XAYCb0Ilp809+bCmac1Vj1zK7JWc3pnZcjC1mJePtuPCvhOG8
    Hr+Yf+YxByXZ3oM4T9wYO54SDdEjJTqFhNubKxYhJMEsd/eRMtErRYaYvH1J0Qoh
    0YHoPb5Lu975yNwwsyQnUBqOMvTvs8kMQkZil/54CMGQvOm3O0wA+t8CfZKfuTqG
    nG1SpK74QiRDg/6cfWF61VzKqIMwm1E5wxY0by52KiaSw8AWIpSqW8Pahtpgg2g8
    y7vZV/BaWAr1QEC72aiCxZD9H2U0B1T9J+tOsitLjRrB1wIDAQABo1AwTjAdBgNV
    HQ4EFgQU8IhKO++rllE2RANJYTszlxvj3s8wHwYDVR0jBBgwFoAU8IhKO++rllE2
    RANJYTszlxvj3s8wDAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEAeHVD
    fgHVqnOySrh2p9qFTJtbEOQ33zP/NjmhmVQJSZrVSIG+nuV/IhyR4hUJXNLZI7g/
    zp2IHFbYvqI69JZIsFrNetSyZFIOSQzV/A4z7eNK3YfwY6E/SKdus9aMywJvvc2c
    dwoAAbDF3uGmlCzcqu/VN5uUVcluBEErShakyFsXNhFEjZhi3ddBL1jfgvwFlQa8
    zEOloNE0N9hW1dd7H3sySdxtjgmUfMj6jIIt1U6jTmuUwSgYM5E0+9rlB4pmuSJJ
    gYXLGh4tc09mk4qlyA6jXtECTXSkzd/4pLldmPcfEvibXUf7BNoKuuJALz3/HvGm
    RU7HjJekMXKcz9wKqg==
    -----END CERTIFICATE-----" >> /home/pi/eduroam_bth.pem`

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
