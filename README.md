# Painel do ASAS

Quadro de acompanhamento: **Faltando · Em andamento · Concluído**. Página única,
sem servidor e sem dependência além das fontes do Google. Qualquer pessoa da
equipe abre, edita e publica.

## Publicar no GitHub Pages

> **Use um repositório separado.** Não publique a partir do repositório do ASAS:
> ele contém o código do dispositivo e o dossiê inteiro, e um repositório público
> exporia tudo isso.

1. Crie um repositório público novo — por exemplo `painel-asas`.
2. Copie para a raiz dele: `index.html`, `dados.json` e este `README.md`.
3. Em `index.html`, preencha a primeira linha de configuração:

   ```js
   const REPO = 'sua-conta/painel-asas';
   ```

4. **Settings → Pages** → origem no ramo `main`, pasta `/ (root)`.
5. Pronto: `https://sua-conta.github.io/painel-asas/`.

Para ver antes de publicar, sirva a pasta localmente — abrir por duplo clique
funciona, mas aí o painel usa os dados embutidos no `index.html` em vez do
`dados.json`:

```bash
python3 -m http.server 8000 --directory painel
```

## Como a equipe usa

- **Editar**: clique em qualquer texto — título, responsável, prazo, subtarefa.
- **Mover**: os botões no pé de cada cartão mandam a atividade para outra coluna.
- **Adicionar**: `+ atividade` no fim de cada coluna, `+ subtarefa` dentro do cartão.
- **Filtrar**: clique numa frente lá em cima; clique de novo para desmarcar.
  Também dá para filtrar por responsável e ver só os atrasados.
- Atividade com prazo vencido e não concluída fica com a borda vermelha.

O que você muda fica gravado no seu navegador na hora.

## Como salvar para todo mundo

**Publicar** copia os dados e abre o `dados.json` no GitHub. Cole por cima,
escreva o que mudou e confirme. Na próxima vez que alguém abrir o painel, é isso
que aparece.

Ninguém precisa de token, chave ou senha: quem publica usa o próprio login do
GitHub, e cada publicação vira um commit — com autor, data e como voltar atrás.
Quem não tiver permissão de escrita recebe do próprio GitHub a oferta de abrir um
*pull request*.

**Baixar** salva o `dados.json` no computador e **Importar** cola um de volta.
Serve de backup.

## O formato dos dados

```jsonc
{
  "meta":     { "atualizado": "AAAA-MM-DD", "fonte": "…" },
  "frentes":  ["CIApp", "Visual 3D Hair", "…"],
  "atividades": [
    {
      "id": "c1",
      "f":  "CIApp",              // frente, tem de existir na lista acima
      "t":  "título da atividade",
      "r":  "responsável",
      "p":  "2026-09-15",         // prazo, ou "" 
      "s":  "feito",              // falta | anda | feito
      "subs": [ { "t": "subtarefa", "ok": true } ]
    }
  ]
}
```

Editar o `dados.json` à mão funciona igual — o painel lê o arquivo se ele existir
e, se não existir, cai nos dados embutidos no `index.html`.
