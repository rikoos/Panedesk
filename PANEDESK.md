# Panedesk: projectcontext voor Claude Code

Panedesk is Ricks fork van Desktop Frames+ (limbo666, MIT; voortzetting van BirdyFences),
bedoeld als gratis alternatief voor Stardock Fences 6. Fences 6 is het functionele uitgangspunt.
Projectplan: https://claude.ai/artifact/H4hHiM6wSTU9j1Fci5Ywqc

## Status
- Fase 0 afgerond (17 nov 2026): DesktopPossible viel af (frames onzichtbaar, geen
  icoon-frame bij eerste start). Desktop Frames+ werkte wel in dezelfde VM. Dit is de basis.
- Remote `upstream` = github.com/limbo666/DesktopFramesPlus. Nog geen `origin` (GitHub-fork volgt).
- Oude DesktopPossible-clone staat in ~/projects/panedesk-dp-archief (alleen ter referentie;
  MIT, losse verbeteringen mogen worden overgenomen met bronvermelding).

## Bouwen
- Het project staat in `Code/Desktop Frames/` en gebruikt nog `<COMReference>`: daardoor
  bouwt het NIET met de dotnet-CLI (MSB4803), ook niet onder Linux.
- Eerste technische taak: COM-interop omzetten naar late binding
  (Type.GetTypeFromProgID + dynamic), zoals DesktopPossible deed, en
  `EnableWindowsTargeting=true` zetten. Daarna bouwt het op Rikoosai.
- Tot die tijd: test met de officiële release (C:\DFPlus in de VM).

## Waar wat draait
- Code, Claude Code, builds: Rikoosai (Fedora), map ~/projects/panedesk.
- Bouwen kan onder Linux (`dotnet build src/DesktopPossible.sln`), draaien en
  testen alleen op Windows: de VM `panedesk-win11` op Rikoosai.
- Ricks eigen bureaublad (Rikoosdesktop): alleen SSH-terminal, plus later een
  geïnstalleerde release. Niets anders installeren of wijzigen op Rikoosdesktop.

## Test-VM
- Naam `panedesk-win11` (Windows 11 Pro), vast IP 192.168.122.103, gebruiker `Rikoos` (beheerder).
- Vanaf Rikoosai: `ssh panedesk-vm` (sleutel, geen wachtwoord); de shell is Windows PowerShell 5.1.
- Bestanden naar de VM: `scp <bestand> panedesk-vm:` ; app draaien kan met de gebouwde output uit `.build/`.
- Rick kijkt mee via Extern bureaublad (profiel "Panedesk VM" in Windows Terminal op Rikoosdesktop).
- VM starten/stoppen: `virsh -c qemu:///system start|shutdown panedesk-win11`.

## Regels
- Communiceer in het Nederlands, beknopt, zonder em-dashes.
- Werk per taak op een eigen branch; push of open een PR alleen als Rick erom vraagt.
- Nooit bestanden van de gebruiker verplaatsen of verwijderen zonder dat de
  gebruiker dat expliciet doet; iconen moeten na crash of afsluiten terugkomen.
- Geen code, iconen, teksten of namen van Stardock Fences overnemen.
- Fork-voorwaarden (MIT): LICENSE met alle copyrightregels behouden
  (HAKANKOKCU, LIMBO666, DevPossible) en Panedesk erbij zetten;
  THIRD-PARTY-NOTICES.md bijwerken bij nieuwe pakketten; credits in README.
- Model: standaard Sonnet. Alleen Opus als Sonnet aantoonbaar vastloopt.
- Lokale modellen (Ollama op Rikoosai) mogen voor eenvoudige taken:
  uitleg, vertalingen, commit-berichten.
