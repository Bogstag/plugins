# Beslutsunderlag för Homelab

Uppdaterat 2026-09-09. Detta repo äger pluginens struktur och återanvändbara
skillkrav. Dotfiles-specifika regler ägs av målrepot.

## Regelägande

De tidigare dotfiles-besluten har flyttats till
[Bogstag/dotfiles: docs/decisions.md](https://github.com/Bogstag/dotfiles/blob/HEAD/docs/decisions.md).
Länken är den avsedda repoplatsen; denna uppdatering är endast lokal och inte
pushad. Läs den lokala filen efter att källkatalogen upptäckts med
`chezmoi source-path`, tillsammans med målrepots AGENTS.md. Hårdkoda inte
källkatalogen och ersätt inte saknade regler med en gammal kopia här.

[Kraven för chezmoi-skillen](../plugins/homelab/references/chezmoi-requirements.md)
beskriver hur reglerna ska läsas, vilka förmågor som behövs och hur de provas.
Detta dokument underhåller ingen separat paket- eller godkännandepolicy.

## Historik och beslut som gäller pluginen

De första användarbesluten om målplattformar, dotfiler, paket, Bitwarden, Git
och officiell dokumentation samlades här 2026-09-09. Vid förtydligandet samma
dag flyttades hela beslutssamlingen, inklusive angivna eller saknade motiveringar,
öppna frågor och verifierat nuläge, till dotfiles-repot. Där dokumenteras nu
också upptäckten av Omarchys gränssnitt och de preciserade godkännandegränserna.

- **Beslutat:** chezmoi är första planerade skill i Homelab. Omfattningen är
  analys, förberedelse och granskning av dotfiles-arbetsflöden. Ingen ytterligare
  motivering angiven.
- **Beslutat:** skillen ska vara återanvändbar och läsa målrepots regler.
  Maskinspecifika beslut ska inte underhållas i flera repon.
- **Status:** första skillen skapad lokalt i 0.2.0 efter nytt användaruppdrag.
  Den tidigare avgränsningen till krav är historik; installation och tillämpning
  ingår fortfarande inte i utvecklingsuppdraget.

## Verifierat i pluginrepot och äldre motsägelser

Pluginen har ett portabelt `plugin.json`, version `0.2.0`, och en
`mcp.json` som deklarerar Aperture. En chezmoi-skill finns nu lokalt. Det är inte
en implementation av dotfiles-repots paket- eller Bitwarden-flöden.

Äldre motsägelser från den första genomgången kvarstår utanför detta uppdrag:
Homelabs AGENTS.md nämner `homelab` som framtida GitHub-reponamn trots
pluginsamlingen `Bogstag/plugins`; kompatibilitetsanteckningarna beskriver
äldre manifest/validering och säger att licens saknas trots MIT i manifestet.
Aperture-konfiguration finns redan, medan äldre planering beskriver den som
framtida. Dessa uppgifter ska inte användas som verifierat nuläge för skillen.

De tidigare öppna frågorna om dotfiles-repo, Omarchy-gränssnitt och
godkännandemodell är besvarade i målrepots beslut. Återstående miljödetaljer
kan hanteras vid ett konkret uppdrag och blockerar inte skapandet av skillen.
