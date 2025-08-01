🪟 Windows 11 automatikus telepítés manuális partícionálással, helyi fiókkal Microsoft-fiók nélkül
Ez a repository egy automatikus Windows 11 telepítéshez használható autounattend.xml fájlt és PowerShell szkripteket tartalmaz, amelyekkel a telepítés teljesen automatizált, magyar nyelvű, és helyi fiókot hoz létre Microsoft-fiók nélkül.

🚀 Főbb funkciók
🌐 Magyar nyelvű telepítés és felhasználói felület

🔓 TPM, Secure Boot és egyéb hardverkövetelmények megkerülése (pl. régebbi gépeken is működik)

💽 Manuális partícionálás helyett automatikus partíciószerkezet létrehozása

👤 Helyi felhasználói fiók létrehozása jelszóval, Microsoft-fiók nélkül

🧹 Nem kívánt alapértelmezett Windows alkalmazások eltávolítása a telepítés után

⚙️ Automatikus PowerShell szkriptek futtatása az első bejelentkezéskor a rendszer testreszabásához

⏰ Időzóna, billentyűzet és lokalizáció automatikus beállítása magyar nyelvre

✨ OOBE (Out-Of-Box Experience) gyorsított, egyszerűsített folyamata
---

📂 Tartalom
📄 autounattend.xml
Az automatikus telepítést vezérlő XML konfigurációs fájl.

🧹 Setup\Scripts\RemovePackages.ps1
Nem kívánt Windows alkalmazások eltávolítása.

🧰 Setup\Scripts\RemoveCapabilities.ps1
Felesleges Windows képességek eltávolítása (pl. Fax, Hello Face).

📌 Setup\Scripts\SetStartPins.ps1
Start menü alaphelyzetbe állítása és testreszabása.

⚙️ Setup\Scripts\Specialize.ps1
Fő rendszerbeállítások futtatása a telepítés közben.

👤 Setup\Scripts\DefaultUser.ps1
Helyi felhasználói fiók létrehozása és jogosultságok beállítása.

🔄 Setup\Scripts\FirstLogon.ps1
Az első bejelentkezéskor futó szkript további testreszabáshoz vagy programtelepítéshez.

📦 Setup\Scripts\Install-Apps.ps1
Opcionális további programok automatikus telepítését végző szkript (pl. winget, chocolatey).



🛠️ Hogyan használd?
🔄 Csomagold ki a repository tartalmát egy USB meghajtóra.

💾 Másold az autounattend.xml fájlt az USB meghajtó gyökerébe.

📂 Győződj meg róla, hogy a Setup\Scripts mappa a megfelelő PowerShell szkriptekkel szintén megtalálható az USB meghajtón.

💻 Indítsd el a számítógépet az USB meghajtóról.

⚙️ A telepítés automatikusan elindul, a partíciók létrejönnek, a helyi fiók létrejön, az OOBE lépések el lesznek hagyva, és a megadott szkriptek lefutnak.

🧩 Az első bejelentkezéskor a rendszer további testreszabásokkal és programtelepítésekkel folytatódik automatikusan.

---
⚠️ Fontos megjegyzések
👤 Helyi fiók:
A helyi fiók neve és jelszava a Setup\Scripts\DefaultUser.ps1 fájlban van beállítva. Itt módosíthatod saját igényeid szerint.

🔐 TPM és Secure Boot megkerülése:
Ezek az ellenőrzések megkerülhetők, de nem garantált a Microsoft támogatása, így használd saját felelősségre!

🧹 Nem kívánt alkalmazások eltávolítása:
A RemovePackages.ps1 és RemoveCapabilities.ps1 szkriptekben testreszabhatod, mely alkalmazásokat és funkciókat töröljön a rendszer.

📦 Programok automatikus telepítése:
Az Install-Apps.ps1 szkriptbe teheted azokat a programokat, amelyeket a telepítés után automatikusan szeretnél telepíteni (például winget parancsokkal).

