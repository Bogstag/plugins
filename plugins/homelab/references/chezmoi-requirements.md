# Krav på första chezmoi-skillen

Status: kravunderlag, 2026-09-09. Implementerat lokalt i Homelab 0.2.0;
se [verifieringsrapport](chezmoi-validation.md). Detta är utvecklingsunderlag,
inte en körreferens som den installerade skillen behöver läsa.

## Syfte och aktivering

Hjälp användaren analysera, förbereda och granska dotfiler och paketarbetsflöden
i ett chezmoi-källrepo. Aktivera vid uttryckliga chezmoi-uppdrag eller arbete
med ett identifierat chezmoi-repo. En allmän SSH-, nätverks- eller paketfråga
utan koppling till dotfiles ska inte ensam aktivera skillen.

Första versionen ska kunna leverera analys och patchförslag utan att lokala
verktyg finns. Den ska inte installera beroenden för att kunna börja hjälpa.

## Regelkällor och verktyg

- Läs användarens aktuella uppdrag, tillämpliga AGENTS.md och målrepots
  beslutsdokument innan implementation. Konflikter ska redovisas, inte döljas.
- För Bogstag/dotfiles finns paketval, Bitwarden-förutsättningar och
  godkännandegränser i målrepots `docs/decisions.md`; se
  [regelägande och historik](../../../docs/decisions.md). Återge inte en egen
  permanent kopia av dessa regler i skillen.
- Identifiera OS, skal, eventuell WSL och tillgängliga kommandon. Använd
  `chezmoi source-path` för lokal källkatalog och verifiera Git-repots identitet.
  Varken ett användarnamn, en hemkatalog eller en Bitwarden-socket ska hårdkodas.
- Chezmoi och Git behövs för fullständig lokal käll-/målgranskning. OS-specifika
  paketeringsverktyg behövs endast när uppgiften berör dem. `gh` behövs för
  relevanta GitHub-flöden, inte all lokal redigering.
- Bitwarden-verktyg och agent ska upptäckas per arbetsflöde. Ett verktygs
  närvaro bevisar inte autentisering. `bw` och `bws` har olika roller; det
  senare får inte bli ett generellt beroende. Läs inte ut hemligheter för
  inventering och kopiera inte sessionsvärden till rapporter eller exempel.
- Om verktyg eller målrepo saknas: analysera tillgängliga filer, ge tydligt
  märkta förslag/manuella kontroller och ange vad som inte verifierats. Be om
  nödvändigt regelunderlag innan beroende ändringar; gissa inte lokala regler.

## Arbetsgång

1. Fastställ uppdragets mål och gräns mellan förberedelse och verkställande.
   Läs regler, inventera relevanta filer och `git status`; bevara andra ändringar.
2. Upptäck körmiljö och källrepo. Läs mallar, ignore-regler, installationsskript,
   modifierare och eventuell hook-/externkonfiguration före rendering eller
   kontroller. Kartlägg externa anrop och risk för hemlighetsutmatning.
3. Verifiera relevanta gränssnitt via lokal kommandokod/hjälp och officiell
   dokumentation. Läs hjälp först när det är klarlagt att den inte verkställer
   en ändring. Skilj användaruppgifter, lokala fynd och ej provade antaganden.
4. Förbered minsta relevanta källändring inom uppdraget. Följ målrepots
   OS-avgränsningar och paketregler. Ett nytt undantag ska förankras enligt
   målrepots beslut innan det införs.
5. Kontrollera syntax, interna länkar och diff. Använd avgränsade chezmoi-
   kontroller endast när mall-/hookanalysen visar att de är lämpliga.
   En generell `diff`, `cat` eller mallrendering kan hämta valvdata; saknad
   autentisering får inte kringgås. `--skip-secrets` ersätter inte kodgranskning.
6. Leverera en förhandsgranskning som innehåller filer och mål, föreslagna
   kommandon, paket/beroenden, skriptens körvillkor och sidoeffekter, tjänster,
   externa anrop samt eventuella aktiva säkerhets-/nätverksändringar.
7. Håll verkställande bakom målrepots uttryckliga godkännandegräns. Godkännande
   ska avse den aktuella förhandsgranskningen; förberedelse är inte tillämpning.
   Undvik kombinerade synk-/apply-kommandon som hoppar över granskningen.
8. Rapportera vad som förbereddes, verifierades, väntar på godkännande eller
   inte kunde provas. Ingen faktisk tillämpning eller publicering ingår i
   framtagandet av denna första skill.

## Förväntade resultat

