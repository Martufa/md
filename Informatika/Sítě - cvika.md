#### Spanning Tree Protocol 
- při problematice možné smyčky; zdroj je označený jako ROOT a cokoli, co by mohlo zapříčinit smyčku je zablokováno
- příklad protokolu na druhé vrstvě

Switch nemusí nutně vědět, kde se nachází cílový adresát, může broadcastovat všem na podsíti

#### Ethernetový rámec 
- dst (MAC) (48bit?)
- src (MAC)
- VLAN tag (1 - 4096) - spolu se baví jen ty části pod switchem, které mají stejný tag, odděluje světy, nebaví se mezi sebou navzájem

VLAN je konstrukt na úrovni L2 (nemá ip a tak), ale můžeme na úrovni L3 vytvořit virtuální rozhraní, které IP má
Aby na sebe IP adresy z L3 viděly, nesmí být stejné, ale musí být ve stejném rozsahu
192.168.x.y
x - VLAN (ne až moc vysoká)
y - identifikátor
Maska, doporučení 255.255.255.0

##### Cisco help
Tab (pokud nedoplní po 2 písmenách, něco je špatně)
?
šipka nahoru

#### Trunk


- na každém switchi 2 vlany, stejné, tag stejný, aby se viděli navzájem
## (L3)

Adresujeme pomocí IP adres síťové rozhraní
- wifi, bluetooth, rádio, síťovka přes usb, loop
## Transportní vrstva (L4)
Nejdůležitější služba - adresace procesů
protože bychom na stroji mohli mít jenom nějaký omezený počet aplikací, ke kterým se připojt
data se přenášejí na libovolné vrstvě
meziprocesová adresace v síti
výjimka oddělení síťových vrstev je firewall

Síťový stack (aplikační, transportní, l3)
127.0.0.1 - home, moje zařízení

IP :Port (adresa procesu, 16bitový číslo)
na L4 řeším i packetizaci

první rozhraní mezi L7 - aplikační vrstvou - a zbytkem sítě
(L5 (html pod https) - prezentační, L6 (tls pod https) - relační se dneska moc neuvažují) - rozdíl mezi ISO/OSI a TCP/IP

TCP UDP protokoly
UDP nikdy nebyl standardizovaný, ale stojí na něm nějaká ze základních složek internetu 

**UDP** - adresuje zdrojový a cílový port (+ přidá length a checksum, ne nutné)
**TCP** - zajišťuje spojovanou a spolehlivou službu - procesy o sobě vzájemně ví a jsou potvrzené; handshake; packety přichází a ve správném pořadí - TCP čísluje packety, potvrzuje jejich doručení - pozitivní potvrzení - zpátky vracím přijatý payload + 1 ("očekávám následující, přijal jsem vše až do bodu následujícího") - ACK = n+1

zajišťuji vyšším vrstvám, že packety pošlu ve správném pořadí - mám odesílací a přijímací buffer (okno/window)

##### Flow control
posílám jen tolik, kolik je druhý schopný zpracovat - v handshaku se vyměňuje velikost okna, používá se menší, je možné ji dynamicky zvětšovat

Efektivita přenosu - v co nejkratším době posílám co nejvíc co největších packetů
ethernet - max velikost packetu 1500 bajtů

Roundtrip time - cesta tam a zpátky

Proč jsou packety malé?
- Síťové vybavení má málo paměti
- Retransmise, pokud je linka plná, nemůžu přesouvat nic dalšího
Duplexní - zároveň vysílá, zároveň přijímá, 2 fronty

Time division multiplexing - čím víc lidí na wifi, tím kratší čas na odesílání packetů

##### Congestion control
TCP se snaží nezahlcovat síťové linky
Packety se odesílají do sítě rychlostí síťové karty
TCP není úplně 100% fér

![[Pasted image 20240409164607.png]]

##### Quality of service
- můžu vzít end-to-end přenos a garantovat parametry (např. latence)
- fail1: máme tři bity na značkování provozu (8 tříd, jenom, lol, málo)
- fail2: je to až na L4, mělo by to být dřív

