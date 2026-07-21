# Řešení problémů

## Program se nespustí

### Runtime Error 339

Význam: chybí nebo není zaregistrovaná OCX/DLL komponenta.

Postup:

1. Zapište si přesný název souboru z hlášení.
2. Ověřte, zda je soubor v `C:\Windows\System32`.
3. Zaregistrujte jej přes `regsvr32`.
4. Restartujte program.

Příklad:

```bat
regsvr32 C:\Windows\System32\MSCOMCTL.OCX
```

Časté soubory:

```text
MSCOMCTL.OCX
COMDLG32.OCX
MSCOMM32.OCX
TABCTL32.OCX
RICHTX32.OCX
MSFLXGRD.OCX
```

## Chybí FM20.DLL

`FM20.DLL` je Microsoft Forms 2.0. Nainstalujte nebo opravte legitimní 32bitovou instalaci Microsoft Office XP/2003.

Nestahujte náhodnou DLL z webu. Může být nekompatibilní, škodlivá nebo licenčně problematická.

## Runtime Error 13

Význam: typová neshoda, často způsobená desetinnou čárkou.

Řešení:

```text
Ovládací panely
→ Místní a jazykové nastavení
→ Vlastní nastavení
→ Desetinný oddělovač
→ .
```

## Program běží, ale relé nereagují

Postupujte v tomto pořadí:

1. Spusťte Brauanlage jako správce.
2. Ověřte `LPT1 (378)` v programu.
3. Ověřte adresu `0378–037F` ve Správci zařízení.
4. Ověřte přítomnost `InpOut32.dll` vedle EXE.
5. Nepoužívejte `regsvr32` na `InpOut32.dll`.
6. Ověřte fyzický DB25 kabel.
7. Ověřte zem na pinu 18.
8. Ověřte 12V napájení reléové části.
9. Vyzkoušejte SPP režim v BIOSu.
10. Změřte výstupní piny multimetrem.

Na ověřené instalaci byl problém vyřešen spuštěním jako správce.

## Všechny LED reléové karty svítí

To může být výchozí stav datových pinů LPT. Neznamená to automaticky, že program zapisuje.

Ověřte, zda se stav konkrétní LED změní při přepnutí výstupu v manuálním režimu.

Pokud ne:

- program nemá oprávnění,
- používá se nesprávná adresa,
- port není skutečný LPT,
- knihovna InpOut32 se nenačetla,
- kabel je chybný.

## LED reaguje, ale relé nesepne

Software a LPT pravděpodobně fungují. Hledejte chybu na desce:

- chybí 12 V,
- vadný nebo obrácený PC817,
- špatně zapojený BC547C,
- přerušená cesta,
- vadné relé,
- ochranná dioda je obráceně nebo ve zkratu,
- nedostatečný proud optočlenem.

## Relé sepne, ale stykač nebo spotřebič ne

Hledejte v silové části:

- napětí cívky stykače,
- pojistku nebo jistič,
- přerušený vodič,
- špatně zvolený kontakt NO/NC,
- nouzové STOP,
- tepelnou ochranu,
- blokovací kontakt.

Silovou část řeší kvalifikovaná osoba.

## DigiTemp nenajde čidlo

- ověřte COM port,
- spusťte DigiTemp samostatně,
- ověřte DS9097,
- zkontrolujte kabeláž 1-Wire,
- ověřte napájení čidla,
- zkraťte sběrnici,
- zkontrolujte pull-up rezistor,
- ověřte, že COM port nepoužívá jiný program.

## DigiTemp měří, ale Brauanlage teplotu neukáže

- špatný název EXE,
- špatný pracovní adresář,
- špatný název logu,
- jiný formát logu,
- desetinná čárka,
- program nemá právo log číst nebo vytvořit,
- cesta obsahuje neočekávané znaky.

Doporučení: umístěte EXE a log do kořenové složky Brauanlage a používejte krátké názvy bez mezer a diakritiky.

## Recept se nenačte nebo chová divně

- uložte `.rez` do kořenového adresáře programu,
- nepoužívejte dlouhé cesty,
- vyhněte se diakritice v názvu souboru,
- nastavte desetinnou tečku,
- porovnejte strukturu s `NewAle.rez` a `MinerAle.rez`,
- spusťte simulaci.

## Regsvr32 hlásí, že vstupní bod nebyl nalezen

Ne každý DLL soubor je COM knihovna. `InpOut32.dll` a běžné runtime DLL se nemusí a nesmějí registrovat.

Používejte `regsvr32` pouze na OCX a DLL, které skutečně exportují `DllRegisterServer`.

## Kontrolní seznam funkční instalace

- [ ] Windows XP 32bit
- [ ] fyzický LPT
- [ ] adresa `0x378`
- [ ] COM port funkční
- [ ] VB6 runtime
- [ ] OCX zaregistrované
- [ ] FM20.DLL z legitimní instalace Office
- [ ] `InpOut32.dll` vedle EXE
- [ ] desetinná tečka
- [ ] spuštění jako správce
- [ ] relé testována bez silové části
- [ ] DigiTemp funguje samostatně
- [ ] recept simulován
- [ ] nouzové vypnutí funkční