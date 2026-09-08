# Planerade arbetsflöden

Detta är planering, inte aktiverbara instruktioner.

## Först: chezmoi

Avgränsa en första skill till granskning och underhåll av dotfiler samt
repots arbetsflöden kring paketinstallation. Utgå från det verkliga
dotfiles-repots regler och låt skillen upptäcka källkatalog och plattform.
Förhandsgranskning med status/diff ska föregå avsedda ändringar.

Målmiljöerna är Omarchy på laptop och Windows 11 på stationär dator.
Git och `gh` används för versionshantering och GitHub. Bitwarden används för
hemligheter och SSH; autentisering och SSH-agent måste kontrolleras separat
i varje miljö utan att hemligheter skrivs ut.

Skapa skillen först när omfattning, verktygskrav, fallback och realistiska
testfall är definierade. Bash, PowerShell och WSL är separata körmiljöer;
kommandon och sökvägar behöver provas där de ska användas.

## Senare: Tailscale och Aperture

Utöka vid konkret behov med nätverksdiagnostik via Tailscale och arbetsflöden
för AI-proxy via Aperture. Utred först var verktygen körs, nätverksåtkomst,
autentisering och ägande av konfiguration. Lägg inte till anslutningar,
proxyadresser, nycklar eller privilegier i förväg.

Stöd i fler värdmiljöer följer [kompatibilitetsgränserna](compatibility.md).
