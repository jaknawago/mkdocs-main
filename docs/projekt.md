# Založení projektu

### Standardní projekt
Tento postup vytvoří nový projekt, vloží do něj zvolené zařízení a základní strukturu projektu.

1.  Klikněte na `File - New Project - Standard project` a povrďte tlačítkem OK.
2.  Vyberte profil vašeho PLC a jazyk pro základní blok.

### Prázdný projekt
Vytvoří prázdný projekt bez zařízení. 

1.  Klikněte na `File - New Project - Empty project` a povrďte tlačítkem OK.

### Přidání zařízení
Do stávájícího projektu lze přidat další zařízení.

1.  Klikněte pravým tlačítkem na název projektu ve stromové struktuře a zvolte `Add Device`.
2.  Z katalogu vyberte profil zařízení - pro urychlení lze filtrovat zadáním objednacího čísla (např. 750-8212).
3.  Přidejte stiskem tlačítka `Add Device`.

<!-- ### Nastavení spojení se zařízením -->
 
## Konfigurace hardware

Kompaktní PLC (např. 751-9301) mají pevně daný typ a počet vstupů a výstupů. Ty jsou definovány při výběru profilu PLC při založení projektu. 

Modulární PLC lze osadit různými moduly - je proto nutné konkrétní moduly v projektu specifikovat. To lze provést buď skenováním nebo je přidat ručně.
???+ info "K-Bus"
    Je interní sběrnice pro komunikaci s jednotlivými IO moduly. Fyzické propojení je realizováno zlacenými kontakty na boční straně každé rozšiřující karty. Z toho plyne omezení v podobě maximálního počtu 64 připojených modulů (lze navýšit až na 250 při použití rozšíření sběrnice 750-627 a 750-628).

    Pro správnou funkci K-Bus je nezbytné využít jako poslední zakončovací modul s označením 750-600.
### Skenování modulů
1.  Klikněte pravým tlačítkem myši na položku `Kbus` ve stromové struktuře projektu a z nabídky vyberte `Scan for Devices`. Zobrazí se okno s načtenými moduly.
2.  Stiskem `Copy All Devices to Project` se moduly přidají do projektu. 
### Ruční přidání modulů
1.  Klikněte pravým tlačítkem myši na položku `Kbus` ve stromové struktuře projektu a z nabídky vyberte `Add Device`. Zobrazí se okno s katalogem modulů.
2.  Z katalogu postupně vyberte jednotlivé moduly podle jejich objednacího čísla a přidejte je do projektu tlačítkem `Add Device`. Pro urychlení lze využít kontextové vyhledávání.
### Pojmenování IO
Každý kanál jednotlivých modulů lze pojmenovat pro snažší orientaci v programu.

1.  Rozklikněte položku `Kbus` a poklepejte na vybraný modul a v novém okně přejděte do záložky `K-Bus I/O Mapping`.

    V přípádě kompaktního PLC (751-9301) poklepejte na položku `Compact_Controller_100_Onboard_IO` a dále `Onboard-IO I/O Mapping`.

2.  Do levého sloupce `Variable` zadejte jednotlivé názvy.
Zadnými názvy se pak v programu budete moci odkazovat na dané kanály modulů.
???+ warning "Varování"
    Pro pojmenování lze použít základní alfanumerické znaky a podtržítko. Nelze použít znaky české abecedy, pomlčky, mezery a jiné symboly. Název proměnné nesmí začínat číslicí.

    -   Příklady nevhodných názvů:
        *   3MojeTeplota
        *   Moje-Teplota
        *   Moje Teplota
        *   Moje#@Teplota
        *   MojeSvětlo

