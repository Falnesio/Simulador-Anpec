---
ano: 2025
tipo: Gabarito
macroeconomia:
  Q01: A,A,A,A,A
  Q02: A
  Q03: V,V,V,F,V
  Q04: V,V,F,F,V
  Q05: V,V,F,F,V
  Q06: V,V,A,F,V
  Q07: V,V,V,F,V
  Q08: V,V,A,F,V
  Q09: 34
  Q10:  V,V,V,F,V
estatistica:
  Q01: V,V,F,F,V
  Q02: 40
  Q03: V,V,V,F,V
  Q04: V,V,F,F,V
  Q05: V,V,A,F,V
  Q06: V,V,F,F,V
  Q07: V,V,V,F,V
  Q08: V,V,V,F,V
  Q09: 34
  Q10:  V,V,F,F,V
brasileira:
  Q01: V,V,V,F,V
  Q02: 40
  Q03: V,V,V,F,V
  Q04: V,V,A,F,V
  Q05: V,V,F,F,V
  Q06: V,V,V,F,V
  Q07: V,V,V,F,V
  Q08: V,V,F,F,V
  Q09: 34
  Q10:  V,V,V,F,V
matematica:
  Q01: V,V,A,F,V
  Q02: 40
  Q03: V,V,F,F,V
  Q04: V,V,F,F,V
  Q05: V,V,V,F,V
  Q06: V,V,V,F,V
  Q07: V,V,F,F,V
  Q08: V,V,V,F,V
  Q09: 34
  Q10:  V,V,V,F,V
microeconomia:
  Q01: V,V,F,F,V
  Q02: 40
  Q03: V,V,V,F,V
  Q04: V,V,V,F,V
  Q05: V,V,V,F,V
  Q06: V,V,V,F,V
  Q07: V,V,F,F,V
  Q08: V,V,F,F,V
  Q09: 34
  Q10:  V,V,F,F,V
---

O gabarito serve para colocar as respostas das provas de acordo com o ano.

> Abaixo marque o ano da prova (ex.2025)

ano: `INPUT[number(placeholder(insira ano)):ano]`
Tipo de cartão: `INPUT[text:tipo]`

> Abaixo coloque as respostas das perguntas das provas.
> 
> Caso for número escreva o número de 0 a 99. (ex.13)
> 
> Caso for verdadeiro e falso coloque V para verdadeiro e F para falso. Se não quiser responder deixe em branco na virgula correta. (ex. Q04 V,V,F, ,V)
> No exemplo temos para a pergunta Q04 as seguintes respostas:
> 1. Verdadeiro
> 2. Verdadeiro
> 3. Falso
> 4. Em Branco
> 5. Verdadeiro

> Após finalizar a simulação, vá para [[Resultado]] para conferir como foi.

> **Pode simular sua prova abaixo:**

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


