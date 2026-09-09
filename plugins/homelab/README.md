# Homelab

Homelab (`homelab@plugins`) innehåller från version **0.2.0** en
[chezmoi-skill](skills/chezmoi/SKILL.md) och den befintliga Aperture MCP-kopplingen.

Skillen analyserar, förbereder och granskar dotfiler och paketarbetsflöden.
Den upptäcker körmiljön och läser målrepots aktuella regler, granskar
skriptens sidoeffekter och skiljer verifiering från tillämpning. När verktyg
eller autentisering saknas kan den fortfarande ge tydligt märkta förslag.

## Struktur

```text
plugin.json                     Portabelt manifest, extensions.com.openai
mcp.json                        Befintlig Aperture-koppling
skills/chezmoi/SKILL.md          Skillens ingång
skills/chezmoi/references/       Referens som följer med installation
references/                     Utvecklingskrav, roadmap och testredovisning
```

Skillen behöver inte pluginrepots `docs/` eller andra utvecklingsfiler utanför
paketet. Målrepots AGENTS.md och beslut måste däremot vara tillgängliga vid
användning. Inga nya hjälpskript, beroenden, hooks eller MCP-ändringar ingår.

## Uppdatera installationen och prova

Detta utvecklingssteg installerar, aktiverar eller publicerar inget.
Codex listar fortfarande 0.1.1 från GitHub-källan; lokala 0.2.0 finns inte där
genom detta uppdrag.

För att senare prova den lokala versionen, kör från pluginsamlingens reporot.
Kontrollera först källan:

```bash
codex plugin marketplace list
```

Om `plugins` fortfarande är den registrerade GitHub-källan, ersätt dess
registrering med denna lokala checkout och installera paketet:

```bash
codex plugin marketplace remove plugins
codex plugin marketplace add .
codex plugin add homelab@plugins
codex plugin list --marketplace plugins --available --json
```

Detta byter marketplace-källa för `plugins`. Om den redan pekar på rätt lokal
checkout behövs bara `codex plugin add homelab@plugins` och kontrollen.
Kontrollera att versionen är 0.2.0 och starta en **ny tråd/CLI-session**.

För GitHub-flödet behöver ändringarna först granskas, committas och pushas
med separat godkännande. När versionen finns i den källan, registrera
`Bogstag/plugins` om nödvändigt och kör:

```bash
codex plugin marketplace upgrade plugins
codex plugin add homelab@plugins
```

Prova i en ny session med målrepot öppet:

> Använd $chezmoi från Homelab för att analysera detta repos regler och föreslå
> en liten Starship-ändring. Ändra eller tillämpa inget. Redovisa skript och
> vad du inte har verifierat.

Prova även automatisk aktivering:

> Granska mitt chezmoi-repo och förklara vad som skulle kunna köras vid
> tillämpning. Gör bara statisk analys och hämta inga hemligheter.

Kontrollera att just Homelabs skill laddas om andra chezmoi-skills finns
installerade. Fler negativa scenarier och testprompter finns i
[verifieringsrapporten](references/chezmoi-validation.md).

## Verifiering och begränsningar

Skill Creator-validering:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py plugins/homelab/skills/chezmoi
```

Kör från pluginsamlingens rot; validatorns plats beror på Codex-installationen.
Den äldre pluginvalidatorn kräver legacy-manifest och används inte för att
underkänna det befintliga portabla formatet. Versionsnumret har höjts från
0.1.1 till 0.2.0 för den nya förmågan.

Se [testredovisningen](references/chezmoi-validation.md) för strukturell
validering, isolerade chezmoi-kontroller och simulerade beteendefall.
Aktivering/discovery i värdappen, Windows, riktig Bitwarden-autentisering,
tillämpning och Aperture-anslutning har inte testats i denna version.

Aperture kräver nätverksåtkomst och tjänstens autentisering. Skillen använder
inte MCP som ett generellt beroende. Varken lokala verktyg eller privat nätverk
kan antas tillgängliga i ChatGPT eller andra värdar.

## Fortsatt arbete

[Roadmap](references/roadmap.md) beskriver nästa steg och
[kravunderlaget](references/chezmoi-requirements.md) bevarar acceptansfallen.
[AGENTS.md](AGENTS.md) gäller pluginutveckling, inte målrepots drift.

Dokumenterade konflikter i målrepot ska följas upp där: Bitwarden-mall kontra
README, `run_once`-beskrivning och ofullständig Windows-avgränsning.
Äldre [kompatibilitetsanteckningar](references/compatibility.md) innehåller
också inaktuella manifestuppgifter. Ingen av dessa används som skillens
körreferens eller tyst rättas genom tillämpning.
