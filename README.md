# Bogstag Plugins

Min samling personliga plugins för Codex och andra värdar som stöder
Agent Plugins-formatet. Marketplace heter `plugins` och visas som **Bogstag Plugins**.

## Struktur

```text
.agents/plugins/marketplace.json   Pluginlista och installationspolicy
plugins/homelab/plugin.json        Portabelt manifest och OpenAI-metadata
plugins/homelab/mcp.json           Aperture MCP-konfiguration
plugins/homelab/skills/chezmoi/    Chezmoi-skill med paketerad referens
plugins/homelab/references/        Referensmaterial och planering
```

[Homelab](plugins/homelab/README.md) är den första pluginen: Aperture-koppling
och en chezmoi-skill för analys, förberedelse och granskning av dotfiles.
Lokalt paket är 0.2.0; det har inte installerats i detta utvecklingssteg.

Marketplace-postens `./plugins/homelab` räknas från reporoten, inte från
`.agents/plugins/`. Fler plugins läggs under `plugins/<namn>/` med egna poster
i samma marketplace. Bevara befintliga poster.

## Installation

Installera från GitHub med en Codex-version som stöder plugin-kommandona:

```bash
codex plugin marketplace add Bogstag/plugins
codex plugin add homelab@plugins
```

För lokal utveckling kan källan i stället registreras med
`codex plugin marketplace add .` från reporoten. Kontrollera först
`codex plugin marketplace list`: GitHub-källan och den lokala källan använder
samma marketplace-namn. Kontrollera vilken källa som är vald innan installation.

På den verifierade datorn används GitHub-källan. Lokala ändringar i denna
arbetsmapp uppdaterar därför inte den installerade pluginen automatiskt.
Starta en ny tråd eller CLI-session efter installation.

## Uppdatering

När ändringarna finns i GitHub-källan:

```bash
codex plugin marketplace upgrade plugins
codex plugin add homelab@plugins
```

För en lokal källa uppdateras filerna i den registrerade checkouten före
ominstallation. Ange en ny version i pluginens rotmanifest när ett nytt paket
ska distribueras. Starta en ny session efter ominstallation. Redigera inte
Codex-cache eller konfiguration manuellt för att uppdatera.

## Verifiering

Kör från reporoten:

```bash
python3 -m json.tool .agents/plugins/marketplace.json
python3 -m json.tool plugins/homelab/plugin.json
python3 -m json.tool plugins/homelab/mcp.json
codex plugin marketplace list
codex plugin list --marketplace plugins --available --json
```

JSON-kommandona kontrollerar syntax, inte fullständig schemakompatibilitet.
Kontrollera även att marketplace-sökvägar når rätt plugin och att namnen
matchar. Den lokala äldre `plugin-creator`-validatorn förväntar sig
`.codex-plugin/plugin.json` och stöder inte det portabla formatet.

Kontrollerat 2026-09-09: JSON, marketplace-namn, policy, sökvägar och
manifestmetadata stämmer. Codex CLI `0.153.4` visar `homelab@plugins` version
`0.1.1` som installerad och aktiverad från GitHub-källan. Pluginens manifest
och MCP-fil matchade då dess lokala marketplace-kopia. Efter skillutvecklingen
är det lokala paketet 0.2.0, medan installerad version fortfarande är 0.1.1.
Se [Homelabs verifiering och uppdateringssteg](plugins/homelab/README.md).

Fullständig schemavalidering, Aperture-anslutning, verktygskörning och stöd i
Windows, ChatGPT eller andra värdar är inte verifierade.

Formatreferens: [OpenAI – Package your plugin](https://developers.openai.com/plugins/build/plugins).
