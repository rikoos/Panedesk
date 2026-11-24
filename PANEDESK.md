# Panedesk: projectcontext voor Claude Code

Panedesk is Ricks fork van Desktop Frames+ (limbo666, MIT; voortzetting van BirdyFences),
bedoeld als gratis alternatief voor Stardock Fences 6. Fences 6 is het functionele uitgangspunt.
Projectplan: https://claude.ai/artifact/H4hHiM6wSTU9j1Fci5Ywqc

## Status
- Fase 0 afgerond (17 nov 2026): DesktopPossible viel af (frames onzichtbaar, geen
  icoon-frame bij eerste start). Desktop Frames+ werkte wel in dezelfde VM. Dit is de basis.
- Remotes: `origin` = github.com/rikoos/Panedesk (GitHub-fork, openbaar),
  `upstream` = github.com/limbo666/DesktopFramesPlus, `rikoosai` = oude kopie op Rikoosai.
- Referentie: ..\referentie-desktoppossible (DesktopPossible, MIT; losse verbeteringen
  mogen worden overgenomen met bronvermelding). Testlijst: docs\panedesk-testlijst.md daarin.

## Waar wat draait (sinds 24 nov 2026)
- Werkmap: C:\Claudecode\Fences op Rikoosdesktop (Windows).
  - `Panedesk\`: deze repository. Claude Code draait hier.
  - `referentie-desktoppossible\`: referentiecode.
  - `omgeving\`: scripts voor de test-VM (draaien op Rikoosai).
- Bouwen en draaien: lokaal op Rikoosdesktop met de .NET 10 SDK.
- Testen bij voorkeur in de VM, niet op Ricks eigen bureaublad: de app verbergt
  bureaubladiconen en dat moet eerst veilig blijken.

## Bouwen
- Het project staat in `Code/Desktop Frames/` en gebruikt nog `<COMReference>`: daardoor
  bouwt het NIET met de dotnet-CLI (MSB4803).
- Eerste technische taak: COM-interop omzetten naar late binding
  (Type.GetTypeFromProgID + dynamic), zoals DesktopPossible deed. Daarna bouwt het met
  `dotnet build` en `dotnet publish -r win-x64`.
- Tot die tijd: test met de officiële release (C:\DFPlus in de VM).

## Test-VM
- Naam `panedesk-win11` (Windows 11 Pro) op Rikoosai, vast IP 192.168.122.103, gebruiker `Rikoos`.
- Vanaf Rikoosdesktop via Rikoosai: `ssh rikoosai "ssh -n panedesk-vm '<PowerShell-commando>'"`.
  Bestanden: eerst `scp <bestand> rikoosai:/tmp/`, dan op Rikoosai `scp /tmp/<bestand> panedesk-vm:`.
- GUI-apps via SSH starten in Ricks sessie met een geplande taak (`schtasks /create ... /it`),
  anders blijven ze onzichtbaar.
- Rick kijkt mee via Extern bureaublad (profiel "Panedesk VM" in Windows Terminal).
- VM starten/stoppen op Rikoosai: `virsh -c qemu:///system start|shutdown panedesk-win11`.

## Regels
- Communiceer in het Nederlands, beknopt, zonder em-dashes.
- Werk per taak op een eigen branch; push of open een PR alleen als Rick erom vraagt.
- Nooit bestanden van de gebruiker verplaatsen of verwijderen zonder dat de
  gebruiker dat expliciet doet; iconen moeten na crash of afsluiten terugkomen.
- Geen code, iconen, teksten of namen van Stardock Fences overnemen.
- Fork-voorwaarden (MIT): LICENSE met alle copyrightregels behouden
  (HAKANKOKCU, LIMBO666) en Panedesk erbij zetten; bij overgenomen DesktopPossible-code
  ook DevPossible vermelden; credits in README.
- Model: standaard Sonnet. Alleen Opus als Sonnet aantoonbaar vastloopt.
