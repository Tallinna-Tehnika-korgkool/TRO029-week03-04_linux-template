# Week 3-4: Linuxi käsud ROS 2 konteineris

## Õpieesmärgid

Selles peatükis saad tuttavaks põhiliste Linuxi käskudega ning õpid neid kasutama ROS 2 konteineris (Dockeris).
Pärast peatüki läbimist oskad:

- navigeerida Linuxi failisüsteemis;
- luua ja kustutada faile ning katalooge;
- muuta failiõigusi ja mõista, miks need olulised on;
- hallata protsesse (käivitada, vaadata, lõpetada);
- otsida ja filtreerida käsurea väljundit.

> **NB!** Kõik harjutused tee kaustas `/workspace`, sest see on püsiv kaust, mis jääb alles ka pärast konteineri uuesti käivitamist.

---

## Linuxi käsud koos näidetega

### Failisüsteemis liikumine

**`pwd` - näita oma asukohta**

See käsk näitab, millises kaustas sa hetkel asud. See on kasulik, kui oled failisüsteemis ära eksinud või tahad veenduda, et oled õiges kohas enne käskude andmist.

```bash
pwd
# /workspace
```

**`ls`, `ls -l` - loetle faile ja katalooge**

`ls` on üks enimkasutatud käske, mis loetleb praeguse kausta sisu. Lipuga `-l` saad detailsema vaate, mis näitab failiõigusi, omanikku, suurust ja muutmise kuupäeva.

```bash
ls
# harjutus  README.md

ls -l
# drwxr-xr-x 2 root root 4096 Sep 29 12:00 harjutus
# -rw-r--r-- 1 root root  123 Sep 29 12:01 README.md
```

**`cd` - liigu kataloogidesse**

`cd` (change directory) abil saad liikuda teistesse kaustadesse. `cd ..` viib sind ühe taseme võrra ülespoole.

```bash
cd harjutus
pwd
# /workspace/harjutus

cd ..
pwd
# /workspace
```

---

### Failide loomine ja vaatamine

**`touch`, `echo`, `cat` - loo ja näita faile**

- `touch` loob tühja faili. Kui fail on juba olemas, uuendab see selle ajatemplit.
- `echo` kirjutab teksti standardsisendisse. Koos `>` operaatoriga saad selle suunata faili.
- `cat` näitab faili sisu.

```bash
touch test.txt
echo "Tere tulemast!" > tervitus.txt
cat tervitus.txt
# Tere tulemast!
```

---

### Kataloogide ja failide haldus

**`mkdir`, `rm`, `rmdir` - loo ja kustuta**

- `mkdir` loob uue kataloogi.
- `rm` kustutab faile. Ole ettevaatlik, sest kustutatud faile ei saa lihtsalt taastada!
- `rmdir` kustutab tühje katalooge. Et kustutada kataloogi koos sisuga, kasuta `rm -r`.

```bash
mkdir minu_kaust
ls
# harjutus  minu_kaust  tervitus.txt  test.txt

rm test.txt
ls
# harjutus  minu_kaust  tervitus.txt

rmdir minu_kaust
ls
# harjutus  tervitus.txt
```

---

### Failiõigused ja turvalisus

Linuxis määravad failiõigused, kes saab lugeda, kirjutada või käivitada faili.

**`chmod`, `ls -l` - muuda ja vaata õigusi**

`chmod` abil saad muuta failiõigusi. `ls -l` näitab neid. Esimene märk näitab, kas tegu on kausta (`d`) või failiga (`-`). Järgmised 9 märki on kolm gruppi kolmest: omanik, grupp ja teised. `r` on lugemis-, `w` on kirjutamis- ja `x` on käivitusõigus.

Numbritega on lihtsam: 4 (read), 2 (write), 1 (execute). Liida numbrid kokku, et saada soovitud kombinatsioon. Näiteks `chmod 600 fail.txt` annab omanikule lugemis- ja kirjutamisõiguse (4+2=6) ning grupile ja teistele mitte ühtegi (0).