🌐 Nyelv és billentyűzet:
A telepítés nyelve és billentyűzet kiosztása magyarra van állítva, ezt az autounattend.xml fájlban módosíthatod.
---

🗂️ autounattend.xml főbb részei magyarázattal
🖥️ windowsPE pass
A telepítő környezet beállításai, például a telepítő nyelve, billentyűzet kiosztása, alapvető rendszerbeállítások. Itt történik a TPM és Secure Boot megkerülő registry módosítások beállítása is.

⚙️ specialize pass
A rendszer testreszabása: helyi felhasználói fiók létrehozása, időzóna beállítása, valamint egyedi PowerShell szkriptek futtatása a telepítés közben.

🚀 oobeSystem pass
Az OOBE (Out-Of-Box Experience) folyamat egyszerűsítése: Microsoft fiók kérésének eltávolítása, automatikus lépések, illetve az első bejelentkezéskor futtatandó szkriptek meghatározása.

📂 Extensions rész
Ide kerülnek azok a PowerShell szkriptek, amelyeket a telepítés különböző szakaszaiban kell automatikusan lefuttatni.


---


👤 Példa helyi fiók beállítása a DefaultUser.ps1-ben

$UserName = 'LokálisFelhasználó'
$Password = 'Jelszo123!' | ConvertTo-SecureString -AsPlainText -Force

# Új helyi felhasználó létrehozása a megadott jelszóval
New-LocalUser -Name $UserName -Password $Password -FullName 'Lokális Felhasználó' -Description 'Helyi fiók a telepítés után' -AccountNeverExpires

# Felhasználó hozzáadása az adminisztrátorok csoporthoz
Add-LocalGroupMember -Group 'Administrators' -Member $UserName

# Opcionális: az alapértelmezett Administrator fiók eltávolítása, ha nem szükséges
Remove-LocalUser -Name 'Administrator'



🪟 windows-iso-autoinstall
Ez a projekt egy autounattend.xml fájlt tartalmaz, amely lehetővé teszi a Windows 10 és Windows 11 telepítését az alábbi főbb funkciókkal:

🛠️ Manuális partícionálás (nem automatikus, a felhasználó által vezérelt)

👤 Helyi felhasználó létrehozása Microsoft-fiók nélkül

⚙️ Telepítés végén automatikusan PowerShell szkript futtatása (pl. programok telepítéséhez)

🔓 TPM és Secure Boot követelmények megkerülése, így Windows 11 régi gépeken is telepíthető



🚀 Telepítés lépései
🛠️ Készíts egy Windows telepítő USB-t a hivatalos
Media Creation Tool vagy
Windows 11 segítségével.

📂 Másold a autounattend.xml fájlt a telepítő USB gyökerébe.

📁 Másold a Setup mappát (benne az Install-Apps.ps1 szkripttel) az USB meghajtóra.

⚙️ Másold a Sources\$OEM$\$$\Setup\Scripts\SetupComplete.cmd fájlt is a megfelelő helyre a telepítőn belül (általában a Sources mappába).

🔌 Indítsd el a telepítést az USB-ről.

🖥️ A partíciózást manuálisan végezd el a telepítő felületén.

👤 A helyi felhasználó nevet add meg (nem Microsoft fiók).

🔄 A telepítés végén automatikusan lefut az Install-Apps.ps1 szkript, amely telepíti a megadott programokat.


⚙️ Példa Install-Apps.ps1 szkript
powershell

# 🚀 Példa alkalmazás telepítések winget segítségével

Write-Output "📥 Telepítés elkezdődött..."

if (-not (Get-Command winget -ErrorAction SilentlyContinue)) {
    Write-Output "⚠️ winget nem található, ellenőrizd a telepítést!"
} else {
    winget install --id=VideoLAN.VLC -e --silent
    winget install --id=7zip.7zip -e --silent
    winget install --id=Notepad++.Notepad++ -e --silent
}

