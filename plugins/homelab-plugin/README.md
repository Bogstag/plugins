# Homelab

Personlig plugin för återanvändbara arbetsflöden på mina datorer och i mitt
homelab. Tekniskt namn, mapp och planerat GitHub-repo: `homelab-plugin`.
Version `0.1.0` innehåller bara grunden. Inga aktiva skills, MCP-kopplingar,
hooks, appar eller hjälpskript ingår.

Chezmoi är [första planerade skill](references/roadmap.md), med Tailscale och
Aperture som senare utökningar. Primärt används pluginen i lokal Codex på
Omarchy och Windows 11. Se [stöd och begränsningar](references/compatibility.md)
för ChatGPT och andra värdar; lokala verktyg följer inte med paketet.

## Struktur

```text
homelab-plugin/
├── .codex-plugin/plugin.json
├── AGENTS.md
├── README.md
├── skills/README.md
└── references/
    ├── compatibility.md
    └── roadmap.md
```

[AGENTS.md](AGENTS.md) gäller utveckling av pluginen. Framtida skills får
egna körinstruktioner och måste följa målrepots regler. Dotfiles- och
infrastrukturkonfiguration förvaltas i sina respektive repon.

## Lokal installation

På denna dator ligger källan i `~/Projects/homelab-plugin`. Den personliga
marketplace-filen är `~/.agents/plugins/marketplace.json`, med namnet
`personal`. Posten använder `./plugins/homelab-plugin`, relativt hemkatalogen
(marketplace-roten), inte katalogen där JSON-filen ligger.
`~/plugins/homelab-plugin` är en relativ symbolisk länk till projektmappen.

Installera med en Codex-version som stöder plugin-kommandona:

```bash
codex plugin add homelab-plugin@personal
```

Alternativt: öppna pluginvyn i en stödd desktop-app, uppdatera/starta om appen
vid behov och installera Homelab från den personliga källan. Standardkällan
upptäcks implicit och behöver inte `codex plugin marketplace add`.
Starta en ny tråd eller CLI-session efter installationen.

På en annan dator: kopiera hela pluginmappen, inklusive `.codex-plugin`, till
`~/plugins/homelab-plugin` eller Windows motsvarighet
`%USERPROFILE%/plugins/homelab-plugin`. Använd `plugin-creator` för att lägga
till posten i datorns personliga marketplace och bevara dess befintliga
poster och namn. Befintlig marketplace kan heta något annat än `personal`;
använd då dess faktiska namn i installationskommandot.
Ingen symlänk behövs om källan ligger direkt under `plugins/`.

Marketplace-posten har följande form (lägg till posten, ersätt inte katalogen):

```json
{
  "name": "homelab-plugin",
  "source": { "source": "local", "path": "./plugins/homelab-plugin" },
  "policy": { "installation": "AVAILABLE", "authentication": "ON_INSTALL" },
  "category": "Productivity"
}
```

Policyn kräver inte någon hemlighet i denna grund, eftersom inga anslutningar
ingår. Marketplace-filen och maskinens länkar ligger utanför pluginrepot.

## Testning

Kör från pluginroten på denna Linux-installation (Python 3 och PyYAML behövs
för validatorn som levereras med `plugin-creator`):

```bash
python3 ~/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
python3 ~/.codex/skills/.system/plugin-creator/scripts/read_marketplace_name.py
python3 -m json.tool .codex-plugin/plugin.json
```

Hjälpverktygens placering är installationsberoende; de ingår inte i Homelab.
På Windows används installerad Python och sökvägen till motsvarande skill.
Kontrollera även att marketplace-sökvägen når samma manifest och att inga
`SKILL.md`-filer finns innan en färdig skill avsiktligt läggs till.

Efter installation: kontrollera visningsnamnet Homelab och att inga skills
eller verktyg tillkommer i en ny session. Det är förväntat för denna version.
En strukturellt giltig grund är inte ett funktionstest av framtida flöden.

## Uppdatering

Ändra källan som marketplace-posten pekar på. Kör följande från pluginroten
med hjälpverktygen från `plugin-creator`:

```bash
python3 ~/.codex/skills/.system/plugin-creator/scripts/read_marketplace_name.py
python3 ~/.codex/skills/.system/plugin-creator/scripts/update_plugin_cachebuster.py .
python3 ~/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
codex plugin add homelab-plugin@personal
```

Avbryt vid valideringsfel och använd marketplace-namnet som läsverktyget
skriver ut. Uppdateringsverktyget behåller basversionen och ersätter ett enda
`+codex.<cachebuster>`-suffix så att ominstallationen tar upp ändringarna.
Redigera inte marketplace eller Codex-konfiguration manuellt för att tömma
cachen. Starta en ny tråd/session; en installerad kopia uppdateras inte
automatiskt när källfiler redigeras. På övriga datorer måste även källan
synkroniseras innan ominstallation. GitHub är ännu inte skapat eller publicerat.

## Verifieringsstatus

Kontrollerat 2026-09-08 med Codex CLI `0.153.4`: plugin-creator-validatorn
godkände manifestet. Marketplace-identitet, policy, källsökväg och interna
Markdown-länkar kontrollerades. Codex listar `homelab-plugin@personal` som
tillgänglig, ännu inte installerad. Inga aktiva skills eller integrationer
finns, och en sökning efter vanliga token- och privatnyckelmönster gav inga träffar.

Själva installationen, Windows, ChatGPT, andra värdar och faktisk aktivering
i en ny apptråd är inte verifierade.
Hemligheter och maskinspecifika autentiseringsuppgifter hör aldrig hemma i
pluginen eller dess exempel; se utvecklingsreglerna i AGENTS.md.
