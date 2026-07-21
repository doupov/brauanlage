# Instalační soubory

Do této složky patří původní instalační balíčky programu Brauanlage, například:

- `Brauanlage_V43_setup.zip`
- `Brauanlage_43.exe`

## Doporučení při nahrávání

- Zachovej původní názvy souborů.
- Neměň obsah archivů ani spustitelných souborů.
- Ke každému souboru doplň kontrolní součet SHA-256.
- Pokud je k dispozici původní licence, README nebo text podmínek autora, přidej jej beze změn.
- Microsoft runtime, Office, FM20.DLL a další redistribuovatelné komponenty Microsoftu sem nevkládej bez ověření jejich licence; v dokumentaci používej oficiální odkazy.

## Výpočet SHA-256

### Windows XP / starší Windows

Lze použít například Microsoft File Checksum Integrity Verifier (`fciv.exe`):

```bat
fciv.exe -sha256 Brauanlage_V43_setup.zip
fciv.exe -sha256 Brauanlage_43.exe
```

### Novější Windows

```powershell
Get-FileHash .\Brauanlage_V43_setup.zip -Algorithm SHA256
Get-FileHash .\Brauanlage_43.exe -Algorithm SHA256
```

### Linux / macOS

```bash
sha256sum Brauanlage_V43_setup.zip Brauanlage_43.exe
```

Na macOS lze také použít:

```bash
shasum -a 256 Brauanlage_V43_setup.zip Brauanlage_43.exe
```

## Poznámka k redistribuci

Program byl historicky uváděn jako freeware pro nekomerční použití. Pokud se podaří dohledat přesné podmínky redistribuce od původního autora, přidej je do repozitáře a odkaž na ně z tohoto souboru.
