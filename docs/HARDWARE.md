# LPT, reléová karta a bezpečnost

## Princip

Brauanlage zapisuje jednotlivé bity datového registru paralelního portu. Každý bit ovládá jeden kanál reléové karty.

Ověřené přiřazení:

| Pin DB25 | Datový bit | Funkce |
|---:|---:|---|
| 2 | D0 | Topení |
| 3 | D1 | Míchání |
| 4 | D2 | Chlazení |
| 5 | D3 | Čerpadlo 1 |
| 6 | D4 | Čerpadlo 2 |
| 9 | D7 | Siréna |
| 18 | GND | zem signálové části |

Piny 7 a 8 mohou zůstat nevyužité podle konkrétního zapojení.

## Typická reléová větev

Historické schéma používá pro každý kanál přibližně:

```text
LPT pin
→ odpor 1 kΩ
→ indikační LED
→ LED optočlenu PC817
→ tranzistor BC547C
→ cívka 12V relé
→ ochranná dioda 1N4007
```

Optočlen odděluje počítač od 12V reléové části. Silové spotřebiče nemají být spínány přímo malým relé na desce, ale vhodnými stykači nebo výkonovými prvky.

## Napájení

Reléová část potřebuje samostatných přibližně 12 V DC. Svítící vstupní LED sama nepotvrzuje, že je 12V větev v pořádku.

Při diagnostice ověřte:

- napětí zdroje,
- polaritu,
- přítomnost společné země tam, kde ji schéma vyžaduje,
- orientaci PC817,
- orientaci tranzistoru,
- orientaci ochranné diody,
- napětí na cívce relé při sepnutí.

## LPT adresa

Ověřený port:

```text
LPT1: 0x378
```

Ve Správci zařízení se může zobrazit:

```text
0378–037F
0778–077B
```

Do programu se zadává základní adresa `378`.

## BIOS

Pokud port nereaguje, ověřte v BIOSu:

- že je paralelní port povolený,
- že používá adresu `378h`,
- případně vyzkoušejte režim SPP místo ECP/EPP.

Brauanlage používá jednoduchý zápis do datového registru; klasický SPP režim bývá nejpředvídatelnější.

## Proč USB–LPT obvykle nefunguje

Běžná USB redukce implementuje tiskový protokol, nikoli skutečný paralelní port dostupný přes I/O adresu `0x378`. `InpOut32.dll` proto nemá kam zapsat.

Použijte:

- základní desku s nativním LPT,
- notebook s fyzickým DB25 portem,
- případně skutečnou PCI/PCIe LPT kartu, která zpřístupní I/O adresu kompatibilní s programem.

## Diagnostický postup

### 1. Test bez silové části

Odpojte topná tělesa, motory a čerpadla. Nechte připojenou jen řídicí a 12V reléovou část.

### 2. Ověření LED

V manuálním režimu zapínejte jednotlivé funkce. Sledujte, zda příslušná LED mění stav.

### 3. Měření LPT

Černý hrot multimetru:

```text
pin 18
```

Červený hrot:

```text
pin 2, 3, 4, 5, 6 nebo 9
```

Při přepnutí výstupu má být vidět změna mezi nízkou a vysokou logickou úrovní, typicky přibližně 0 V a několik voltů.

### 4. Test reléové desky mimo PC

Pouze po odpojení DB25 od počítače lze vstup konkrétního kanálu zkusit budit externím logickým napětím odpovídajícím schématu. Nikdy současně nepřipojujte externí zdroj na datový pin a LPT počítače.

## Administrátorská práva

Pokud všechny vstupní LED zůstávají ve výchozím stavu a manuální režim nic nemění, přestože je adresa správná, spusťte Brauanlage jako správce.

Na ověřené instalaci byl program bez správce funkční pouze na úrovni GUI. Přístup přes `InpOut32.dll` k portu `0x378` nefungoval.

## Bezpečnost silové části

Silová část varny může zahrnovat:

- síťové napětí 230/400 V,
- topná tělesa s vysokým příkonem,
- čerpadla,
- motory míchadel,
- stykače,
- ochranné prvky,
- kovové nádoby a vlhké prostředí.

Minimální požadavky:

- proudový chránič,
- správné jištění každé větve,
- ochranný vodič PE,
- oddělení SELV a síťových obvodů,
- vhodná krytí a průchodky,
- nouzové vypnutí nezávislé na PC,
- stykače navržené na skutečný proud,
- odborná kontrola a revize.

PC nesmí být jediným bezpečnostním prvkem. Při pádu Windows nebo zamrznutí programu musí být možné topení fyzicky odpojit.