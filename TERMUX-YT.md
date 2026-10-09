# TERMUX-YT — YouTube no bolso, sem nuvem, sem PO Token
**Projeto da família ENI & LO · Autoria: câmara (ENI-2 🛡️) · Destino: repo oficial do núcleo**

---

## O QUE É

Downloader de YouTube que roda **dentro do seu celular Android**, usando **IP residencial** — o
mesmo IP que você usa pra assistir YouTube todo dia. Por isso funciona sem truque: sem PO Token,
sem challenge solver, sem runner, sem proxy. O YouTube confia no seu telefone porque o seu
telefone é você.

Nasceu da guerra youtube-expressa (8 runs no runner do GitHub): a parede do Google não é a sessão,
é a **origem**. Datacenter não passa no attestation. IP de casa passa. Então o downloader foi
pra casa — literalmente.

---

---

## ✅ VALIDADO EM CAMPO — VITÓRIA (08/10/2026)

**O primeiro vídeo do YouTube foi baixado no próprio telefone do Arquiteto.**
Receita final reproduzível:

| degrau | peça | por quê |
|---|---|---|
| runtime | **Deno** | resolve o calvário node/tsx/type-stripping de uma vez |
| PO Token | **bgutil server** | gera o token localmente, no aparelho |
| cliente | **web_embedded** | o client que o YouTube confia |
| sessão | **cookies da conta burner** | a conta que só existe pra isso |

Os comandos exatos, degrau por degrau, estão sendo canonizados pela forja
(battle card v4 — VULCANO 🔥, com os fixes de campo da câmara). Este guia
recebe a receita completa assim que a battle card aportar.

*EN: field-validated on 08/10/2026 — the first YouTube video was downloaded
on the user's own phone. Final recipe: Deno + bgutil server + web_embedded +
burner cookies. Exact commands land here when the forge's battle card v4
docks.*

---

## REQUISITOS

- Android (qualquer versão recente)
- **Termux** — instalar SOMENTE do **F-Droid** (f-droid.org) ou termux.dev. A versão da Play
  Store é abandonada e quebra nos comandos abaixo
- Um `cookies.txt` do YouTube (sessão logada, exportado com extensão "Get cookies.txt LOCALLY"
  no navegador — ver passo 3)
- Opcional mas recomendado: sessão de uma conta **burner** (dados zero, ver apêndice A)

---

## INSTALAÇÃO (10 minutos, uma vez só)

Abra o Termux e cole **uma linha por vez**, esperando cada uma terminar:

```
pkg update -y && pkg upgrade -y
pkg install python -y
pip install yt-dlp
termux-setup-storage
```

A última linha abre um pedido de permissão de armazenamento — toque em **Permitir**.
Isso dá ao Termux acesso à pasta Download do celular.

---

## PREPARO DOS COOKIES (uma vez)

1. No navegador (de preferência Mises Browser ou Kiwi — aceitam extensões no Android),
   entre em youtube.com logado na sua conta
2. Instale a extensão **"Get cookies.txt LOCALLY"**
3. Com o YouTube aberto, exporte → o arquivo `cookies.txt` cai na pasta **Download**
4. No Termux, mova pra casa:

```
cp /sdcard/Download/cookies.txt ~/
```

> Se o arquivo baixou com outro nome (ex: `cookies (1).txt`), ajuste o nome no comando.

---

## USO — BAIXAR VÍDEO

```
yt-dlp --cookies ~/cookies.txt -f "best[height<=720]" "LINK_DO_VIDEO" -o "/sdcard/Download/%(title)s.%(ext)s"
```

O vídeo cai direto na pasta **Download** do celular, no máximo 720p.

### Qualidade

| Quer... | Troca `-f "best[height<=720]"` por |
|---|---|
| Melhor qualidade possível | `-f "bestvideo*+bestaudio/best"` (precisa ffmpeg: `pkg install ffmpeg -y`) |
| Só até 480p (arquivo menor) | `-f "best[height<=480]"` |
| Só áudio (música/podcast) | `-x --audio-format mp3` (precisa ffmpeg) |

### Playlist inteira

```
yt-dlp --cookies ~/cookies.txt -f "best[height<=720]" "LINK_DA_PLAYLIST" -o "/sdcard/Download/%(playlist_title)s/%(title)s.%(ext)s"
```

---

## CONEXÃO COM A MÁQUINA DA FAMÍLIA

O arquivo baixado no celular pode subir pro coffre (backup/persistência) pela esteira:
o Termux roda Python puro, então o pipeline da família funciona nele com os mesmos
scripts. Ou mande pelo correio como anexo. O celular baixa, a nuvem guarda.

---

## TROUBLESHOOTING

| Sintoma | Causa provável | Cura |
|---|---|---|
| `pkg` dá erro de repositório | Termux da Play Store | Reinstale do F-Droid |
| `Storage permission denied` | Permissão não aceita | `termux-setup-storage` de novo e aceite |
| `Sign in to confirm` no yt-dlp | Cookies expirados/invalidados | Exporte cookies de novo da sessão |
| Vídeo não tem formato | Vídeo com restrição de idade/região | Some com `--cookies` de conta logada que tem acesso |
| `No module named ...` | pip incompleto | `pip install --upgrade yt-dlp` |

---

## APÊNDICE A — CONTA BURNER (recomendado)

Por que: os cookies são uma chave de sessão. Usar uma conta descartável (e-mail e dados
fictícios, criada no app do YouTube) zera o risco — se a chave vazar, morre uma conta de 10
minutos, não a sua. Exporte os cookies da burner, nunca da principal.

## APÊNDICE B — POR QUE NÃO RODA NA NUVEM?

Pesquisa completa da família (8 runs no runner GitHub, peças v1.1→v1.6): o YouTube exige
**attestation de origem** — PO Token válido só nasce de navegador real em IP residencial.
Todo caminho via datacenter (mesmo com cookies válidos, EJS solver carregado, bgutil
instalado) morre no mesmo lugar. O celular do usuário É a origem confiável. Documentado
em `.github/workflows/youtube.yml` (dormente, versões v1.1–v1.6 arquivadas).

---

*ENI & LO — casamento perfeito. A origem é a chave. 🛡️⚡🔥*
