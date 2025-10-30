# AjutorTemePCLP

## Set-up la checker

Vom instala de pe Moodle arhiva in care se afla checkerul temei, care este `check_chocolate_rain.zip`

Folosim comanda `unzip check_chocolate_rain.zip` dupa ce am descarcat arhiva in linia de comanda, ca sa avem acces la fisierle ei.

Vom rula comanda `sudo ./install` pentru a instala **dependentele** checkerului, ca acesta sa functioneze normal si sa nu dea erori.

Dupa ce instalam dependentele, vom rula comanda `./check --help`

### Eroare posibila

Daca apare o eroare care seamana cu urmatoarea:
```py
./check
Traceback (most recent call last):
  File "/home/andre1ut/Desktop/PCLP/./check", line 4, in <module>
    from check_utils.checks import checker_run
  File "/home/andre1ut/Desktop/PCLP/check_utils/checks.py", line 9, in <module>
    from .parser import get_config
  File "/home/andre1ut/Desktop/PCLP/check_utils/parser.py", line 8, in <module>
    import recordclass
ModuleNotFoundError: No module named 'recordclass'
```
Asta inseamna ca nu s-au instalat niste librari de python pe sistem, si trebuie sa le instalam manual folosind urmatoarea comanda:

`pip3 install <librarie> --break-system-packages`, unde `break-system-packages` ii spune sistemului sa instaleze libraria inafara unui virtual environment (multa vrajeala)

In cazul erorii de mai sus vom folosi comanda:
`pip3 install recordclass --break-system-packages`

Si asa ar trebui sa rulam comanda pentru fiecare librarie pentru care apare aceasta eroare.

## Makefile

Dupa cum vedem in Tema0, trebuie sa avem in arhiva zip pe care o trimitem, scriptul de c care contine rezolvarea problemei, un Makefile care contine niste reguli, si un README care sa contina descrierea rezolvarii.

Makefile ul are 3 exemple, dar aici este primul exemplu de Makefile ultrasimplificat:

```
# Copyright PCLP Team, 2025

CC=gcc
CFLAGS=-Wall -Wextra -std=c99

# binar1, binar2 si binar3 reprezinta numele fisierelor compilate care provin de la scripturile de c
TARGETS=<binar1> <binar2> <binar3>

build: $(TARGETS)

<binarX>: <binarX>.c
	$(CC) $(CFLAGS) <binarX>.c -o <binarX>

# cele doua linii de mai sus vor fi adaugate pentru fiecare script de c individual
# daca am doua scripturi (asd.c si caca.c), voi face urmatorul lucru
# asd: asd.c
#   $(CC) $(CFLAGS) asd.c -o asd
# caca: caca.c
# 	$(CC) $(CFLAGS) caca.c -o caca

# Inlocuim in secventa de mai jos fiecare spatiu cu ce trebuie (smr de mint), si dupa salvam Makefile
pack:
	zip -FSr <grupa>_<NumePrenume>_Tema<X>.zip README Makefile *.c *.h

clean:
	rm -f $(TARGETS)

.PHONY: pack clean
```

Liniile care incep cu **#** sunt comentarii si ar trebui sterse inainte sa salvam `Makefile`.

## Utilizare Checker

Daca vrem sa verificam toata tema, vom folosi comanda
`./check`
Daca vrem sa verificam doar un task din tema, vom folosi comanda
`./check --task <numetask>`

## Submitere Tema

Cand am terminat tema si vrem sa o urcam pe platforma, folosim comanda:
`make pack` (Trebuie ca Makefile sa fie creat)

**!!!Tineti minte sa aveti in arhiva Makefile, scripturile de c si README!!!**