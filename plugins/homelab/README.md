# Homelab

Personlig plugin för datorer och homelab. Tekniskt namn är `homelab`,
visningsnamnet är **Homelab**, och pluginen ingår i marketplace `plugins`
i repot `Bogstag/plugins`.

Version `0.1.1` innehåller ett portabelt manifest, en MCP-koppling till
Aperture och dokumentation för kommande arbetsflöden. Inga aktiva skills,
hooks, appmappningar eller hjälpskript ingår.

## Struktur

```text
homelab/
├── plugin.json       Identitet och extensions.com.openai
├── mcp.json          Aperture MCP-server
├── AGENTS.md         Regler för pluginutveckling
├── README.md
├── skills/README.md
└── references/
    ├── compatibility.md
    └── roadmap.md
```

`plugin.json` är ingången. OpenAI-inställningarna ligger i
`extensions.com.openai`; ingen separat `.codex-plugin/plugin.json` behövs
för denna struktur. `skills/` och `mcp.json` använder det portabla formatets
fasta sökvägar.

## Installation och uppdatering

Följ [repots installations-, uppdaterings- och kontrollsteg](../../README.md).
Pluginens installationsnamn är `homelab@plugins`. Den verifierade
installationen använder GitHub-marketplace, inte denna arbetsmapp direkt.

## Aperture och körmiljö

`mcp.json` konfigurerar servern `aperture` med transporten `streamable-http`.
Adressen är miljöspecifik och avsedd för det privata nätverket. Körmiljön
måste kunna nå servern och ha de behörigheter som tjänsten kräver.
Plugininstallation ger inte automatiskt nätverksåtkomst eller autentisering.

Målmiljöerna är lokal Codex på Omarchy och Windows 11. Chezmoi, Git, `gh`,
Bitwarden och SSH-agent måste finnas och fungera där respektive framtida
arbetsflöde körs; de installeras inte av pluginen. Bash, PowerShell och WSL
har olika förutsättningar.

Det portabla formatet möjliggör återanvändning, men garanterar inte stöd i
alla värdar. ChatGPT eller andra molnmiljöer kan inte förutsättas nå datorns
verktyg eller privata nätverk. Inga hemligheter, tokens eller privata
SSH-nycklar ska lagras i paketet eller dess exempel.

## Plan och utveckling

Chezmoi är första planerade skill. Tailscale- och Aperture-arbetsflöden kan
byggas ut senare; själva Aperture-kopplingen finns redan.
Skapa `SKILL.md` först när en skill är färdig och testbar.

[AGENTS.md](AGENTS.md) gäller pluginutveckling. Framtida skills får egna
körinstruktioner och ska följa reglerna i målrepot. Dotfiles- och
infrastrukturrepon äger sina egna installations- och driftsregler.

Äldre underlag finns i [planen](references/roadmap.md) och
[kompatibilitetsanteckningarna](references/compatibility.md). De är ännu inte
fullt uppdaterade för det portabla manifestet och den tillagda MCP-kopplingen;
den aktuella strukturen och verifieringsstatusen beskrivs här.

## Verifieringsstatus

Kontrollerat 2026-09-09: manifest och MCP-fil är giltig JSON, marketplace-posten
pekar rätt och Codex listar version `0.1.1` som installerad och aktiverad.
Inga tomma appfiler, trasiga hook-referenser eller aktiva `SKILL.md` finns.

Den äldre lokala `plugin-creator`-validatorn underkänner avsaknaden av
`.codex-plugin/plugin.json`; den stöder inte detta portabla manifestformat.
Fullständig schemavalidering har inte genomförts.

Apertures anslutning och verktyg har inte funktionstestats via denna plugin.
Windows, ChatGPT och andra värdar är inte testade. Installationsstatus ska
därför inte tolkas som att alla framtida arbetsflöden fungerar.
