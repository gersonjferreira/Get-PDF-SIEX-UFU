# Get PDF SIEX UFU

Código js para baixar automaticamente lista de PDFs de uma tabela do SIEX. Este código é um quebra galho e pode falhar. Se necessário, compare o loop abaixo com a função semelhante que está no código fonte da página e faça alterações.

Abra o site do SIEX e filtre de acordo com suas necessidades. Assim que estiver na página com a lista filtrada pronta, faça:

1. Abra o console JS. Tipicamente com o atalho `F12` ou `CTRL+SHIFT+I` e busque pela aba console.
2. Para poder colar códigos digite `permitir colar` ou `allow pasting`.
3. Rode o código abaixo para atualizar o limite de linhas da lista para um número alto o suficiente: 999999. Aguarde alguns segundos para o *reload*  finalizar.

```js
jQuery("#list").jqGrid('setGridParam', { rowNum: 999999 }).trigger('reloadGrid');
```

4. Pegue a lista de `ids` com o comando abaixo e verifique se o número de elementos bate com o número de linhas que você quer baixar.

```js
var ids = jQuery("#list").jqGrid('getDataIDs');
print(len(ids))
```

5. Rode o loop abaixo para baixar todos os arquivos. O navegador deve pedir autorização para baixar vários arquivos.

```js
for (var i = 0; i < ids.length; i++) {
    var id = ids[i];
   
    var parameters = new Object();
    parameters.acao_id = id;
   
    var report = new Object();
    report.parameters = parameters;
    report.report_name = "acao_dados_informacionais";
    var titulo = "Dados Informacionais de Ação";
    report.output = "pdf";
   
    // Ajustado para incluir o ID no nome do arquivo, evitando que um substitua o anterior
    report.filename = "Dados_Informacionais_Acao_" + id + ".pdf";
    report.content_type = "application/pdf";
    report.content_disposition = "attachment";
   
    // Comando que gera e dispara o download do relatório para o ID atual
    reportCreate("report", report);
}
```

## Contribuições

Código desenvolvido pelo Prof. Gerson durante conversas no curso de Física Computacional de 2026, com auxílio dos estudantes Thiago Tome Costa Moreira e Lucas Dias Rodrigues.
