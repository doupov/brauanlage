# Používání Brauanlage 4.3

## První orientace

Po spuštění programu:

1. vyberte jazyk,
2. nastavte LPT port,
3. nastavte COM port pro teplotu,
4. zadejte DigiTemp program a název logu,
5. potvrďte podmínky použití,
6. vyčkejte na nalezení teplotního čidla.

Při správné konfiguraci se teplota objeví v zeleném poli v pravé horní části hlavního okna.

## Manuální režim

Před automatickým vařením ověřte každý výstup ručně:

- topení,
- míchání,
- chlazení,
- čerpadlo 1,
- čerpadlo 2,
- siréna.

Test provádějte nejprve bez připojených silových spotřebičů. Sledujte LED reléové karty a sepnutí malých relé.

## Ukázkové recepty

Původní instalace obsahuje dva demonstrační recepty:

```text
NewAle.rez
MinerAle.rez
```

Načtení:

```text
Parameters / Parametry
→ Load
→ vybrat soubor .rez
```

Tyto soubory jsou nejlepším zdrojem pro pochopení syntaxe a pořadí kroků.

## Simulace

Před prvním skutečným vařením spusťte recept v simulaci a sledujte:

- změny cílové teploty,
- čekání na dosažení teploty,
- spínání topení,
- míchání,
- časování prodlev,
- aktivaci čerpadel,
- chlazení,
- alarmy.

Simulace pomůže odhalit chyby v receptu bez rizika přehřátí nebo chodu čerpadla nasucho.

## Zadávání hodnot

Historické české zkušenosti doporučují:

- přepnout klávesnici do angličtiny,
- používat desetinnou tečku,
- číslice zadávat horní číselnou řadou,
- při prvním vytvoření textu nepoužívat diakritiku,
- diakritiku případně doplnit až následně.

Program je citlivý na místní formát a některé znaky.

## Ukládání receptů

Vlastní recept ukládejte do kořenového adresáře programu, tedy tam, kde jsou demonstrační `.rez` soubory.

Doporučené umístění:

```text
C:\Program Files\Brauanlage\MujRecept.rez
```

Při ukládání jinam mohou vznikat problémy s relativními cestami nebo následným načtením.

## Doporučený proces tvorby receptu

1. Zkopírujte demonstrační recept.
2. Přejmenujte kopii.
3. Měňte vždy jen jednu část.
4. Po každé změně recept uložte.
5. Spusťte simulaci.
6. Zkontrolujte všechny přechody a podmínky.
7. Udělejte suchý test s relé bez silové části.
8. Teprve potom proveďte zkušební várku pod dohledem.

## Provozní doporučení

- Nenechávejte varnu bez dozoru.
- Mějte samostatné nouzové vypnutí topení.
- Ověřte, že čidlo teploty je mechanicky upevněné.
- Před startem zkontrolujte, zda čerpadla nejsou nasucho.
- Po změně receptu vždy proveďte simulaci.
- Uchovávejte známou funkční kopii receptu.
- Zapisujte změny hardware i software.

## Zálohování receptů

Doporučená struktura:

```text
recipes/
├── original/
│   ├── NewAle.rez
│   └── MinerAle.rez
├── tested/
└── experimental/
```

Ke každému receptu je užitečné přidat textový soubor s:

- datem posledního testu,
- použitým objemem,
- výkonem topení,
- zapojenými čerpadly,
- verzí programu,
- poznámkami k výsledku.