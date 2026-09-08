# Utveckling av Homelab

Dessa regler gäller arbete i detta pluginrepo. De är inte körinstruktioner
för installerade skills och ger inte rätt att ändra datorer eller andra repon.

- Behåll `homelab-plugin` som mapp-, manifest- och framtida GitHub-reponamn;
  visningsnamnet är `Homelab`.
- Skriv kort på svenska. Länka till gemensamma referenser i stället för att
  kopiera instruktioner. Använd relativa sökvägar inom paketet.
- Lägg framtida körinstruktioner i `skills/<namn>/SKILL.md` först när skillen
  är färdig och testbar. Planering hör hemma i `references/roadmap.md`.
- Framtida skills ska läsa målrepots egna regler, upptäcka OS, skal, verktyg
  och behörigheter samt beskriva vad som kan göras när ett verktyg saknas.
  Dotfiles- och infrastrukturrepon äger sina egna installations-, ändrings-
  och driftsregler; kopiera dem inte hit och åsidosätt dem inte.
- Lägg till MCP, hooks, appar, beroenden och hjälpskript först för ett konkret
  arbetsflöde. Anta inte att lokal CLI, SSH-agent eller nätverksåtkomst finns.
- Förvara hemligheter i Bitwarden eller miljöns avsedda hemlighetshantering.
  Lägg aldrig tokens, lösenord, privata SSH-nycklar, valvexporter eller verkliga
  autentiseringsuppgifter i filer, exempel, loggar eller testdata här.
- Bevara andra marketplace-poster. Följ `plugin-creator` för registrering och
  uppdatering; lägg personlig marketplace-konfiguration utanför pluginrepot.
- Kör valideringen i README efter ändringar. Rapportera vilka miljöer och
  funktioner som faktiskt testats. Publicering kräver ett separat uppdrag.