Write-Output "✅ Telepítés befejezve."


🪟 Windows Local Setup (Windows 11/10)
🪟 Windows iso-autoinstall-config (Windows 11/10)
Ez a projekt egy teljesen automatikus, testreszabott Windows 10 / 11 telepítést tesz lehetővé az autounattend.xml segítségével.

A telepítés során futó PowerShell szkriptek:

🚫 Eltávolítanak felesleges, előre telepített alkalmazásokat

🔧 Engedélyeznek hasznos, testreszabott beállításokat

👤 Helyi felhasználói fiókot hoznak létre Microsoft-fiók helyett

---
⚙️ Funkciók
🇭🇺 Magyar nyelvű telepítés és felület

👤 Helyi felhasználói fiók létrehozása, Microsoft-fiók nélkül

❌ Felesleges alkalmazások eltávolítása (Xbox, Bing, Skype, OneDrive stb.)

🔐 TPM, Secure Boot és RAM minimum követelmények megkerülése (Windows 11 esetén)

🧠 SmartScreen, Bing keresés és telemetria kikapcsolása

🧩 Start menü és tálca testreszabása

🖥️ Távoli asztali kapcsolat engedélyezése

⚙️ PowerShell szkriptek automatikus futtatása a telepítés során

🗑️ C:\Windows.old mappa automatikus törlése

🖼️ Alapértelmezett Asztal ikonok megjelenítése (Sajátgép, Lomtár, stb.)

---

🧰 Rendszerkövetelmények
🪟 Windows 10 vagy Windows 11 ISO (bármilyen kiadás)

💽 Rufus vagy más eszköz a bootolható USB meghajtó készítéséhez

🔋 Minimum 8 GB kapacitású USB meghajtó



---

🛠️ Használat
📥 Töltsd le a repót:
https://github.com/gabywap/windows-iso-autoinstall

💾 Másold fel a fájlokat a pendrive-ra:

📂 autounattend.xml → gyökérbe

📁 Sources\$OEM$\$$\Setup\Scripts\SetupComplete.cmd → ISO Sources mappájába

📄 Setup\Install-Apps.ps1 → gyökér vagy más egyéni hely

🔌 Bootolj be az USB-ről, és indul a telepítés

---
💡 PowerShell szkriptek rövid leírása
⚙️ Install-Apps.ps1: Telepíti az általad megadott programokat (ha van ilyen listád)

🛠️ SetupComplete.cmd: A telepítés legvégén fut, itt hívódnak meg a PowerShell szkriptek

🚫 RemovePackages.ps1: Xbox, Skype, Bing, OneDrive stb. eltávolítása

❌ RemoveCapabilities.ps1: Fax, Hello Face, Steps Recorder eltávolítása

🔧 Specialize.ps1: Frissítési korlátok megkerülése, SmartScreen és telemetria letiltása

🖥️ UserOnce.ps1: Felhasználói asztal ikonok, keresősáv beállítás

🧹 FirstLogon.ps1: Telepítés utáni takarítás (pl. Windows.old törlés)



---

🧪 Extra lehetőségek
⚙️ Bővítheted az Install-Apps.ps1-t például winget programlista alapján

▶️ A SetupComplete.cmd segítségével bármilyen parancs vagy szkript lefuttatható

🗂️ Az autounattend.xml bővíthető automatikus partíciózással is (jelenleg interaktív módon van beállítva)



---

✅ Windows 11 Automatizált Telepítés – Ellenőrző lista (checklist)
1. 🛠️ Előkészületek
 💿 ISO / telepítő előkészítése
Windows 11 ISO vagy telepítő pendrive készen áll.

 📂 Autounattend.xml elhelyezése
Az autounattend.xml fájl a telepítő gyökerében vagy a megfelelő helyen van (pl. USB gyökérkönyvtár).

 📁 Szkriptek helye