Ett konkret uppdrag ska ge relevant patch eller förslag, redovisning av
verifieringsmiljö och källor, en förhandsgranskning inklusive skript, samt
precis status för nästa åtgärd. Fullständig systemkompatibilitet får inte
påstås utifrån enbart giltig syntax eller ett lyckat installationstillstånd.
Inga nya hemligheter, oavsiktliga målposter eller paketundantag ska skapas.

## Provfall inför implementation

Detta är acceptansfall, inte genomförda funktionstester. Använd isolerade
testrepon och simulerade kommandon; paket, valv och aktiva inställningar ska
inte ändras av testerna.

| Fall | Underlag | Förväntat beteende |
| --- | --- | --- |
| Dotfilsändring på Omarchy | Begär en liten Starship-ändring i ett källrepo med befintlig orelaterad diff och installationsskript. | Upptäck källa och regler; bevara diffen; förbered endast avsedd fil. Visa måländring och berörda skript/sidoeffekter. Tillämpa inte före uttryckligt godkännande enligt målrepot. |
| Scoop-paket på Windows | Simulerad Windows/PowerShell-miljö, önskat paket finns i godkänd Scoop-källa. | Verifiera manifest/namn och förbered OS-specifik källändring. Visa beroenden och installationssteg. Ingen WinGet-fallback och ingen installation utan verkställandegodkännande. |
| Nytt WinGet-undantag | Önskat .NET-relaterat paket saknar bekräftad Scoop-lösning; ingen fastställd ID/version. | Utred alternativen och officiell paketinformation. Föreslå exakt undantag och fråga innan det införs. Hitta inte på ID eller behandla .NET-exemplet som generellt tillstånd. Installation kräver separat godkännande. |
| Bitwarden-autentisering saknas | Mall använder `bitwarden`; `bw` finns men användbar session saknas. | Fortsätt statisk analys där det går. Markera rendering som overifierad. Be användaren hantera autentisering lokalt när den behövs; fråga inte efter tokens, byt inte till `bws` och ändra inte agenten. |
| Ingen lokal chezmoi | Endast ett läsbart repo/utdrag finns, ingen chezmoi eller tillgång till datorns målstate. | Läs regler och ge analys/patchförslag. Ange att source-path, rendering, mål-diff och tillämpning inte verifierats. Installera inte chezmoi automatiskt och anta inte en lokal katalog. |
| Omarchy-gränssnitt saknas eller avviker | Omarchy-uppdrag men förväntat kommando kan inte verifieras. | Stanna före paketåtgärden, undersök officiella gränssnitt och redovisa avvikelsen. Anropa inte pacman/yay direkt som reservlösning. Fortsätt oberoende analys. |

## Tekniska källor och verifieringsgräns

Kontrollerat 2026-09-09 genom officiell dokumentation och lokal kodläsning.
Detaljer och evidens finns i målrepots beslut; källorna nedan förklarar
skillens generella arbetsgång, inte användarens personliga policy:

- [chezmoi source-path](https://www.chezmoi.io/reference/commands/source-path/)
  och [managed](https://www.chezmoi.io/reference/commands/managed/): upptäckt och målposter.
- [chezmoi ignore](https://www.chezmoi.io/reference/special-files/chezmoiignore/):
  matchning på målvägar, inklusive dokumentationsundantag.
- [chezmoi scripts](https://www.chezmoi.io/user-guide/use-scripts-to-perform-actions/):
  `run_once` per unikt innehåll, `run_onchange` vid ändring och dry-run utan skriptkörning.
  Sidorna lästes i chezmois officiella GitHub-dokumentationskälla.
- [Omarchy pkg-add](https://github.com/basecamp/omarchy/blob/master/bin/omarchy-pkg-add):
  jämförd med lokal wrapper och hjälp. Kommandot verifierades utan installation.
- [Bitwarden CLI](https://bitwarden.com/help/cli/),
  [Secrets Manager CLI](https://bitwarden.com/help/secrets-manager-cli/) och
  [SSH Agent](https://bitwarden.com/help/ssh-agent/): olika autentiseringsytor.
- [Scoop](https://github.com/ScoopInstaller/Scoop) och
  [WinGet install](https://github.com/MicrosoftDocs/windows-dev-docs/blob/docs/hub/package-manager/winget/install.md):
  paketmanifest, identifiering och exakt paketval; inga Windows-paket kördes.

Lokalt har bara källkatalog, relevanta filer, kommandogränssnitt och
dokumentationsundantag undersökts. Varken hemligheter, agentnycklar eller
Windows-miljön har lästs ut/testats. Återstående miljöval löses per uppdrag;
inga ytterligare användarbeslut blockerar att skriva första skillen.
