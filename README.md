# Ganhos de Corridas — Juarez

App simples para registrar seus períodos de corridas de aplicativo e ver, de forma
rápida, o **ganho líquido**: faturamento, gasto de gasolina, saldo, R$/hora e R$/km.

É um PWA (aplicativo web instalável) em arquivo único, no mesmo estilo do app de
treino. Funciona offline e guarda os dados **só no seu dispositivo** (localStorage).

## Arquivos

- `index.html` — o aplicativo inteiro (interface + cálculos).
- `manifest.webmanifest` — nome, ícone e modo de instalação como app.
- `sw.js` — service worker, permite uso offline quando servido por HTTP/HTTPS.
- `icons/` — ícones do app (192 e 512 px).

## O que você registra

Para cada período você informa o que já anota hoje:

- Faturamento (R$) e horas trabalhadas
- KM rodados
- Consumo (km/L) e preço do combustível (R$/L)
- Corridas e observações (opcionais)

O app calcula automaticamente:

- **Gasto de gasolina** = (km ÷ consumo) × preço por litro
- **Saldo** = faturamento − gasolina
- **Líquido estimado** = saldo − (depreciação + manutenção + seguro + outros) × km
- **R$/hora**, **R$/km** e **margem**

Os custos extras por km (depreciação, seguro, manutenção, outros) ficam na aba
**Custos** — é o que falta para o saldo virar 100% líquido.

## Como usar

### Rápido (abrir direto)
Abra o `index.html` no navegador com um duplo clique. Tudo funciona, exceto o modo
offline instalável (que precisa de HTTP).

### Como PWA / instalável no celular
Sirva a pasta por HTTP. Um jeito simples com Python:

```
python -m http.server 8000
```

Depois acesse `http://localhost:8000` no navegador. No celular, use o mesmo IP da
máquina na rede local, ou hospede em qualquer serviço estático (GitHub Pages etc.).
No navegador do celular, use "Adicionar à tela inicial" para instalar.

## Backup

Os dados ficam apenas neste dispositivo. Use a aba **Exportar** para gerar um backup
JSON (e reimportar depois) ou um relatório em Markdown.