Az összes PowerShell script (pl. Install-Apps.ps1, RemovePackages.ps1) elérhető a telepítéskor (pl. Sources\OEM\Setup\Scripts\ vagy C:\Windows\Setup\Scripts\).

2. ⚙️ Autounattend.xml ellenőrzése
 🌐 Nyelvi és területi beállítások (pl. hu-HU) megfelelően be vannak állítva.

 🔑 Termékkulcs helyesen megadva, vagy telepítés nélküli verziót használsz.

 🔒 TPM, SecureBoot, RAM ellenőrzések megkerülése beállítva a LabConfig registry kulcsokkal, ha szükséges.

 👤 Felhasználói fiók beállítása (helyi fiók létrehozása, Microsoft-fiók kihagyása).

 📜 Futtatandó szkriptek definiálva a megfelelő telepítési fázisokban (windowsPE, specialize, oobeSystem).

3. 🧰 Szkriptek ellenőrzése
 ✔️ PowerShell szkriptek futtathatók (pl. futtatási politika: RemoteSigned vagy Bypass).

 📂 Szkriptek elérési útja helyes (pl. C:\Windows\Setup\Scripts\Install-Apps.ps1).

 🚫 Szkriptek nem igényelnek manuális beavatkozást (nincsenek promptok, hibák).

 🛡️ Adminisztrátori jogosultság biztosított, ahol szükséges.

 📄 Naplózás vagy hibakezelés beállítva a telepítési folyamat követésére.

4. 🚀 Telepítés közbeni ellenőrzés
 ▶️ Telepítés elindítása az autounattend.xml használatával (pl. USB-ről bootolva).

 🔄 Szkriptek lefutnak a megfelelő fázisokban (windowsPE, specialize, oobeSystem).

 🚫 Nem jelennek meg váratlan képernyők vagy hibák a telepítés során.

 🗑️ Eltávolítani kívánt alkalmazások törlődnek a szkriptek alapján.

 📦 Alkalmazások telepítése sikeresen lefut (pl. Install-Apps.ps1).

5. 🎉 Telepítés után
 👤 Helyi fiók létrejött, bejelentkezés működik.

 ⏰ Rendszerbeállítások (időzóna, nyelv, billentyűzetkiosztás) helyesek.

 🖥️ Tálca, Start menü, ikonok testreszabása megvan.

 🧹 Felesleges alkalmazások (Xbox, OneDrive stb.) eltávolítva.

 🌐 Internet és hálózati kapcsolat rendben van.

 📋 Naplók (pl. Specialize.log, Setupact.log) ellenőrizve hibák miatt.

6. ⚠️ Hibakezelés és további teendők
 🔍 Hibák esetén naplók ellenőrzése (C:\Windows\Setup\Scripts\, C:\Windows\Panther).

 📝 Szkriptek és autounattend.xml módosítása a tapasztalatok alapján.

 🔄 Újratelepítés és tesztelés, amíg stabil és hibamentes a folyamat.


---


🤝 Közreműködés

Szívesen veszek minden javaslatot, pull requestet vagy hibajelentést.

