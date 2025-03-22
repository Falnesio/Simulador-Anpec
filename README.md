Auxílio por meio de simulado para estudo da Anpec

`BUTTON[iniciarSimulado]` `BUTTON[criarGabarito]`

```meta-bind-button
label: Iniciar simulado
style: default
class: iniciar-anpec-button
cssStyle: "background-color: #4CAF50; color: white; padding: 10px 20px; border-radius: 5px;"
backgroundImage: ""
tooltip: "Iniciar o simulado da Anpec"
id: iniciarSimulado
hidden: true
actions:
  - type: templaterCreateNote
    templateFile: assets/template-cartao-resposta.md
    folderPath: Respostas
    fileName: Respostas ano
    openNote: true
    openIfAlreadyExists: false
```
```meta-bind-button
label: Criar um gabarito novo
style: default
class: iniciar-anpec-button
cssStyle: "background-color: #c3d442; color: white; padding: 10px 20px; border-radius: 5px;"
backgroundImage: ""
tooltip: "Criar um novo gabarito Anpec"
id: criarGabarito
hidden: true
actions:
  - type: templaterCreateNote
    templateFile: assets/template-cartao-gabarito.md
    folderPath: Gabaritos
    fileName: Gabarito ANO
    openNote: true
    openIfAlreadyExists: false
```



```dataviewjs
const copyleft = '<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/Falnesio/encontrar_ati">Simulado Obsidian da Anpec</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://falnes.io/">Falnésio GS Borges</a> is licensed under <a href="https://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""></a></p>'
dv.paragraph(copyleft);
```


![[qr-code-plus.svg|200]]
# Se não tiver pix, pode me incentivar a mexer nesse projeto por paypal ou cartão de crédito :)

<iframe id='kofiframe' src='https://ko-fi.com/falnesio/?hidefeed=true&widget=true&embed=true&preview=true' style='border:none;width:70%;padding:4px;background:#f9f9f9;' height='650' title='falnesio'></iframe>