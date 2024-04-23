#### Domácí úkoly
git pull upstream main
git push
git switch -c hwNN
git push --set-upstream origin hwNN

#### Odevzdávání
```
/home/kontr/odevzdavam pb071 hw02 nanecisto
```
#### Semináře - help

**stáhni zadání:**
git status
git switch main
git pull upstream seminar-NN
git push

**hoď lokální na remote repo:**
git push --set-upstream origin seminar-NN

#### Valgrind
kontruluje za běhu (possible problém)
gcc -g file.c (-g doplní debugovací značky)
==valgrind  --leak-check=full --show-reachable=yes --track-origins=yes ./file.c==


TESTUJ NA AISE (rozbité knihovny, může leakovat třeba printf)
Na paměť nepoužíváme ASSERTY, protože nedostatek paměti není naše chyba
DON'T EXIT v Cčku

#### Fce - soubory
- ftell = aktuální pozice
- fseek(file, o kolik, odkud) = skočí na offset od současné pozice
- rewind = vrátí se na normální

fgetc
fread
fscanf

fputc
fprintf
fwrite

gcc (do assembleru) (čtyři úrovně optimalizace)
gcc -S -00 source.c (případně: -o output.s)


__attribute__((unused))