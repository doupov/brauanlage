# Brauanlage 4.3 – záchrana historického řízení domácí varny

Tento repozitář dokumentuje zprovoznění a zachování programu **Brauanlage 4.3** od německého autora **Thomase Karpena** (Samba und Bier), který byl v české komunitě domácích sládků používán k automatizaci varny.

Program pochází z éry Windows XP a ovládá technologii pomocí:

- paralelního portu **LPT** a reléové karty,
- sériového portu **RS-232**,
- teplotních čidel **DS18B20** přes adaptér **DS9097**,
- externího programu **DigiTemp**,
- receptů uložených v souborech `.rez`.

Původní webové stránky, návody a instalační balíčky postupně mizely. Tento repozitář proto neslouží jen jako instalační návod, ale jako dokumentace digitální archeologie: co bylo nutné dohledat, proč program přestal fungovat na čisté instalaci Windows XP a jak se podařilo obnovit celý řetězec od VB6 knihoven až po skutečné sepnutí relé.

> [!WARNING]
> Silová část varny pracuje se síťovým napětím a vysokými proudy. Zapojení, revizi a servis silové části musí provádět osoba s odpovídající kvalifikací. Počítač ani LPT reléovou kartu nepřipojujte a neodpojujte za provozu.

## Stav projektu

Ověřeno na 32bitovém Windows XP:

- program se spustí,
- české rozhraní funguje,
- načítání receptů funguje,
- LPT1 na adrese `0x378` ovládá relé,
- zásadní podmínkou je spuštění programu s administrátorskými právy,
- instalace Microsoft Office doplnila chybějící `FM20.DLL`.

## Rychlý postup

1. Použijte 32bitový Windows XP s fyzickým LPT a COM portem.
2. Nainstalujte Visual Basic 6 Runtime.
3. Doplňte a zaregistrujte požadované OCX komponenty.
4. Nainstalujte vhodnou 32bitovou verzi Microsoft Office kvůli `FM20.DLL`.
5. Ve složce programu ponechte `InpOut32.dll` a `IOWKIT.dll`.
6. V místním nastavení změňte desetinný oddělovač z čárky na tečku.
7. Nastavte LPT1 na adrese `378h` a správný COM port.
8. Program **spouštějte jako správce**.
9. Nejprve ověřte relé v manuálním režimu, teprve potom připojte silovou část.
10. Prostudujte ukázkové recepty `NewAle.rez` a `MinerAle.rez`.

## Dokumentace

- [Digitální archeologie a příběh záchrany](docs/ARCHEOLOGIE.md)
- [Kompletní instalace](docs/INSTALACE.md)
- [LPT, reléová karta a bezpečnost](docs/HARDWARE.md)
- [DigiTemp a měření teploty](docs/DIGITEMP.md)
- [Používání programu a recepty](docs/POUZITI.md)
- [Řešení problémů](docs/TROUBLESHOOTING.md)
- [Zdroje, odkazy a archivace](docs/ZDROJE.md)
- [Právní a licenční poznámky](LEGAL.md)

## Nejdůležitější poznatek

Program může vypadat plně funkčně, ale bez administrátorských práv nemusí `InpOut32.dll` získat přístup k I/O portu `0x378`. GUI reaguje, všechny vstupní LED reléové karty mohou zůstat ve výchozím stavu HIGH, ale relé se nepřepnou.

Řešení:

```text
Brauanlage_43.exe
→ pravé tlačítko
→ Spustit jako správce
```

Na testované instalaci to byl poslední chybějící krok a po jeho provedení začala relé fungovat.

## Microsoft odkazy

- [Visual Basic 6.0 SP6 Cumulative Update – Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=7030)
- [Visual Basic 6.0 SP6 Security Rollup – Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=30505)
- [Microsoft Forms 2.0 / FM20.DLL – vysvětlení na Microsoft Learn](https://learn.microsoft.com/en-us/answers/questions/4374482/microsoft-forms-2-0-dll-download)

Upozornění: balíček `VB60SP6-KB2708437-x86-ENU.msi` aktualizuje komponenty existující instalace VB6 a nemusí sám nainstalovat všechny chybějící ovládací prvky, pokud na systému není VB6 IDE. Proto jsou v návodu popsány i ruční kontroly a registrace OCX.

## Cíl repozitáře

Cílem není modernizovat program za každou cenu. Cílem je uchovat dostatek znalostí, aby bylo možné:

- znovu sestavit funkční historickou instalaci,
- pochopit vazby mezi softwarem a hardwarem,
- diagnostikovat chyby bez závislosti na zaniklých fórech,
- bezpečně archivovat původní instalační soubory a dokumentaci,
- případně později nahradit jednotlivé části moderním hardwarem.

## Referenční hardware

Rekonstrukce byla úspěšně ověřena na:

- Dell Latitude D600
- Windows XP SP3
- integrovaný LPT (0x378)
- integrovaný COM (RS-232)
- DS9097 + DS18S20 / DS18B20
- původní reléová karta podle schématu Thomase Karpena

Dell D600 se ukázal jako ideální "záchranný notebook" pro historický software,
protože jako jeden z posledních běžných notebooků nabízí současně nativní
LPT i COM port.

## Poděkování

- Thomas Karpen – původní autor programu.
- Framax a další čeští domácí sládci – praktické návody a zkušenosti.
- Autoři webu Kralupyvo – článek „Řízení varny pomocí PC“.
- Komunita kolem DigiTemp a 1-Wire.
- Internet Archive a všichni, kteří uchovali kopie zaniklých souborů.

Dokumentace byla znovu sestavena a prakticky ověřena v roce 2026.
