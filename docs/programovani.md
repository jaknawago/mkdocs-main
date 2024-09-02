# Programování
## Klávesové zkratky
| Příkaz      | Zkratka                          |
| ----------- | ------------------------------------ |
| `Build`       |   ++f11++  |
| `Connect`     |  ++alt+f8++ |
| `Disconnect`  |   ++ctrl+f8++ |
| `Start`  |   ++f5++ |
| `Stop`  |   ++shift+f8++ |
| `Input assist`  |   ++f2++ |
| `Auto declare`  |   ++alt+f2++ |
| `Force value`  |   ++f7++ |
| `Unforce value`  |   ++alt+f7++ |
| `Write value`  |   ++ctrl+f7++ |
| `IntelliSense`  |   ++ctrl+space++ |
| `Comment`  |   ++ctrl+o++ |
| `Uncomment`  |   ++ctrl+i++ |

Klávesové zkratky lze změnit v nastavení prostředí: `Tools` :material-arrow-right-bold-box-outline: `Customize` :material-arrow-right-bold-box-outline: `Keyboard`

## Asistenti
### Auto declare
Průvodce pro deklaraci proměnných nebo úpravu existující deklarace.

:material-mouse: Stisk ++alt+f2++ s kurzorem myši v bloku nebo na proměnné.

### Input assistant
Procházení nebo prohledávání existujících bloků, knihoven, proměnných a dalších. Buď ve stromové struktuře nebo s pomocí kontextového hledání.

:material-mouse: Stisk ++f2++ na prázdném místě.

### IntelliSense

Automatické dokončování při psaní. Nabídka s možností relevantních dokončení dle kontextu.

:material-mouse: Stisk ++ctrl+space++.

???+ tip
    Je možné aktivovat automatické zobrazení nabídky po začátku psaní. 

    V menu `Tools` :material-arrow-right-bold-box-outline: `Options` :material-arrow-right-bold-box-outline: `Smart coding` :material-arrow-right-bold-box-outline: `List components immediately...`


## Boot project

Přeložený projekt je po nahrání uložen pouze v paměti RAM. Při dalším restartu PLC se tedy smaže a jednotka nemá program. Pro zkopírování projektu do flash paměti PLC je nutné vytvořit tzv. boot project.

:material-mouse: Menu `Online` :material-arrow-right-bold-box-outline: `Login` a následně menu `Online` :material-arrow-right-bold-box-outline: `Create Boot Application`.

???+ tip
    Vytvoření boot projektu lze automatizovat nebo nastavit připomenutí při zavření vývojového prostředí. 

    V menu ++rbutton++ `Application` :material-arrow-right-bold-box-outline: `Properties` :material-arrow-right-bold-box-outline: `Boot Application`.

Boot project je reprezentován dvěma soubory `Application.app` a `Application.crc`, které jsou uloženy v adresářové struktuře PLC `:/home/codesys_root/PlcLogic/Application/`.

## Source code

Projekt je PLC uložen v podobě přeloženého binárního souboru, který nelze zpětně editovat v prostředí CODESYS. Pro tyto účely je nutné nahrát i tzv. `Source code`.  

:material-mouse: Menu `Online` :material-arrow-right-bold-box-outline: `Login` a následně menu `Online` :material-arrow-right-bold-box-outline: `Sourcecode download to connected device`.

???+ tip
    Rozsah zálohy a automatizované nahrávání lze nastavit v menu `Project` :material-arrow-right-bold-box-outline: `Project Settings` :material-arrow-right-bold-box-outline: `Sourcecode Download`.

## Vložení knihovny

Pro správu knihoven slouží `Library Manager` umístěný ve stromové struktuře projektu. Aktuálně vložené kniovny jsou zobrazeny ve vrchní části okna správce. 

Přidání knihovny provedeme kliknutím na `Add Library` v okně `Library Manageru`.

Odebrání vybrané knihovny provedeme kliknutím na `Delete Library`.

Knihovny jsou řazeny do složek. V katalogu lze vyhledávat podle slov v názvu knihovny nebo konkrétní funkce nebo bloku.

???+ tip
    Knihovny WAGO můžete rychle vyhledat zadáním `WagoApp` nebo `WagoSys`.



## Proměnné retain, persistent

Standardní proměnné při jakémkoliv restartu ztrácejí svoji aktuální hodnotu. Deklarováním proměnné jako `RETAIN PERSISTENT` lze tomuto zabránit. Množství takových proměnných je omezeno dáno typem procesorové jednotky (velikosti remanentní paměti).

| Událost               | VAR       	   | VAR RETAIN       | VAR RETAIN PERSISTENT |
| -----------           | ---------------- | ---------------- | ---------------- |
| Neočekávané vypnutí   | :material-close: | :material-check: | :material-check: |
| Reset warm            | :material-close: | :material-check: | :material-check: |
| Reset cold            | :material-close: | :material-close: | :material-check: |
| Reset origin          | :material-close: | :material-close: | :material-close: |
| Nahrání projektu      | :material-close: | :material-close: | :material-check: |
| Online change         | :material-check: | :material-check: | :material-check: |

### Deklarace
Pro deklaraci persistentních proměnných slouží globální seznam. 

:material-mouse: V menu ++rbutton++ `Application` :material-arrow-right-bold-box-outline: `Add Object` :material-arrow-right-bold-box-outline: `Persistent Variables`.

### Záloha a obnovení

Pro zálohu seznamu persistent proměnných lze využít knihovnu `SysPlcCtrl23`.

Funkce `SysSaveRetains` uloží seznam do interní paměti PLC. Funkci je nutné volat ve zláštním tasku jako event. Exportovaný soubor `.ret` je umístěn ve složce `:/home/codesys_root/PlcLogic/Application/`.

Funkce `SysRestoreRetains` slouží pro obnovení ze souboru.

## Informace o kompilaci

Identický projekt v počítači i PLC ještě nezaručuje přihlášení (login) bez nutnosti přehrání projektu. To je možné pouze pokud existují informace o překladu projektu. 

Jedná se o soubor s příponou `.compileinfo`, který musí být ve stejném adresáři jako hlavní soubor projektu `.project`. 

Pokud tento soubor chybí (stává se typicky při zálohování nebo přenášení projektu), je při přihlášení zobrazeno upozornění s výzvou přehrát projekt v PLC. 