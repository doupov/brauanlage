# Digitální archeologie: jak byla Brauanlage 4.3 zachráněna

## Proč bylo potřeba program zachraňovat

Brauanlage vznikla v době, kdy byl běžný domácí počítač s Windows XP, fyzickým paralelním portem LPT a sériovým portem RS-232. Program byl šířen jako freeware pro nekomerční domácí použití a část dokumentace žila pouze na osobních stránkách autora a domácích sládků.

Takový software stárne jinak než samostatný spustitelný soubor. K jeho funkci je potřeba celý ekosystém:

- konkrétní verze Windows,
- Visual Basic 6 runtime,
- ActiveX/OCX knihovny,
- Microsoft Forms 2.0,
- ovladač pro přímý přístup k LPT,
- externí program DigiTemp,
- správná místní nastavení,
- fyzický port na správné I/O adrese,
- reléová karta a odpovídající zapojení.

Jakmile zaniknou původní weby a odkazy, nestačí najít jen `Brauanlage_43.exe`. Je potřeba zrekonstruovat prostředí, které autor považoval za samozřejmé.

## 1. Hledání na zaniklých stránkách

Původní stránky autora už neposkytovaly funkční stažení. Stopy však zůstaly v:

- starých českých článcích o domácím vaření,
- návodech uživatelů Framax, Kralupyvo a dalších,
- odkazech na demonstrační recepty,
- názvech instalačních souborů,
- internetových archivech,
- soukromých zálohách uživatelů.

Klíčové bylo nehledat pouze obecné slovo „Brauanlage“, ale přesné historické názvy:

```text
Brauanlage_43.exe
Brauanlage_V43_setup.zip
NewAle.rez
MinerAle.rez
digitemp_DS9097.exe
InpOut32.dll
IOWKIT.dll
```

Přesný název souboru často vede k archivní kopii nebo zmínce na stránce, která už sama nefunguje.

## 2. Dohledání instalačních souborů

Podařilo se obnovit nebo identifikovat zejména:

```text
Brauanlage_43.exe
Brauanlage_V43_setup.zip
VB6.0-KB290887-X86.exe
VB60SP6-KB2708437-x86-ENU.msi
VisualBasic6-KB896559-v1-ENU
```

Samotný instalační balíček však nestačil. Po prvním spuštění se postupně objevovaly chybějící komponenty. Každá chybová zpráva se tak stala vodítkem k další vrstvě původního prostředí.

## 3. Visual Basic 6 runtime

Brauanlage je klasická 32bitová aplikace napsaná ve Visual Basicu 6. Pro spuštění potřebuje runtime a ActiveX komponenty, které bývaly na starých počítačích často přítomné díky jiným aplikacím nebo Microsoft Office.

Na čisté instalaci Windows XP ale mohou chybět.

Důležité rozlišení:

- **VB6 Runtime** zajišťuje základní běh aplikace.
- **OCX komponenty** poskytují konkrétní ovládací prvky, dialogy, tabulky a komunikaci.
- **VB6 SP6 aktualizace** nemusí sama doplnit všechny chybějící komponenty, pokud na počítači není VB6 IDE.

Proto bylo nutné kombinovat instalaci runtime, aktualizace a ruční registraci knihoven.

## 4. Registrace OCX

Postupně se objevily chyby typu Runtime Error 339. Ty obvykle znamenají, že komponenta:

- není v systému,
- je ve špatné složce,
- není zaregistrovaná,
- nebo je přítomná nesprávná verze.

Mezi důležité komponenty patřily například:

```text
MSCOMCTL.OCX
COMDLG32.OCX
MSCOMM32.OCX
TABCTL32.OCX
RICHTX32.OCX
MSFLXGRD.OCX
```

Na 32bitovém Windows XP se obvykle kopírují do:

```text
C:\Windows\System32
```

A registrují se:

```bat
regsvr32 C:\Windows\System32\MSCOMCTL.OCX
regsvr32 C:\Windows\System32\COMDLG32.OCX
```

Registrace musí skončit hlášením o úspěchu. U běžných OCX a COM DLL se používá `regsvr32`; u `InpOut32.dll` nikoli.

## 5. FM20.DLL a Microsoft Office

Další překážkou byla chybějící knihovna:

```text
FM20.DLL
```

Jde o Microsoft Forms 2.0 Object Library. Není to běžný samostatný redistribuovatelný balíček a Microsoft ji neposkytuje jako doporučený samostatný download. Historicky se instalovala jako součást Microsoft Office.

Praktické řešení bylo nainstalovat 32bitový Microsoft Office XP. Poté se program rozběhl.

To je důležitá archivní informace: u starých VB6 aplikací může být Office fakticky součástí běhového prostředí, i když aplikace samotná není kancelářský program.

Nedoporučuje se stahovat `FM20.DLL` z náhodných webů s DLL soubory. Bezpečnější a licenčně čistší je instalovat ji z legitimní kopie Office.

## 6. Runtime Error 13 a desetinný oddělovač

České místní nastavení používá desetinnou čárku. Program však některé hodnoty očekává s desetinnou tečkou.

