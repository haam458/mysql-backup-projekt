# MySQL andmebaasi varukoopia ja taastamise projekt 

## Projekti eesmärk

Selle projekti eesmärk on kontrollitud keskkonnas läbi viia MySQL andmebaasi varundamise ja taastamise protsess.

Mille käigus:

- luuakse MySQL andmebaas
- tehakse sellest varukoopia
- salvestatakse varukoopia GitHubi
- taastatakse andmebaas varukoopia põhjal

## Kasutatud tehnoloogiad

- Ubuntu Server VM (VirtualBox keskkonnas)
- MySQL andmebaasiteenus
- Git versioonihaldus
- GitHub veebikeskkond

## Andmebaasi loomine

Kõigepealt logitakse MySQL serverisse:

```bash
sudo mysql
```
Seejärel luuakse andmebaas:

```sql
CREATE DATABASE testdb;
```
See loob tühja andmebaasi nimega `testdb`, mida kasutatakse edasistes sammudes.

Andmebaasi sisse loodi tabel:

```sql
CREATE TABLE `inimesed` (
  `id` int NOT NULL AUTO_INCREMENT,
  `nimi` varchar(50) DEFULT NULL,
PRIMERY KEY (`id`)
);
```
Tabel `inimesed` salvestab kasutajate andmeid.

## Andmebaasi varukoopia tegemine

Andmebaasist tehakse varukoopia käsuga:

```bash
sudo mysqldump testdb > backup.sql
```
Selle tulemusel luuakse fail `backup.sql`, mis sisaldab kogu andmebaasi struktuuri ja andmeid.

## Varukoopia lisamine GitHubi

Varukoopia lisatakse Git versioonihaldusesse ja saadetakse GitHubi:

```bash
git add backup.sql
git commit -m "Lisatud MySQL varukoopia"
git push
```
Fail on nüüd kättesaadav GitHubi repositooriumis.

## Andmebaasi taastamine

Varukoopia taastatakse andmebaasi käsuga:

```bash
sudo mysql testdb < backup.sql
```
See impordib kõik tabelid ja andmed tagasi andmebaasi.

## Kontrollimine

Kontrollitakse, kas taastamine õnnestus:

```bash
sudo mysql
```
MySQL-i sees:

```sql
USE testdb;
SHOW TABLES;
```
Kui tabelid on nähtavad siis see kinnitab edukat taastamist.

## Põhimõisted

**Andmebaas (Database):**struktuur, kuhu salvestatakse andmed. Selles töös kasutati `testdb` andmebaasi andmete hoidmiseks.

**MySQL:**relatsiooniline andmebaasihaldur. Kasutati andmebaasi loomiseks, haldamiseks ja taastamiseks.

**Varukoopia (Backup):**andmete koopia, mis võimaldab taastamist. Selles töös loodi fail `backup.sql`.

**Restore:**varukoopia tagasi laadimine andmebaasi.

**Git:**versioonihaldussüsteem, mida kasutati failide jälgimiseks.

**GitHub:**veebikeskkond Git repositooriumide hoidmiseks.

**VM (Virtual Machine):**virtuaalne arvuti, kus kogu süsteem töötas.

**mysqldump:**tööriist andmebaasi varundamiseks.

## Kontrolli eeldused

- MySQL teenus pead töötama
- kasutajal peavad olema sudo õigused
- andmebaas `testdb` peab olemas olema või loodud
- `backup.sql` fail peab olemas olema enne taastamist