icmp - request, ping, pinguju L3 ip adresu (např 8888, Google DNS, domain name service, ~ 15 DNS serverů, podvržené DNS odpovědi na subsítích, Starbucks, RJ, Kafec...)
FQDN - fully quallified domain names (např. www.google.com), tohle nepoužívám pro ping, protože je to příliš dlouhé, proto používám IP adresy

Na portu **53** služba musí být služba DNS (UDP)

80 - číslo portu pro http
443 - číslo portu pro https
### Poznámky
Maximální velikost packetů už od L2
Na L3 musíme mít přidělenou IP adresu z rozsahu 10.0.0.0/8 - privátní adresní rozsah
192.168.0.0/16 - přiděluju sám
172.16.0.0/12 - přiděluju sám

Co není unikátní, router nesmí routovat, musí zahazovat - privátní by se neměly routovat mimo síť
Při handshaku by se muselo vyhodit, co je nakonfigurované privátně, ALE! NAT (na L3/L4)

portů je 2^16

ethtool eth0
ip address

Length - velikost packetu na L1, na wiru (zde na ethernetu, největší zde 1514 bytů, ethernetová hlavička má MTU 1500 + ethernetová hlavička 14 bytů)
info - source port -> dest port
##### Řídící bity
	SYN synchronize
	ACK acknowledge
	FIN finalize
	PSH push
	RST reset (reset spojení)
	URG urgent

Win = moje velikost okna (v bytech), narveme do okna tak 20 packetů, používá se menší z obou 64 240 a 28 960
Seq = sekvenční číslo (používáme relativní, ne raw)
Len = velikost payloadu
MSS = maximum segment size (payload + tcp hlavička) musí se vlést do maximum transfer unit
zachycení od epochy, zachycení od posledního přijatého (pro debugging)

ack je 33 bitů informace, piggybackuju
fin
fin,ack
ack

přes terminál jsme uploadovali na adresu 
pošle http post příkaz, ale packet neplním úplně
224 bytů (5. packet) - má jako příznak push, na L7 stavím zprávu HTTP POST/ HTTP1.1 data
pokud server zprávě rozumí, mohu přidat push -> rovnou expedovat aplikační vrstvě na L7; pokud úspěšně přijato, zpět se vrací ACK = 225 (tedy přijatá velikost + 1).
přijde-li mi push, vracím stejně s pushem HTTP 100 CONtinue, čímž říkám, že očekávám data, jelikož má velikost 25, tak se od původního klienta vrací ACK = 26.

Máme potvrzené všechny packety předtím
9. packet začínám posílat text (pošleme 5, než máme další push acknowledged)
payload 1448 bytů, protože máme jenom velikost hlaviček

rychlost přenosu dat = objem dat / čas přenosu dat
čas - od přesunu prvního packetu s obsahem až po poslední ack
prohlížeč drží proces, pokud by ho chtěl uživatel znovu využít, curl, aby se choval mravně, musí spojení uzavřít

retransmise - k výpadku nedošlo, vidíme jen duplicitní ack, protože nedošlo k přeposílání žádných dat
Tři třídy problémů
1. Out of order packet - něco ještě nepřišlo, žádám znovu, zvětšuju velikost okna (proto vím, že je to out of order, pokud čistě vypadne packet, nesignalizuju zvětšení okna, duplicitní ack -> retransmise)
2. duplikovaný ack
3. retransmise

destination ip address - co to sakra je?
tcp se nedalo použít, protože nebyl handshake (tcp je proces to proces komunikace, na broadcastu není možné)
co u udp popisuje length - jsou větší než u tcp
jumbo frames? větší packety, protože chci vyšší efektivitu přenosu, ale musíme mít dostatečně velké buffery
max packet 64kb, OSka snižují samy, 
graf nám říká, kolik jsme za vteřinu přijali
~ 70Mb/s, fullHD vido, (nekompresované video má ~1Gb/s)

25 burstů za vteřinu - jednotlivé snímky videa
1\*10^6 bitů / ms ==  \* 1000 protože ms -> 10^9 bitů za sekundu -> 1 Gb/s == po strop naplněná linka v době peaku
limituje mě procesor a síťový interface (spíš to druhé), u UDPka, TCP brzdí přes okna