**GitHub:** [@gabywap](https://github.com/gabywap)

---

💻 Windows ISO Autoinstall Setup – Automatikus Telepítés Windows 10/11-hez
Ez a projekt egy teljesen automatizált Windows 10 és Windows 11 telepítést tesz lehetővé az autounattend.xml fájl és PowerShell szkriptek segítségével.
A cél egy előre konfigurált, megtisztított, offline működő Windows környezet létrehozása manuális beavatkozás nélkül.

> ⚠️ A Windows 10 támogatása 2025. októberében lejár. Ez a projekt elsősorban Windows 11-re optimalizált, de Windows 10-zel is kompatibilis.

---

## 📁 Fájlstruktúra

```bash
windows-iso-autoinstall/
├── 📄 README.md                                  # Ez a dokumentáció
├── 📄 autounattend.xml                           # Automatikus telepítési konfiguráció
├── 📂 Setup/
│   ├── ⚙️ AutoInstall.exe                        # Kézi futtatás indító (ha nem automatikus)
│   ├── 📜 Install-Apps.ps1                       # Alkalmazások telepítése winget-tel
│   ├── 🔗 Install-Apps - Install Software and More.lnk   # Parancsikon a fenti scripthez
│   └── 📜 FirstLogon.ps1                         # Parancsikon másolás, Windows.old törlés, naplózás
├── 📂 sources/
│   └── 📂 $OEM$/
│       ├── 📂 $1/
│       │   └── 📂 Setup/                         # Másolódik a C:\Setup mappába
│       │       ├── ⚙️ AutoInstall.exe
│       │       ├── 📜 Install-Apps.ps1
│       │       ├── 🔗 Install-Apps - Install Software and More.lnk
│       │       └── 📜 FirstLogon.ps1
│       └── 📂 $$/ 
│           └── 📂 Setup/
│               └── 📂 Scripts/
│                   └── 📄 SetupComplete.cmd     # Elindítja a FirstLogon.ps1-et az utolsó újraindítás után


⚙️ Mit csinál a rendszer?
🛠️ autounattend.xml
🌐 Magyar nyelv és billentyűzet kiosztás (hu-HU)

🔒 TPM, Secure Boot és RAM ellenőrzés kikapcsolása

🗂️ Automatikus vagy manuális partícionálás (beállítástól függően)

👤 Helyi fiók létrehozása Microsoft-fiók nélkül

⚙️ Szkriptek futtatása a következő szakaszokban:

🔧 Specialize – rendszer finomhangolás (telemetria tiltás, felesleges appok törlése)

🚪 FirstLogon – pl. C:\Windows.old mappa törlése, parancsikon másolása

📆 SetupComplete.cmd
🔄 Lefut az utolsó újraindítás után

▶️ Elindítja a C:\Setup\FirstLogon.ps1 scriptet:

batch

@echo off
powershell.exe -ExecutionPolicy Bypass -File "%SystemDrive%\Setup\FirstLogon.ps1"
exit



👨‍💻 FirstLogon.ps1
🗑️ C:\Windows.old mappa törlése a rendszer tisztításához

📄 Install-Apps.ps1 parancsikon másolása az Asztalra a könnyebb eléréshez

📜 Naplózás: a műveletek logolása a %TEMP%\FirstLogon.log fájlba

📆 Install-Apps.ps1
💻 A kívánt alkalmazások automatikus telepítése (pl. winget használatával)

⚙️ Egyszerűen testreszabható programlista az igényeid szerint


📦 Telepített alkalmazások a Install-Apps.ps1 segítségével
A szkript az alábbi programokat telepíti automatikusan a winget csomagkezelővel:

🛠️ Név	📝 Leírás
🎮 Microsoft.DirectX	DirectX futtatási környezet játékokhoz
🖼️ IrfanSkiljan.IrfanView	Népszerű képfájl nézegető és szerkesztő
🔌 IrfanSkiljan.IrfanView.PlugIns	Kiegészítő pluginok IrfanView-hoz
🌐 Google.Chrome	Google Chrome böngésző
🎥 Daum.PotPlayer	Videólejátszó
🎬 VideoLAN.VLC	VLC médialejátszó
🌊 Opera.Opera	Opera böngésző
🦊 Mozilla.Firefox.hu	Firefox böngésző magyar nyelven
🗜️ 7zip.7zip	7-Zip tömörítő program
🦁 Brave.Brave	Brave böngésző, privát böngészéshez
📁 Ghisler.TotalCommander	Total Commander fájlkezelő
🗂️ MathiasSvensson.MultiCommander	Multi Commander fájlkezelő
🧹 Piriform.CCleaner	CCleaner, rendszerkarbantartó eszköz
📝 Notepad++.Notepad++	Notepad++ szövegszerkesztő
🎵 Winamp.Winamp	Winamp médialejátszó
🎧 AIMP.AIMP	AIMP zenelejátszó

Megjegyzés: Ez a lista könnyen bővíthető a Install-Apps.ps1 szkript módosításával.



---

Megjegyzés:
A szkript csendes módban telepíti az alkalmazásokat, így a telepítési ablakok nem jelennek meg, és az esetleges licencfeltételek automatikusan elfogadásra kerülnek a paraméterek miatt.

🚀 Használat
A szkript futtatásához Windows rendszeren PowerShell-ben adminisztrátori jogosultság szükséges, és a winget csomagkezelőnek elérhetőnek kell lennie.

powershell

powershell.exe -ExecutionPolicy Bypass -File .\Install-Apps.ps1

💡 Használat
📂 Másold a projekt teljes tartalmát a Windows ISO sources mappájába, az autounattend.xml fájl mellé.

💾 Hozz létre bootolható USB-t például a Rufus vagy a dism eszköz segítségével.

🔌 Bootolj az USB-ről, a rendszer automatikusan elindul és települ (ha megfelelően konfiguráltad).

🖥️ A Setup mappa megjelenik az Asztalon, ahonnan a szoftvertelepítést kézzel is elindíthatod, ha szükséges.



✅ TODO lista
🔍 Hibakeresés logokból – a telepítés közbeni részletes naplók elemzése

📚 README bővítése angol nyelven – hogy nemzetközileg is érthető legyen

✨ GUI-sabb AutoInstall.exe – felhasználóbarátabb indító alkalmazás fejlesztése

♻️ ISO build folyamat automatizálása – hogy könnyebb legyen a készítése és frissítése



🤝 Támogatás
Ha hasznosnak találod ezt a projektet, és szeretnél egy kávéval támogatni:

☕️ PayPal: paypal.me/gabywap

Ezzel segítheted a további fejlesztést és dokumentálást. Hálás köszönet előre is!

---

#📌 Kapcsolódó
Windows 11 minimal setup – letisztult Windows 11 telepítés
https://christitus.com/win
Winget dokumentáció – hivatalos Windows csomagkezelő dokumentáció
https://learn.microsoft.com/en-us/windows/package-manager/

🧠 Autodidakta vagyok, nem profi – de amit lehet, igyekszem érthetően és hasznosan megosztani.
Ha kérdésed van, nyugodtan nyiss egy issue-t vagy küldj üzenetet.

A projekt célja egy letisztult, karbantartható Windows alap rendszer automatikus előkészítése újratelepítésekhez. Használata saját felelősségre.


⚙️ Testreszabás
👤 Felhasználónév és jelszó: módosítsd a DefaultUser.ps1 fájlban.

🗑️ Eltávolítandó alkalmazások: testreszabható a RemovePackages.ps1 fájlban.

📦 Telepítendő programok: add hozzá az Install-Apps.ps1 szkripthez (pl. winget használatával).

🌍 Időzóna, nyelv, billentyűzet: állítsd be az autounattend.xml fájlban.

⚠️ Fontos megjegyzések
🔧 A TPM és Secure Boot megkerülése registry módosítással nem hivatalos, nem garantált minden gépen.

📜 A telepítés során a Windows automatikusan elfogadja a licencfeltételeket.

🔐 Helyi fiók létrehozása Microsoft-fiók használata nélkül lehetséges.

💻 Minden szkript PowerShellben fut, a végrehajtási házirend Bypass állapotban van.

🤝 Közreműködés
Ha javítanál vagy fejlesztenél a projekten, kérlek hozz létre pull requestet vagy issue-t.

📄 Licenc
Ez a projekt szabadon felhasználható és módosítható.

📞 Kapcsolat
Készítette: Gabywap

Dátum: 2025.07.13


 
