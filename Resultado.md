---
respostas: "[[Respostas 2025]]"
gabarito: "[[Gabarito 2024]]"
peso:
  macroeconomia: 20
  microeconomia: 20
  matematica: 15
  estatistica: 20
  brasileira: 5
  discursiva: 20
nota_discursiva: 0
mostrar_gabarito: false
obsidianUIMode: preview
---

Escolha a sua folha de respostas e o gabarito:
```dataviewjs
const respostas = dv.pages('"Respostas"').file.name.map(item => "[["+item+"]]")
const gabaritos = dv.pages('"Gabaritos"').file.name.map(item => "[["+item+"]]")

let dropdownresposta = "`INPUT[inlineSelect("
const options_respostas = respostas.map(resposta => `option(${resposta})`);
dropdownresposta += options_respostas.join(',') + '):respostas]`'

let dropdowngabarito = "`INPUT[inlineSelect("
const options_gabarito = gabaritos.map(gabarito => `option(${gabarito})`);
dropdowngabarito += options_gabarito.join(',') + ',showcase):gabarito]`'

// Create a container element
const container = dv.el('div', '');
container.style.display = 'flex';
container.style.gap = '10px';
container.style.alignItems = 'center';

// Create dropdown elements
const respostaPara = dv.paragraph(dropdownresposta);
const gabaritoPara = dv.paragraph(dropdowngabarito);

// Append to container
container.appendChild(respostaPara);
container.appendChild(gabaritoPara);

// Display the container
dv.paragraph(container);
```
Escolha os [[Exame_2025-Manual_do_Candidato-v20240513.pdf#page=6&selection=0,1,2,23|pesos]] de sua instituição:
```dataviewjs
const temas = ["macroeconomia", "microeconomia", "brasileira", "estatistica", "matematica", "discursiva"];

let colocarPesos = temas.map(tema => `${tema}: \`INPUT[number:peso.${tema}]\``);

const container = dv.el('div', '');
container.style.display = 'flex';
container.style.gap = '1px';
container.style.alignItems = 'center';

for (const peso of colocarPesos){

  let localInput = dv.el('div','')
  localInput.style.padding = '1px'
  localInput.style.overflow = 'hidden'; // Cut off overflowing content
  localInput.appendChild(dv.paragraph(peso))
  container.appendChild(localInput);
};

```

Nota da prova discursiva: `INPUT[number:nota_discursiva]`

Mostra respostas do gabarito abaixo? `INPUT[toggle:mostrar_gabarito]`


```dataviewjs
const temas = ["macroeconomia", "microeconomia", "brasileira", "estatistica", "matematica"];

// Get file references
const respostas = dv.page(dv.current().respostas);
const gabarito = dv.page(dv.current().gabarito);

if (!respostas || !gabarito) {
  dv.el("p", "🔴 Arquivos não encontrados. Verifique os links.");
} else {
  const calcularPontos = (gabaritoResposta, minhaResposta) => {
    if (!isNaN(parseFloat(gabaritoResposta))) {
      return parseFloat(minhaResposta) === parseFloat(gabaritoResposta) ? 1 : 0;
    } else {
      if (gabaritoResposta === 'A') {return "🅰️"};
      let divisor = 0
      if(gabaritoResposta.match(/A/g)) {
        divisor += 5 - gabaritoResposta.match(/A/g).length;
      } else {
        divisor += 5
      }
      if (divisor === 0) {return "🅰️"};
      const gabaritoSplit = gabaritoResposta.split(',');
      const minhaSplit = isNaN(parseFloat(minhaResposta)) ? minhaResposta.split(',') : "E,E,E,E,E";
      let pontos = 0;
      for (let i = 0; i < gabaritoSplit.length; i++) {
        if (gabaritoSplit[i] === 'A') continue; // Ignora anulados
        if (minhaSplit[i].trim() === "") continue; // Ignora não respondido
        if (minhaSplit[i] === gabaritoSplit[i]) pontos += 1;
        else pontos -= 1;
      }
      return (pontos/divisor);
    }
  };

  let total = 0;
  const resultados = {};
  const pesoTotal = Object.values(dv.current().peso).reduce((sum, value) => sum + value, 0)

  for (const tema of temas) {
    const gabaritoTema = gabarito.file.frontmatter[tema];
    const respostasTema = respostas.file.frontmatter[tema];
    
    if (!gabaritoTema || !respostasTema) continue;
    
    resultados[tema] = { detalhes: [] };
    
    for (const [questao, gabaritoResposta] of Object.entries(gabaritoTema)) {
      const minhaResposta = respostasTema[questao];
      const pontos = calcularPontos(gabaritoResposta, minhaResposta);
      const anulado = typeof gabaritoResposta === 'string' ? gabaritoResposta.includes("A") : 0;
      resultados[tema].detalhes.push({
        questao,
        pontos: pontos,
        gabarito: gabaritoResposta,
        resposta: minhaResposta,
        status: anulado ? '🅰️' : (pontos > 0.9 ? '✅' : ( pontos > 0 ? '🟡' : '❌'))
      });
    }
    let pontosTema = resultados[tema].detalhes.filter(item => item.pontos !== '🅰️').map(Q => parseFloat(Q.pontos));
    resultados[tema].valorNaoNulos = pontosTema.length;
    resultados[tema].media = pontosTema.reduce((soma, valor) => soma + valor, 0) / resultados[tema].valorNaoNulos;
    resultados[tema].variancia = pontosTema.reduce((soma, valor) => soma + Math.pow(valor - resultados[tema].media,2),0)/resultados[tema].valorNaoNulos;
    resultados[tema].desvioPadrao = Math.sqrt(resultados[tema].variancia);
    resultados[tema].resultadoProva = pontosTema.reduce((soma, valor) => soma + valor, 0)
    resultados[tema].escorePadronizado = (resultados[tema].resultadoProva - resultados[tema].media) / resultados[tema].desvioPadrao;
    resultados[tema].notaSemiFinal = resultados[tema].escorePadronizado * 10 * (dv.current().peso[tema]/pesoTotal);
    total += resultados[tema].notaSemiFinal;
  }

  total += dv.current().nota_discursiva * 10 * (dv.current().peso.discursiva/pesoTotal)

  // Exibição dos resultados
  dv.header(3, `📊 Resultado ANPEC ${gabarito.file.frontmatter.ano}`);
  dv.el("p", `⭐ **Pontuação Total: ${total.toFixed(1)}**`);

  for (const tema of temas) {
    if (!resultados[tema]) continue;
    dv.header(4, `📚 ${tema.toUpperCase()}: ${resultados[tema].resultadoProva.toFixed(1)} pontos, EscoreP: ${resultados[tema].escorePadronizado.toFixed(2)}, comPeso: ${resultados[tema].notaSemiFinal.toFixed(2)}`);
    if(dv.current().mostrar_gabarito){
      dv.table(
      ["Questão", "Gabarito", "Sua Resposta", "Pontos", "Status"],
      resultados[tema].detalhes.map(d => [d.questao, d.gabarito, d.resposta, d.pontos, d.status])
    );
    } else {
    dv.table(
      ["Questão", "Sua Resposta", "Pontos", "Status"],
      resultados[tema].detalhes.map(d => [d.questao, d.resposta, d.pontos, d.status])
    );
    }
  }
}
```

#### Explicação sobre os pontos


É possível encontrar a explicação completa sobre os pontos [[Exame_2025-Manual_do_Candidato-v20240513.pdf#page=20&selection=134,0,134,2|aqui]]. 

**Pontos**: O somatório dos pontos para cada tema.
**EscoreP**: Pontos padronizados pela por essa [[Exame_2025-Manual_do_Candidato-v20240513.pdf#page=20&selection=186,0,227,14|formula]].
**comPeso**: EscoreP de acordo com o [[Exame_2025-Manual_do_Candidato-v20240513.pdf#page=6&selection=0,1,2,23|peso]] dado pela sua instituição. 

 