```bash
ls -l tervitus.txt
# -rw-r--r-- 1 root root 15 Sep 29 12:05 tervitus.txt

chmod 600 tervitus.txt
ls -l tervitus.txt
# -rw------- 1 root root 15 Sep 29 12:05 tervitus.txt
```

---

### Protsesside haldamine

**`ps aux`, `kill` - vaata ja lõpeta protsesse**

- `ps aux` näitab kõiki käimasolevaid protsesse. See on kasulik, kui soovid näha, mis süsteemis toimub või leida protsessi ID (PID).
- `kill` lõpetab protsessi selle PID-i abil.

```bash
sleep 120 &
# [1] 42

ps aux | grep sleep
# root        42  0.0  0.0   2600   896 pts/0    S    12:10   0:00 sleep 120

kill 42
ps aux | grep sleep
# (tühjus - protsess on lõpetatud)
```

---

### Teksti otsimine ja filtreerimine

**`grep`, `|` (pipe) - otsi ja filtreeri**

- `grep` otsib tekstist mustreid.
- `|` (pipe) on võimas tööriist, mis suunab ühe käsu väljundi teise käsu sisendiks. See on väga kasulik keerukamate operatsioonide jaoks.

```bash
echo -e "üks
kaks
kolm" > numbrid.txt
cat numbrid.txt | grep kolm
# kolm
```

**Protsesside otsimine:**

```bash
ps aux | grep bash
# root      100  0.0  0.1  10000  2000 pts/0    Ss   12:12   0:00 bash
```

---

## Harjutus: loo ja halda faile `/workspace` kaustas

1. Liigu `/workspace` kausta ja loo sinna alamkataloog nimega `harjutus`.
2. Loo sinna fail `minu_fail.txt` ja kirjuta sinna mõni tekst.
3. Muuda faili õigused nii, et ainult sina saad seda lugeda ja kirjutada.
4. Käivita taustal käsk `sleep 120 &` ning lõpeta see `kill` abil.
5. Loo fail `kasutatud_kasud.txt`, kuhu kirja paned kõik käsud, mida harjutuse käigus kasutasid.
6. Kontrolli `ls -l` abil, et failide õigused ja sisu on korrektsed.

---

## Esitamise kord

Harjutuse edukaks esitamiseks **pead töötama oma isiklikus GitHub Classroomi repos**, mis on loodud selle nädala jaoks.

1.  **Ava ülesande link Moodle'ist:**
    - Mine kursuse Moodle'i lehele.
    - Leia sealt selle nädala (Week 03-04) ülesande juurest link oma isikliku GitHub Classroomi repositooriumi loomiseks.

2.  **Klooni enda isiklik repo GitHubist**, mille nimi sisaldab sinu GitHubi kasutajanime.
    Näide:
    ```bash
    git clone https://github.com/Tallinna-Tehnika-korgkool/TRO029-week03-04_linux-<sinu_kasutajanimi>
    ```

3.  **Tee kõik ülesanded selles kloonitud repos.**

4.  **Lisa ja `commit`'i oma muudatused** (nt. `minu_fail.txt`, `kasutatud_kasud.txt`).
    ```bash
    git add .
    git commit -m "docs: Complete week 3-4 exercise"
    git push
    ```

5.  Kui `push` on tehtud, käivituvad **automaatsed testid** (GitHub Actions) sinu repo **Actions** vahekaardil.
    - ✅ **Roheline** ✔️ tähendab, et kõik on korras.
    - ❌ **Punane** ✖️ tähendab, et midagi on puudu või valesti – paranda ja tee uus `commit` ja `push`.

> **NB!** Kui töötad väljaspool oma isiklikku Classroom repo't, siis testid ei tööta ja harjutust ei loeta esitatuks.
