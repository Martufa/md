33. if1
```
for JMENO in *; do if echo $JMENO | grep smaz >/dev/null; then rm $JMENO; elif grep smaz $JMENO >/dev/null; then mkdir -p Trash && mv $JMENO Trash/$JMENO; elif grep text $JMENO >/dev/null; then mv $JMENO $JMENO.txt;fi;done
```

34. whr
*do filu se jménem zrovna přihlášeného uživatele hoď konkrétní info o něm*
```
who | (while read NAME IDK DATE TIME THIS REST; do echo $THIS >> /home/xkozlov2/pv004lab/ukol_whr_d890f/$NAME; done)
```

35. te1
*pokud mají soubory právo na spuštění, přidej k nim .sh*
```
for FILE in *; do if [ -x $FILE ]; then mv $FILE $FILE.sh; fi; done
```
36. nastavení skriptovacího prostředí - ez

37. sk1
```
#!/bin/bash

echo -e "Ahoj světe!\n\nTvůj b9b90941"
```

38. cap
```
#!/bin/bash
case "${1}" in 
        verze|-v) echo "verze 936"
        ;;
	celkem|-a) if [ -f "${2}" ]; then wc -l < "${2}"; else echo "tak to se nepovedlo" >&2 && exit 1; fi
        ;;
	vybrane|-s) if [ -f "${2}" ] && [ -n "${3}" ]; then  grep "${3}" "${2}" |wc -l; else echo "vyber pořádně p>
        ;;
	nevybrane|-r) if [ -f "${2}" ] && [ -n "${3}" ]; then  grep -v "${3}" "${2}" |wc -l; else echo "eeeeh!" >&>
        ;;
	*) echo "lolz" >&2 && exit 1
        ;;
esac
```

39. nup - numerické porovnávání
```
#!/bin/bash  
if [ -z $1 ] || [ -z $2 ] || [ ! -z $3 ]; then echo "22b59" >&2 && exit 1; fi 
[ $2 -eq $2 ] 2> /dev/null || exit 1 
[ -e $1 ] || exit 1  

FSIZE=$(stat -c %s $1) 
if [ $FSIZE -ge $2 ]; then echo $FSIZE ; else echo "0"; fi
```

40. fo2 - expanze proměnných a sufixy
```
#!/bin/bash
for JMENO
do 
       mv $JMENO ${JMENO%.d15}.7e2
done
```

41. poa - počet pozičních argumentů získáš přes $#
```
#!/bin/bash

if [ ! $# -eq 5 ]; then echo "jádydááá" >&2; exit 1;fi

echo "ok 2a56dee4ba673cb70cce"
```

42. pjs
```
#!/bin/bash

JMENO=$(basename "$0")

if [ "$JMENO" == "vytvorit" ]; then echo "Skript 9cb19 bude vytvářet.";fi
if [ "$JMENO" == "smazat" ]; then echo "Skript 9cb19 bude mazat."; fi
```