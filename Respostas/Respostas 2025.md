---
ano: 2025
tipo: Resposta
macroeconomia:
  Q01: V,V,F,F,F
  Q02: 40
  Q03: V,V,V,F,V
  Q04: V,V,F,F,V
  Q05: V,V,,F,V
  Q06: V,V,F,F,V
  Q07: V,V,V,F,V
  Q08: V,V,F,F,V
  Q09: "34"
  Q10: V,V,,F,V
estatistica:
  Q01: V,V,V,F,V
  Q02: 40
  Q03: V,V,F,F,V
  Q04: V,V,F,F,V
  Q05: V,V,V,F,V
  Q06: V,V,V,F,V
  Q07: V,V,F,F,V
  Q08: V,V,V,F,V
  Q09: 34
  Q10: V,V,F,F,V
brasileira:
  Q01: V,V,V,F,V
  Q02: 40
  Q03: V,V, ,F,V
  Q04: V,V,F,F,V
  Q05: V,V,V,F,V
  Q06: V,V,F,F,V
  Q07: V,V,F,F,V
  Q08: V,V,V,F,V
  Q09: 34
  Q10: V,V,F,F,V
matematica:
  Q01: V,V,F,F,V
  Q02: 40
  Q03: V,V,V,F,V
  Q04: V,V,V,F,V
  Q05: V,V,F,F,V
  Q06: V,V,F,F,V
  Q07: V,V,V,F,V
  Q08: V,V, ,F,V
  Q09: 34
  Q10: V,V, ,F,V
microeconomia:
  Q01: V,V, ,F,V
  Q02: 40
  Q03: V,V,F,F,V
  Q04: V,V,V,F,V
  Q05: V,V,V,F,V
  Q06: V,V,F,F,V
  Q07: V,V,V,F,V
  Q08: V,V,V,F,V
  Q09: 34
  Q10: V,V, ,F,V
obsidianUIMode: preview
---

> Abaixo marque o ano da prova (ex.2025) para aparecer os links dos PDFs com as perguntas das provas do ano que deseja.

ano: `INPUT[inlineSelect(option(2024),option(2025)):ano]`
Tipo de cartão: Resposta

Segure **ctrl** e **alt** no teclado ao clicar abaixo para abrir o PDF em uma aba ao lado.
```dataviewjs
const pdfFiles = app.vault.getFiles().filter(file => 
    file.extension === 'pdf' && 
    file.path.includes('Provas') && 
    !file.path.includes('Gabarito')
);

const itensPorAno = pdfFiles.reduce((acc, file) => {
    const yearMatch = file.basename.match(dv.current().ano);
    if (yearMatch) {
        const year = yearMatch[0];
        if (!acc[year]) acc[year] = [];
        acc[year].push(file);
    }
    return acc;
}, {});

for (const ano in itensPorAno) {
    dv.header(5, ano); 
    dv.list(itensPorAno[ano].map(file => dv.fileLink(file.path)));
}
```

> Abaixo coloque as respostas das perguntas das provas, de acordo com o tipo de questão.
> 
> Caso seja uma questão numérica, escreva entre o número de 0 a 99. (Ex.:13). Caso não queira deixar em branco a questão, apenas deixe em branco. 
> 
> Caso seja uma questão de verdadeiro ou falso, coloque V para verdadeiro e F para falso. Se não quiser responder deixe em branco, entre as virgulas. (Ex.: Q04 V,V,F==, ,==V). Neste exemplo temos para a pergunta Q04 as seguintes respostas:
> 1. Verdadeiro
> 2. Verdadeiro
> 3. Falso
> 4. ==Em Branco==
> 5. Verdadeiro

> Após finalizar a simulação, acesse este link com o > [[Resultado]] <.

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