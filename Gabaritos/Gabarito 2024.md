---
ano: 2024
tipo: Gabarito
macroeconomia:
  Q01: "15"
  Q02: F,F,V,V,V
  Q03: F,V,V,F,V
  Q04: F,V,F,F,V
  Q05: "10"
  Q06: F,F,V,F,F
  Q07: A
  Q08: F,V,F,F,A
  Q09: V,F,V,V,V
  Q10: V,V,F,V,V
estatistica:
  Q01: V,V,F,F,V
  Q02: "4"
  Q03: V,F,F,V,F
  Q04: V,F,A,F,F
  Q05: F,V,F,A,F
  Q06: "18"
  Q07: F,F,V,V,F
  Q08: V,F,V,V,F
  Q09: V,F,F,V,F
  Q10: F,V,V,F,F
brasileira:
  Q01: V,V,V,F,V
  Q02: F,F,V,V,V
  Q03: F,V,F,V,F
  Q04: V,V,F,F,F
  Q05: F,V,V,F,F
  Q06: V,F,V,F,F
  Q07: F,F,V,F,F
  Q08: V,F,V,V,F
  Q09: F,V,F,V,F
  Q10: F,V,V,F,F
matematica:
  Q01: F,V,F,F,F
  Q02: F,F,F,V,V
  Q03: V,F,F,F,V
  Q04: V,F,V,F,V
  Q05: V,V,V,V,F
  Q06: V,V,F,F,F
  Q07: V,V,F,V,F
  Q08: V,V,F,V,V
  Q09: "24"
  Q10: "55"
microeconomia:
  Q01: F,V,F,F,V
  Q02: V,V,F,F,F
  Q03: F,V,V,V,V
  Q04: F,V,F,V,V
  Q05: V,F,V,F,V
  Q06: F,F,F,V,F
  Q07: F,V,V,F,F
  Q08: V,V,F,V,F
  Q09: "26"
  Q10: "40"
---

O gabarito serve para colocar as respostas das provas de acordo com o ano.

> Abaixo marque o ano da prova (ex.2024)

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


