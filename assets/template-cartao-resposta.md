---
ano: 
tipo: Resposta
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
<%* 
const date = tp.date.now("YYYY-MM-DD"); 
await tp.file.rename(`Respostas ANO ${date}`);
%>

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

# Prova Discursiva

> Escreva seu texto abaixo: