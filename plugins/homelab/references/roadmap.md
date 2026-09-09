# Planerade arbetsflöden

Detta är planering, inte aktiverbara instruktioner.

## Levererat lokalt: chezmoi i 0.2.0

[Skillen](../skills/chezmoi/SKILL.md) finns nu med en paketerad granskningsreferens.
Den är inte installerad eller aktiverad i denna utvecklingssession.
Återstår: aktiveringsprov i en ny session, verkliga Windows-flöden och senare
användningsprov med separat godkännande av tillämpning. Se
[verifieringsrapporten](chezmoi-validation.md) för testnivåer och testprompter.

Syfte, arbetsgång och provfall finns i [chezmoi-kraven](chezmoi-requirements.md).
Dotfiles-specifika beslut förvaltas i målrepot; se
[regelägande och historik](../../../docs/decisions.md). De första anteckningarna
här har ersatts av dessa underlag för att undvika dubblerade regler.

## Senare: Tailscale och Aperture

En Aperture MCP-konfiguration finns redan. Utöka vid konkret behov med
nätverksdiagnostik via Tailscale och arbetsflöden
för AI-proxy via Aperture. Utred först var verktygen körs, nätverksåtkomst,
autentisering och ägande av konfiguration. Lägg inte till anslutningar,
proxyadresser, nycklar eller privilegier i förväg.

Stöd i fler värdmiljöer följer [kompatibilitetsgränserna](compatibility.md).
Äldre manifest-/reponamnsuppgifter och dotfiles-konflikterna är kvar som
uppföljning i beslutsunderlagen; detta steg ändrar inte dotfiles-repot.
