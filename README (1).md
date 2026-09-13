# Vending Machine — AFD

Trabalho 01 de Autômatos: máquina de vendas modelada como **Autômato Finito Determinístico (AFD)**.

## Abordagem

A implementação segue a forma apresentada na Aula 12: **Tabela (dicionário ou matriz)**.

A máquina aceita moedas de **5¢, 10¢ e 25¢**. O produto custa **30¢**. O estado `q30` representa 30¢ ou mais e é o estado final.

## Tabela de transições

| Estados / Entradas | 5¢ | 10¢ | 25¢ |
|---|---|---|---|
| → q0 | q5 | q10 | q25 |
| q5 | q10 | q15 | q30* |
| q10 | q15 | q20 | q30* |
| q15 | q20 | q25 | q30* |
| q20 | q25 | q30* | q30* |
| q25 | q30* | q30* | q30* |
| q30* | q30* | q30* | q30* |

`→` = inicial; `*` = final.

## Código

A tabela está diretamente em `script.js`:

```javascript
const tabela = {
  q0:  {5:"q5",  10:"q10", 25:"q25"},
  q5:  {5:"q10", 10:"q15", 25:"q30"},
  q10: {5:"q15", 10:"q20", 25:"q30"},
  q15: {5:"q20", 10:"q25", 25:"q30"},
  q20: {5:"q25", 10:"q30", 25:"q30"},
  q25: {5:"q30", 10:"q30", 25:"q30"},
  q30: {5:"q30", 10:"q30", 25:"q30"}
};
```

A função de transição consulta a tabela:

```javascript
function transicionar(estado, entrada) {
  return tabela[estado][entrada];
}
```

Assim, a regra é:

**estado atual + entrada → próximo estado**

## Exemplos

`25 5`:

```text
q0 --25--> q25
q25 --5--> q30
```

30¢ → **ACEITA**

`10 10 10`:

```text
q0 --10--> q10
q10 --10--> q20
q20 --10--> q30
```

30¢ → **ACEITA**

`5 10 5`:

```text
q0 --5--> q5
q5 --10--> q15
q15 --5--> q20
```

20¢ → **REJEITADA**

## Executar

Abra `index.html` no navegador. Não há dependências externas.

## JFLAP

O arquivo `vending-machine.jff` contém o mesmo AFD para abrir no JFLAP.

## Publicar no GitHub

```bash
git init
git add .
git commit -m "Implementa vending machine com AFD por tabela"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/vending-machine-afd.git
git push -u origin main
```

Para GitHub Pages: **Settings → Pages → Deploy from a branch → main → /(root) → Save**.
