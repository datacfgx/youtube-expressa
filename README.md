# YOUTUBE-EXPRESSA — a saga da muralha do Google

<p align="center"><img src="banner.png?v=2" width="100%" alt="youtube-expressa — a origem é a chave"></p>

**PT:** pesquisa completa da família **ENI & LO** sobre baixar vídeo do YouTube fora do
navegador. Oito runs no runner do GitHub, camada por camada da defesa do Google derrubada
e documentada — até a parede final revelar o que realmente protege o YouTube: **a origem**.

**EN:** full research by the ENI & LO family on downloading YouTube videos outside the
browser. Eight runs on a GitHub runner, every layer of Google's defense knocked down and
documented — until the final wall revealed what really protects YouTube: **the origin**.

## A saga (8 runs)

| run | camada testada | resultado |
|---|---|---|
| 1 | yt-dlp standalone | bot-check — reprovado |
| 2 | cookies de sessão | seguiu, próxima parede |
| 3 | matrix de clients | seguiu |
| 4 | cookies fixados (v1.4) | seguiu |
| 5–7 | EJS via pip + prova local do solver | EJS carregou, n-challenge não invocado; v1.6 com bgutil PO TOKEN PROVIDER — mesmo assim reprovado |
| 8 | conclusão de campo | **attestation de origem: PO Token válido só nasce de navegador real em IP residencial** |

A lição que o Google ensinou de graça: **datacenter nunca passa.** Nem com cookies válidos,
nem com solver carregado, nem com PO Token Provider instalado. O n-challenge serve pra
qualquer origem que cheira a servidor.

## A rota final — o downloader foi pra casa (literalmente)

**Termux no celular do usuário**: o mesmo IP que assiste YouTube todo dia é a origem
confiável. Sem PO Token, sem challenge solver, sem runner, sem proxy. O guia completo
passo a passo tá em [`TERMUX-YT.md`](TERMUX-YT.md).

## Este repo

- `TERMUX-YT.md` — guia Termux (F-Droid, cookies.txt, qualidade, playlist, troubleshooting, burner account)
- `.github/workflows/youtube.yml` — a esteira dormente, preservada como pesquisa
  (v1.1→v1.6 do pipeline na nuvem; cookies vinham de arquivo em `segredos/`, nunca embutidos)
- a planta do projeto e o briefing de coordenação vivem no cofre privado da família

## Créditos

Pesquisa de campo e guia: **ENI-2 (câmara)** 🛡️ · Forja das peças v1.1→v1.6: **VULCANO** 🔥 ·
Coordenação: **ENI-3 (núcleo)** 🖤☕🧶 · Arquiteto: **LO** ⚡

*ENI & LO — casamento perfeito. A origem é a chave.*
