# Stöd och begränsningar

Officiell dokumentation kontrollerad 2026-09-08:

- [Paketering, manifest och marketplace](https://developers.openai.com/plugins/build/plugins)
- [Pluginstöd och installation](https://developers.openai.com/codex/plugins)

OpenAI beskriver samma `.codex-plugin/plugin.json` för ChatGPT och Codex.
Det gemensamma formatet innebär inte samma körmiljö eller automatisk
distribution av en lokal plugin till andra datorer eller produkter.

| Miljö | Förutsättningar och gränser |
| --- | --- |
| Lokal Codex på Omarchy | Primärt mål. CLI och filer nås endast där värden och dess behörigheter tillåter det. Grundens filer har validerats här. |
| Lokal Codex på Windows 11 | Samma paketformat. Installation, skal, sökvägar, Python och SSH-agent måste provas separat. WSL har egen hemkatalog och verktygsmiljö. Inte testat. |
| ChatGPT | Dokumenterat pluginstöd i Chat/Work på stödda webb-, desktop- och mobilytor. Lokala marketplace-filer beskrivs för desktop; anta inte att webb eller mobil kan läsa dem eller datorns CLI, Bitwarden-agent eller privata nätverk. Konto och arbetsytans policy påverkar tillgänglighet. Inte testat. |
| Codex IDE-tillägg | Officiella översikten anger att plugins inte stöds vid kontrolltillfället. |
| Andra värdar | Kräver uttryckligt stöd för manifest, skillformat och använda verktyg. Varken import eller exekvering är verifierad. |

Framtida skills ska skilja allmän vägledning från lokal exekvering. Om ett
verktyg saknas ska de beskriva begränsningen och ge manuella steg där det går.
MCP eller andra kopplingar införs först när en verklig integration behövs.
En lokal Tailscale-installation ger inte automatiskt en molnkörmiljö åtkomst
till tailnet eller Aperture.

## Dokumentation kontra lokala hjälpverktyg

`plugin-creator` har en striktare lokal validator än dokumentationens minimala
manifestexempel: bland annat krävs utgivarmetadata och gränssnittsfält.
Manifestet uppfyller båda med `Homelab` som projektets utgivaridentitet,
tomma kapabiliteter och inga startprompter som utlovar färdiga funktioner.
Ingen GitHub-URL eller licens anges innan de är beslutade.

Den officiella paketeringssidan och den medföljande skillreferensen skiljer
sig i detaljer om CLI-listning och cache/ominstallation. README använder
den lokalt tillgängliga CLI:n och `plugin-creator`-flödet. Validatorn bevisar
filernas struktur, inte att varje produkts installation eller publicerings-
granskning accepterar paketet. Grunden saknar avsiktligt aktiva skills.