Řešení ve Windows XP:

```text
Ovládací panely
→ Místní a jazykové nastavení
→ Vlastní nastavení
→ Desetinný oddělovač
→ změnit , na .
```

Bez této změny se může objevit:

```text
Runtime Error 13 – Type mismatch
```

Při zadávání receptů se také osvědčilo přepnout klávesnici do angličtiny a číslice psát horní číselnou řadou.

## 7. LPT a reléová karta

Po zprovoznění GUI program stále neovládal relé. Hardware používal:

```text
LPT1: 0378–037F
pomocný rozsah: 0778–077B
```

V programu bylo správně nastaveno:

```text
LPT1 (378)
```

Na reléové kartě svítily vstupní LED. To dokazovalo, že na pinech LPT existuje logická úroveň, ale ne že program skutečně úspěšně zapisuje.

Původně se prověřovalo:

- napájení 12 V reléové části,
- správné číslování DB25,
- spojení pinů 2, 3, 4, 5, 6 a 9,
- zem na pinu 18,
- režim LPT v BIOSu,
- správná adresa portu,
- verze `InpOut32.dll`.

## 8. InpOut32.dll

Ve složce programu byla původní knihovna:

```text
InpOut32.dll
velikost: 32 768 B
historické datum: 2005/2007
```

Tato knihovna umožňuje 32bitové aplikaci zapisovat přímo na hardwarovou I/O adresu LPT. Na Windows NT/2000/XP není přímý přístup do portu běžné uživatelské aplikaci automaticky povolen.

`InpOut32.dll` se neregistruje pomocí `regsvr32`. Musí být dostupná aplikaci, typicky přímo vedle EXE.

## 9. Poslední chybějící krok: správce

Rozhodující objev byl prostý:

> Brauanlage musí být spuštěna jako správce.

Bez zvýšených oprávnění:

- aplikace se normálně otevřela,
- ovládací prvky reagovaly,
- reléová karta zůstávala ve výchozím stavu,
- nebyla vidět jasná chyba zápisu na LPT.

Po spuštění jako správce začalo přímé ovládání portu `0x378` fungovat a relé se přepínala.

Tato chyba byla zákeřná právě proto, že nebránila spuštění aplikace. Selhala jen hardwarová vrstva.

## 10. Co se podařilo zachránit

Výsledkem není jen funkční EXE, ale rekonstruovaný provozní celek:

- Windows XP,
- VB6 runtime,
- potřebné OCX,
- Microsoft Forms 2.0 z Office,
- správné místní nastavení,
- DigiTemp a DS9097,
- fyzické LPT na `0x378`,
- InpOut32,
- reléová karta,
- recepty `.rez`,
- znalost nutnosti administrátorských práv.

## Proč to dokumentovat

Historický software se neztrácí jen smazáním zdrojového kódu. Ztrácí se také tehdy, když nikdo neví:

- jaké měl závislosti,
- na jakém hardware běžel,
- co znamenají jeho chybové hlášky,
- jak byly zapojeny periférie,
- jaké nezdokumentované předpoklady měl autor.

Tento repozitář proto uchovává nejen soubory, ale i postup uvažování. Právě ten bývá při další obnově nejcennější.

# Epilog

Celá rekonstrukce byla provedena na notebooku **Dell Latitude D600**.

Notebook strávil dlouhá léta odložený ve skladu. Po jeho otevření následovalo
jediné, co bylo potřeba udělat: vyfoukat prach a několik pavučin z ventilátoru.

Pak se stal malý zázrak.

Dell bez problémů nabootoval původní **Windows XP**, ožil integrovaný
paralelní port (LPT), sériový port (COM) a po několika hodinách digitální
archeologie se podařilo znovu zprovoznit celý pivovarský systém.

Cesta vedla přes:

- hledání zaniklých webových stránek,
- dohledání instalačních balíků,
- Visual Basic 6 Runtime,
- registraci OCX komponent,
- Microsoft Forms 2.0 (FM20.DLL),
- DigiTemp a 1-Wire teploměr,
- InpOut32.dll,
- správné nastavení LPT,
- a nakonec zdánlivě banální, ale zásadní zjištění, že **Brauanlage musí být spuštěna jako správce**, aby mohl zapisovat na LPT port.

Výsledek stál za to.

> **Vyfoukali jsme pavouky z ventilátoru, notebook nastartoval po dvaceti letech a začal znovu vařit pivo.**

Doufáme, že tento repozitář pomůže zachovat Brauanlage i dalším domácím
sládkům a že za dalších deset nebo dvacet let nebude potřeba začínat znovu od nuly.

---

## Poděkování

Rekonstrukce, testování, archivace a ověření funkčnosti:
- **Martin Fox** (https://github.com/doupov)

Při analýze historického software, přípravě dokumentace, rekonstrukci
instalačního postupu a řešení kompatibility byla využita asistence
**ChatGPT (OpenAI)**.

Pokud máte další materiály, schémata, instalační soubory nebo zkušenosti s Brauanlage,
budeme rádi za Issue nebo Pull Request.
