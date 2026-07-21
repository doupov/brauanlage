# Zdroje, odkazy a archivace

## Původní a komunitní zdroje

### Řízení varny pomocí PC – Kralupyvo

Dochovaný český článek z roku 2011 popisuje:

- použití programu Thomase Karpena,
- požadavek na Windows XP, LPT a RS-232,
- reléovou kartu,
- DigiTemp a DS9097,
- Runtime Error 13,
- registraci OCX/DLL,
- demonstrační recepty `NewAle.rez` a `MinerAle.rez`.

Odkaz:

- https://kralupyvo.webnode.cz/news/rizeni-varny-pomoci-pc/

### Framax

Historický návod k odstranění Runtime Error 13 pomocí změny desetinného oddělovače:

- https://hobby.framax.cz/?page_id=968

### Temper / 1-Wire – Tour de Bier

Česká zkušenost s USB/1-Wire teploměrem a DS18B20:

- https://tourdebier.cz/francek/temper-1wire-teplomer-s-cidly-2-x-ds-18b20-z-hongkongu/

### Registrace DLL a OCX

Historický český návod k použití `regsvr32`:

- https://programujte.com/?akce=clanek&cl=2005090104-jak-zaregistrovat-knihovnu-dll-nebo-komponentu-ocx

Uvedené komunitní stránky mohou časem zaniknout nebo změnit obsah. Doporučuje se uložit jejich snímky do Internet Archive a lokálního archivu.

## Oficiální Microsoft zdroje

### Visual Basic 6.0 SP6 Cumulative Update

- https://www.microsoft.com/en-us/download/details.aspx?id=7030

Soubor uváděný Microsoftem:

```text
VB60SP6-KB2708437-x86-ENU.msi
```

Tento balíček je aktualizace. Na čistém systému bez VB6 IDE nemusí nainstalovat všechny chybějící ActiveX komponenty.

### Visual Basic 6.0 SP6 Security Rollup

- https://www.microsoft.com/en-us/download/details.aspx?id=30505

Aktualizuje zejména společné ovládací prvky Visual Basic 6.0 SP6.

### Microsoft Forms 2.0 / FM20.DLL

- https://learn.microsoft.com/en-us/answers/questions/4374482/microsoft-forms-2-0-dll-download

Microsoft uvádí, že `FM20.DLL` je starší komponenta Microsoft Forms 2.0 dodávaná s Office a není poskytována jako podporovaný samostatný download.

## Historické názvy souborů k archivnímu hledání

Při hledání v Internet Archive, katalozích starého software nebo soukromých zálohách používejte přesné názvy:

```text
Brauanlage_43.exe
Brauanlage_V43_setup.zip
VB6.0-KB290887-X86.exe
VB60SP6-KB2708437-x86-ENU.msi
VisualBasic6-KB896559-v1-ENU
MSCOMCTL.OCX
COMDLG32.OCX
MSCOMM32.OCX
TABCTL32.OCX
RICHTX32.OCX
MSFLXGRD.OCX
FM20.DLL
InpOut32.dll
IOWKIT.dll
digitemp_DS9097.exe
NewAle.rez
MinerAle.rez
```

## Jak archivovat soubory správně

Ke každému binárnímu souboru uložte:

- původní název,
- velikost v bajtech,
- datum získání,
- původní URL nebo zdroj,
- SHA-256 hash,
- stručnou poznámku k licenci,
- výsledek antivirové kontroly,
- informaci, zda byl prakticky otestován.

Výpočet SHA-256 na moderním systému:

```bash
sha256sum soubor.exe
```

Ve Windows PowerShell:

```powershell
Get-FileHash .\soubor.exe -Algorithm SHA256
```

Windows XP nemá PowerShell standardně; hash lze spočítat na jiném počítači, aniž by se binární soubor spouštěl.

## Doporučená struktura archivu

```text
archive/
├── original-software/
├── microsoft-prerequisites/
├── third-party-prerequisites/
├── recipes-original/
├── manuals-original/
├── web-snapshots/
├── checksums/
└── photos-and-schematics/
```

## Co neukládat veřejně bez ověření

- nelegální kopie Microsoft Office,
- produktové klíče,
- binární soubory bez jasného práva k redistribuci,
- náhodně stažené DLL neznámého původu,
- osobní údaje z konfigurace nebo logů.

GitHub může sloužit jako dokumentační a hashový katalog, zatímco právně problematické nebo licencované instalační médium musí zůstat v soukromé záloze oprávněného vlastníka.