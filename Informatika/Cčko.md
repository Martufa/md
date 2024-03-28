
#### Semináře
git status
git switch main
git pull upstream seminar-NN
git push

#### Valgrind
kontruluje za běhu (possible problém)
gcc -g file.c (-g doplní debugovací značky)
==valgrind  --leak-check=full --show-reachable=yes --track-origins=yes ./file.c==
