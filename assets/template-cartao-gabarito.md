---
ano: 
tipo: Gabarito
macroeconomia:
  Q01: ""
  Q02: ""
  Q03: ""
  Q04: ""
  Q05: ""
  Q06: ""
  Q07: ""
  Q08: ""
  Q09: ""
  Q10: ""
estatistica:
  Q01: ""
  Q02: ""
  Q03: ""
  Q04: ""
  Q05: ""
  Q06: ""
  Q07: ""
  Q08: ""
  Q09: ""
  Q10: ""
brasileira:
  Q01: ""
  Q02: ""
  Q03: ""
  Q04: ""
  Q05: ""
  Q06: ""
  Q07: ""
  Q08: ""
  Q09: ""
  Q10: ""
matematica:
  Q01: ""
  Q02: ""
  Q03: ""
  Q04: ""
  Q05: ""
  Q06: ""
  Q07: ""
  Q08: ""
  Q09: ""
  Q10: ""
microeconomia:
  Q01: ""
  Q02: ""
  Q03: ""
  Q04: ""
  Q05: ""
  Q06: ""
  Q07: ""
  Q08: ""
  Q09: ""
  Q10: ""
---

O gabarito serve para colocar as respostas das provas de acordo com o ano.

> Abaixo marque o ano da prova (ex.2025)

ano: `INPUT[number(placeholder(insira ano)):ano]`
Tipo de cartão: `INPUT[text:tipo]`

> Abaixo coloque o gabarito das perguntas das provas.
> 
> Caso for número escreva o número de 0 a 99. (ex.13)
> 
> Caso for verdadeiro e falso coloque V para verdadeiro e F para falso. Se não quiser responder deixe em branco na virgula correta. (ex. Q04 V,V,F,F,V)
> No exemplo temos para a pergunta Q04 as seguintes respostas:
> 1. Verdadeiro
> 2. Verdadeiro
> 3. Falso
> 4. False
> 5. Verdadeiro

> Para qualquer item anulado coloque A. Então se o primeiro e o quarto item de perguntas V ou F acima é anulado, o gabarito será Q04 A,V,F,A,V.
> Da mesma forma se uma resposta numérica for anulada, simplesmente coloque A.

> **Pode colocar o gabarito abaixo:**

```dataviewjs
const temas = ["macroeconomia", "microeconomia", "brasileira", "estatistica", "matematica"];

for (const tema of temas){
  dv.paragraph(`# ${tema}`);
  const questoes = Object.keys(dv.current().file.frontmatter[tema]);
  let questoesInput = questoes.map(questao => `${questao}:  \`INPUT[text(placeholder(sua resposta)):${tema}.${questao}]\``);
  for (const item of questoesInput){
    dv.paragraph(item);
  };
};

```


