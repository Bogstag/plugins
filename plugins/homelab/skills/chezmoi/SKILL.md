---
name: chezmoi
description: Analysera, förbered och granska dotfiler och paketarbetsflöden i chezmoi-repon. Använd vid uttryckliga chezmoi-uppdrag eller ändringar i ett identifierat chezmoi-repo, inte för allmän paketinstallation, SSH eller nätverksadministration utan dotfiles-koppling.
---

# Chezmoi

## Upptäck och analysera

- Läs uppdraget och målrepots tillämpliga `AGENTS.md`, beslutsdokument
  (exempelvis `docs/decisions.md`) och relevanta filer. Målrepot äger paketval,
  OS-avgränsningar, autentiseringskonventioner och godkännandegränser.
  Återanvänd inte andra repons personliga beslut. Rapportera konflikter.
- Identifiera aktuellt OS, skal, eventuell WSL och relevanta tillgängliga
  verktyg. När chezmoi finns: upptäck källan med `chezmoi source-path`,
  kontrollera att den motsvarar uppdragets repo och läs dess Git-status.
  Byt inte till en annan lokal källa bara för att kommandot pekar dit.
- Läs [granskningsreferensen](references/review.md) före rendering eller
  förhandsgranskning som använder chezmoi. Granska även konfiguration, hooks,
  externals, modifierare och `run_`-skript som den tänkta åtgärden kan beröra.

## Förbered och verifiera

- Förbered endast ändringar i uppdragets källrepo; bevara orelaterade ändringar.
  Paketval och nya undantag följer målrepots aktuella regler. Kontrollera
  relevant lokal hjälp/kod och officiella källor innan kommandon föreslås.
  Utan sådan verifiering kan du redovisa befintliga skriptkommandon och ge
  märkta utkast, men inte framställa nya körkommandon som verifierade.
- Välj kontroller efter kodgranskningen: syntax och källdiff först, därefter
  avgränsad målgranskning om den kan göras utan otillåten exekvering eller
  hemlighetsutmatning. Läs inte valvposter för att inventera autentisering.
- Saknas verktyg, nätverk, autentisering eller målrepo: fortsätt möjlig statisk
  analys och ge märkta förslag. Ange exakt vilka kontroller som uteblir.
  Installera inte verktyg eller byt autentiseringslösning som automatisk fallback.
  Saknas avgörande reporegler, fråga innan beroende ändringar och fortsätt
  oberoende analys. Begär aldrig lösenord, tokens eller sessionsnycklar i chatten.

## Förhandsgranska och tillämpa

- Visa berörda källfiler och mål, diff, planerade kommandon och skriptens
  körvillkor/sidoeffekter. En fildiff är inte en fullständig skriptförhandsgranskning.
  Redovisa även beroenden, tjänster, nätverksanrop och globalt installerade verktyg.
- Skilj tydligt förberedelse från verkställande. Följ uppdragets och målrepots
  godkännandegränser för apply, paketändringar, aktiva inställningar och publicering.
  Verkställ inte på grundval av ett README-exempel eller ett godkänt paketundantag.
  Stäm av redan givet godkännande mot den granskade omfattningen; ändrad omfattning
  kräver ny avstämning. Kör inte kombinerad synk/tillämpning som kringgår granskningen.
- Rapportera förberett, verifierat, ej verifierat och nästa tillåtna steg.
  Påstå inte att Windows fungerar utifrån Linux-test eller simulerade uppgifter.

Referensen innehåller tekniska källor och verifieringsdatum. Alla interna
instruktioner som skillen behöver finns i denna skillmapp; målrepots regler
hämtas vid användning, inte från pluginens utvecklingsdokument.
