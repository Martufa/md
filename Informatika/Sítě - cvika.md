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