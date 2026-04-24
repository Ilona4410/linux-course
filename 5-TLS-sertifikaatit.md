# TLS Sertifikaatit

## Johdanto

## DNS

- Asensin tunnilla dig-työkalun komennolla sudo apt install dnsutils
- Testasin, että DNS toimii oiken ja domain osoittaa oikeaan palvelimeen


  ```
  linuxuser@test026:~$ dig test026.linuxkurssi.xyz

  ; <<>> DiG 9.20.21-1~deb13u1-Debian <<>> test026.linuxkurssi.xyz
  ;; global options: +cmd
  ;; Got answer:
  ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62844
  ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

  ;; OPT PSEUDOSECTION:
  ; EDNS: version: 0, flags:; udp: 65494
  ;; QUESTION SECTION:
  ;test026.linuxkurssi.xyz.	IN	A

  ;; ANSWER SECTION:
  test026.linuxkurssi.xyz. 1799	IN	A	65.52.72.83

  ;; Query time: 40 msec
  ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
  ;; WHEN: Fri Apr 24 14:03:12 UTC 2026
  ;; MSG SIZE  rcvd: 68
  ```

## Yhteenveto

## Lähteet
