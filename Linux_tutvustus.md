# 🐧 Sissejuhatus Linuxi – algajale arusaadavalt

##  Eesmärk

See dokument aitab sul mõista, **kuidas Linux töötab**, millised on erinevad käsud ja **kuidas see erineb Windowsist**. Kui sa pole kunagi Linuxi kasutanud, siis see on just sulle!

---

##  Mis on Linux?

Linux on **operatsioonisüsteem** nagu Windows või macOS, aga:
- **avatud lähtekoodiga** (igaüks saab vaadata ja muuta, kuidas see töötab);
- **väga paindlik ja turvaline** (seetõttu kasutatakse seda serverites ja robootikas);
- **põhineb UNIX-il**, mis on üks esimesi operatsioonisüsteeme.

---

##  Kuidas Linux "mõtleb"?

Linuxil on kaks peamist tasandit:

### 1.  Kernelitasand – süsteemi süda

- Kernel haldab **riistvara**: protsessor, mälu, kettad, võrk.
- Kasutajad ja programmid suhtlevad kerneliga kaudselt.

💡 **Näide:** kui käivitad käsu `cp`, et kopeerida faili, siis tegelik töö teeb ära kernel.

### 2.  Kasutajatasand – see, mida sa näed ja kasutad

- Käsureal käskude sisestamine (`ls`, `cd`, `nano` jne)
- Programmid töötavad "kasutaja ruumis"
- Ei pääse otse kernelini (v.a `sudo` abil)

---

##  Failisüsteem erineb Windowsist

| Windows                | Linux                    |
|------------------------|--------------------------|
| C:\Users\Student     | /home/student            |
| D:\failid\dokumendid | /mnt/d/failid/dokumendid |
| .exe failid            | Käivitusõigusega failid  |

Linuxis **pole draive nagu C: või D:** – kõik on **üks suur puulaadne struktuur**.

---
##  Mis vahe on Linuxil, Ubuntul ja Unixil?

### Unix
- 1970ndatel loodud operatsioonisüsteem, mille ideedel põhineb kogu Linuxi ökosüsteem.
- Suletud lähtekoodiga, kommertslik (nt AIX, Solaris).

### Linux
- Unixiga **ühilduv** operatsioonisüsteem, aga **avatud lähtekoodiga**.
- Kernel (Linuxi süda) on universaalne, ent selle ümber on palju eri maitseid.

### Ubuntu ja teised distributsioonid (distrod)

| Distro       | Eesmärk ja omadused                                  |
|--------------|-------------------------------------------------------|
| **Ubuntu**   | Kasutajasõbralik, populaarne töölaua- ja serverikasutuses |
| Debian       | Ubuntu "ema", stabiilne ja konservatiivne            |
| Fedora       | Uuemate tehnoloogiate testplatvorm, seotud Red Hatiga|
| Arch Linux   | Minimalistlik ja täielikult kohandatav               |
| Raspberry Pi OS | Kerge ja Raspberry Pi jaoks mõeldud distro        |

💡 *Kõik need jagavad Linuxi kerneli, aga erinevad tööriistade, paigaldusviiside ja vaikeseadete poolest.*

---

##  Mis on APT ja muud pakendihaldurid?

Linuxis installitakse tarkvara **pakettidena**. Selleks kasutatakse **pakendihaldureid**, mis aitavad paigaldada, värskendada ja hallata tarkvara.

### APT – Advanced Package Tool

- Kasutatakse **Debianipõhistes** distributsioonides nagu Ubuntu.
- Käskude näited:
```bash
sudo apt update       # Uuenda pakettide nimekiri
sudo apt install nano # Paigalda uus programm
```

### Muud pakendihaldurid

| Süsteem         | Pakendihaldur   | Kasutatakse distrodes          |
|------------------|------------------|--------------------------------|
| `apt`            | Debian, Ubuntu   | `sudo apt install`             |
| `dnf`            | Fedora, RHEL     | `sudo dnf install`             |
| `pacman`         | Arch Linux       | `sudo pacman -S`               |
| `snap`, `flatpak`| Universaalsed    | Mitme distro vahel jagatavad   |

💡 *Kuigi käsud erinevad, teevad kõik need sama asja – toovad tarkvara internetist ja paigaldavad selle süsteemi.*

---

##  Kasutajad ja õigused

Linuxis iga kasutaja:
- kuulub **gruppi** (nt `student`, `sudo`);
- ei tohi muuta teiste faile ilma loata;
- võib saada **ajutiselt kõrgemad õigused** käsuga `sudo`.

| Roll         | Õigused                  |
|--------------|--------------------------|
| Tavaline     | Saab käivitada programme, muuta enda faile |
| Root / sudo  | Saab muuta süsteemi, paigaldada tarkvara   |

---

##  Näide: kasutaja vs kernelitaseme käsk

| Käsk                | Tase     | Kirjeldus                       | Vaja `sudo`? |
|---------------------|----------|----------------------------------|--------------|
| `cd /home`          | Kasutaja | Liigub kataloogi                | ❌           |
| `ls -l`             | Kasutaja | Näitab failide nimekirja        | ❌           |
| `reboot`            | Kernel   | Taaskäivitab süsteemi           | ✅           |
| `apt install`       | Kernel   | Paigaldab tarkvara              | ✅           |

---

##  Kuidas suhelda Linuxiga?

Linuxis kasutatakse sageli **käsurida** (CLI), mitte graafilist akent.

```bash
# Liigu oma kausta ja kuva failid
cd /home/student
ls -lah
```

*Käsurida annab sulle rohkem kontrolli kui Windowsi „hiireklõpsud“.*

---

##  Näide: failide otsimine

### Windows:
- Otsid kaustast läbi File Exploreriga või kasutad otsinguakent

### Linux:
```bash
find . -name "*.txt"
grep "otsitav_sõna" fail.txt
```

---

##  Turvalisus

Linux:
- Iga programm töötab oma õiguste piires.
- Süsteemifailide muutmiseks on vaja `sudo`.
- Vähem viirusi ja pahavara (vähem administraatori õigusi).

Windows:
- Paljud programmid töötavad administraatori õigustes.
- Rohkem pahavara sihib seda platvormi.

---

##  Kokkuvõte

- **Linux on nagu tööriistakast – saad rohkem kontrolli.**
- **Failisüsteem on teistsugune, aga loogiline.**
- **Käsurea õppimine annab sulle eelise robootikas, serverites ja programmeerimises.**

---

##  Edasi lugemiseks

- [https://linuxjourney.com](https://linuxjourney.com)
- `man <käsk>` – iga käsu kohta juhend terminalis
- Proovi käske `--help` laiendiga (nt `ls --help`)
