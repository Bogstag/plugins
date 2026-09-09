# Granskning, begränsningar och källor

Läs före chezmoi-baserad förhandsgranskning. Detta är tekniskt underlag;
användarens paket- och godkännandepolicy ska läsas i det aktuella målrepot.

## Förhandsgranskning utan oavsiktlig verkställning

Läs källan till relevanta mallar och modifierare, `run_*`, `.chezmoiscripts`,
`.chezmoiignore`, externals och kommandokonfiguration/hooks innan kontroller.
Kontrollera särskilt `output`/andra processanrop och hemlighetsfunktioner.
Även `diff`, `status`, `cat` och mallrendering kan behöva beräkna målstate och
anropa externa verktyg. Undvik breda kommandon över hemlighetsbärande mallar.
Logga inte miljövariabler, valvresultat eller renderade hemligheter.

`--skip-secrets` och `--refresh-externals=never` kan begränsa vissa kontroller
när installerad version stöder dem, men är inte en sandbox för godtyckliga
mallkommandon eller hooks. Välj statisk granskning när säker rendering inte
kan fastställas. Håll eventuella testfall isolerade med egna source, destination,
config, cache och persistent state; använd inga verkliga valv eller authdata.

Granska skript som kod, kör dem inte för att se vad de gör:

- `run_` körs vid tillämpning; `before_`/`after_` påverkar ordningen.
- `run_once_` registreras per unikt innehåll, inte bara filnamn. Ändrat innehåll
  kan köras igen. `run_onchange_` körs när innehållet ändrats sedan lyckad körning.
- Dry-run kör inte chezmois scripts, men mallutvärdering och annan konfiguration
  behöver fortfarande granskas. Skripttext förutsäger inte alla externa effekter.
- Redovisa installations-/uppdateringsanrop, tjänstestart, katalogskapande,
  globala ändringar och nätverk. Är körhistorik okänd, märk körningen som möjlig,
  inte säkert genomförd eller säkert överhoppad. Rensa inte körhistorik för test.

## Miljö och verktyg

Upptäck verktyg med körmiljöns tillgängliga funktioner, exempelvis `command -v`
i POSIX-skal och `Get-Command` i PowerShell. Skilj värdens OS från WSL eller en
container. Identifiera bara de verktyg som det aktuella uppdraget behöver.

Omarchy: `omarchy pkg add <packages...>` är verifierat via lokal kommandokod,
hjälp och officiell upstream 2026-09-09. `omarchy install` har särskilda
installationsflöden, inte ett generellt paketargument. Läs målrepots regler
för om och när dessa får användas. Intern pakethantering i wrappern är inte
samma sak som agentens direkta anrop. Om ett beslutat gränssnitt saknas,
rapportera det; kringgå inte beslutet med en annan pakethanterare.

Windows: verifiera skal, paketkälla, manifest/ID, version och beroenden för
uppgiften. Scoop och WinGet är skilda verktyg; ett byte är ett policybeslut,
inte bara en teknisk fallback. Val av exakt paket får inte härledas från ett
brett produktnamn som .NET. Inget Windows-flöde har funktionstestats här.

Bitwarden: `bw` är Password Manager CLI; `bws` är Secrets Manager CLI med annan
autentisering. Desktop SSH-agent är en separat integrationsyta. Närvaro av en
socket eller upplåst skrivbordsapp bevisar inte fungerande CLI-autentisering.
Bevara befintlig integration, gör inte `bws` till standardberoende och hämta
inte poster/nycklar för att inventera status. Låt användaren hantera nödvändig
inloggning lokalt; fortsätt oberoende analys medan autentisering saknas.

## Officiella källor

Lästa 2026-09-09. Verifiera mot installerad version vid användning; källorna
bevisar inte att en viss dators integration fungerar.

- [chezmoi source-path](https://www.chezmoi.io/reference/commands/source-path/)
  och [scripts](https://www.chezmoi.io/user-guide/use-scripts-to-perform-actions/).
  Lästa som Markdown från [officiella källan](https://github.com/twpayne/chezmoi/tree/master/assets/chezmoi.io/docs).
- [chezmoi ignore](https://www.chezmoi.io/reference/special-files/chezmoiignore/)
  och [managed](https://www.chezmoi.io/reference/commands/managed/): målsökvägar
  och inventering. Dokumentationsundantag måste omfatta katalog och innehåll.
- [Omarchy pkg-add](https://github.com/basecamp/omarchy/blob/master/bin/omarchy-pkg-add).
- [Bitwarden CLI](https://bitwarden.com/help/cli/),
  [Secrets Manager CLI](https://bitwarden.com/help/secrets-manager-cli/) och
  [SSH Agent](https://bitwarden.com/help/ssh-agent/).
- [Scoop](https://github.com/ScoopInstaller/Scoop) och
  [Microsoft WinGet install](https://github.com/MicrosoftDocs/windows-dev-docs/blob/docs/hub/package-manager/winget/install.md).
