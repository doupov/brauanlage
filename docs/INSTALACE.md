# Kompletní instalace Brauanlage 4.3

## 1. Doporučená platforma

Nejjednodušší a nejvěrnější prostředí:

- Windows XP 32bit,
- fyzický paralelní port LPT,
- fyzický sériový port RS-232,
- lokální administrátorský účet,
- 32bitový Microsoft Office XP nebo 2003.

USB–LPT redukce obvykle nevytvářejí klasický I/O port na adrese `0x378` a pro přímé bitové ovládání nejsou vhodné.

## 2. Doporučené pořadí instalace

1. Windows XP a ovladače čipsetu.
2. Ověření LPT a COM ve Správci zařízení.
3. Visual Basic 6 Runtime.
4. VB6 SP6 aktualizace.
5. Potřebné OCX knihovny.
6. Microsoft Office kvůli Microsoft Forms 2.0.
7. Brauanlage 4.3.
8. DigiTemp.
9. Nastavení místního formátu.
10. Test programu jako správce.
11. Test LPT bez připojené silové části.
12. Test teploty.

## 3. Ověření portů

Ve Windows XP:

```text
Ovládací panely
→ Systém
→ Hardware
→ Správce zařízení
```

U LPT otevřete kartu **Prostředky**. Typický funkční stav:

```text
0378–037F
0778–077B
```

Do Brauanlage se zadává základní adresa:

```text
378
```

COM port si poznamenejte, například `COM1`.

## 4. Visual Basic 6 Runtime

Nainstalujte historický VB6 runtime odpovídající 32bitovému systému. Archivovaný soubor se často jmenuje:

```text
VB6.0-KB290887-X86.exe
```

Microsoft stále nabízí některé aktualizace VB6 SP6:

- https://www.microsoft.com/en-us/download/details.aspx?id=7030
- https://www.microsoft.com/en-us/download/details.aspx?id=30505

Pozor: aktualizační MSI nemusí samo nainstalovat všechny chybějící ActiveX komponenty na počítači bez VB6 IDE.

## 5. OCX knihovny

Nejčastěji potřebné soubory:

```text
MSCOMCTL.OCX
COMDLG32.OCX
MSCOMM32.OCX
TABCTL32.OCX
RICHTX32.OCX
MSFLXGRD.OCX
```

Na 32bitovém Windows XP je zkopírujte do:

```text
C:\Windows\System32
```

Poté spusťte příkazový řádek jako správce a registrujte jednotlivé soubory:

```bat
regsvr32 C:\Windows\System32\MSCOMCTL.OCX
regsvr32 C:\Windows\System32\COMDLG32.OCX
regsvr32 C:\Windows\System32\MSCOMM32.OCX
regsvr32 C:\Windows\System32\TABCTL32.OCX
regsvr32 C:\Windows\System32\RICHTX32.OCX
regsvr32 C:\Windows\System32\MSFLXGRD.OCX
```

Úspěšná registrace skončí potvrzením `DllRegisterServer succeeded` nebo českým ekvivalentem.

### Hromadná registrace

```bat
@echo off
cd /d C:\Windows\System32
for %%F in (MSCOMCTL.OCX COMDLG32.OCX MSCOMM32.OCX TABCTL32.OCX RICHTX32.OCX MSFLXGRD.OCX) do regsvr32 /s %%F
pause
```

Tichý přepínač `/s` skryje dialogy. Pro první diagnostiku je lepší registrace bez `/s`.

## 6. Microsoft Forms 2.0 – FM20.DLL

Když program hlásí chybějící `FM20.DLL`, nejbezpečnější řešení je nainstalovat legitimní 32bitovou kopii Microsoft Office XP/2003.

Microsoft uvádí, že FM20.DLL není podporovaný samostatný download a je součástí Office:

- https://learn.microsoft.com/en-us/answers/questions/4374482/microsoft-forms-2-0-dll-download

Nedoporučuje se stahovat tuto knihovnu z náhodných DLL webů.

## 7. Instalace Brauanlage

Doporučená cesta:

```text
C:\Program Files\Brauanlage
```

Ve složce programu by měly zůstat také knihovny dodané autorem, zejména:

```text
InpOut32.dll
IOWKIT.dll
```

`InpOut32.dll` neregistrujte pomocí `regsvr32`. Program ji načítá přímo.

## 8. Místní nastavení

Nastavte desetinný oddělovač na tečku:

```text
Ovládací panely
→ Místní a jazykové nastavení
→ Vlastní nastavení
→ Desetinný oddělovač: .
```

Tím se řeší častý `Runtime Error 13`.

## 9. První spuštění

Spusťte program administrátorsky:

```text
pravé tlačítko na Brauanlage_43.exe
→ Spustit jako správce
```

Je-li dostupná karta Kompatibilita, nastavte tuto volbu trvale.

## 10. Základní konfigurace

Doporučené hodnoty:

```text
Language: Czech
Relay output: LPT1 (378)
Temperature port: COM1 až COM4 podle Správce zařízení
Temperature program: digitemp_DS9097.exe
Log file: log
```

Některé verze rozhraní očekávají název bez přípony:

```text
digitemp_DS9097
```

Řiďte se názvem souboru skutečně uloženého vedle programu a původní konfigurací.

## 11. Bezpečný test

Nejdříve odpojte silové spotřebiče. Ověřte pouze:

- změnu LED reléové karty,
- sepnutí malých 12V relé,
- správné přiřazení funkcí,
- čtení teploty.

Teprve potom připojte stykače a silovou část.

## 12. Záloha funkční instalace

Po úspěšném zprovoznění zazálohujte:

- celý adresář Brauanlage,
- instalační soubory VB6,
- OCX knihovny,
- Office instalační médium a licenci,
- DigiTemp,
- recepty `.rez`,
- konfiguraci,
- fotografie a schémata hardware,
- export Správce zařízení nebo alespoň seznam adres portů.

Doporučuje se vytvořit i obraz celého disku, protože budoucí obnova starého systému může být jednodušší z image než opakováním instalace.