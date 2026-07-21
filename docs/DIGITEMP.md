# DigiTemp, DS9097 a měření teploty

## Jak Brauanlage získává teplotu

Brauanlage podle dochovaných návodů nekomunikuje s 1-Wire sběrnicí přímo. Spouští externí program DigiTemp a čte jeho výstupní log.

Typická konfigurace:

```text
Program: digitemp_DS9097.exe
Log soubor: log
Port: COM1 až COM4
```

Některé návody uvádějí jméno programu bez přípony:

```text
digitemp_DS9097
```

## Hardware

Původní řešení používá:

- sériový port RS-232,
- adaptér DS9097,
- 1-Wire teplotní čidlo DS18B20 nebo příbuzný typ,
- případně více čidel na jedné sběrnici.

USB varianta může fungovat, ale vyžaduje kompatibilní převodník, ovladač a případně upravený způsob vytváření logu.

## Doporučený diagnostický postup

Nejprve zprovozněte DigiTemp samostatně, mimo Brauanlage.

1. Ověřte COM port ve Správci zařízení.
2. Spusťte detekci 1-Wire adaptéru.
3. Ověřte, že DigiTemp najde ROM adresu čidla.
4. Nechte DigiTemp vypsat jednu teplotu do konzole.
5. Ověřte vytvoření log souboru.
6. Teprve potom nastavte stejné jméno programu a logu v Brauanlage.

## Co kontrolovat, když se teplota nezobrazí

- nesprávný COM port,
- jiný typ adaptéru než DS9097,
- chybějící DigiTemp EXE,
- EXE není ve složce očekávané programem,
- log má jiné jméno nebo příponu,
- log používá desetinnou čárku místo tečky,
- jiný formát řádku než program očekává,
- čidlo není nalezeno,
- přerušená nebo příliš dlouhá 1-Wire sběrnice,
- chybějící zem nebo napájení čidla,
- program nemá právo zapisovat log.

## Čekání při startu

Dochované české návody uvádějí, že hledání 1-Wire čidla může po potvrzení konfigurace trvat přibližně deset sekund. Pokud je vše správně, hodnota teploty se objeví v zeleném poli v pravé horní části hlavní obrazovky.

## Log jako integrační rozhraní

Protože Brauanlage pravděpodobně čte jednoduchý textový soubor, je možné původní hardware nahradit moderním zařízením, pokud bude pravidelně generovat přesně stejný formát logu.

Možné moderní zdroje:

- Arduino s DS18B20,
- ESP32,
- Raspberry Pi,
- USB 1-Wire adaptér,
- síťový teploměr.

Nejdříve je ale nutné zachytit přesný formát funkčního souboru `log`. Do repozitáře je vhodné přidat anonymizovaný příklad, až bude k dispozici.

## Doporučení pro archivaci

Uložte společně:

- `digitemp_DS9097.exe`,
- konfigurační soubor DigiTemp,
- příklad funkčního logu,
- ROM adresy čidel,
- schéma adaptéru,
- označení COM portu,
- použitou verzi programu DigiTemp.