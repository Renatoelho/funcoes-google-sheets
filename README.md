# Google Sheet: Criando uma Função Personalizada com Apps Script

Neste vídeo, você aprenderá como criar funções personalizadas no **Google Sheets** utilizando o Apps Script. As funções que serão criadas incluem uma para calcular a idade com base em uma **data de nascimento** e outra para buscar informações detalhadas de um **CEP** utilizando uma API. Essa funcionalidade é útil para realizar cálculos ou operações que **não são cobertas** pelas fórmulas nativas do Google Sheets.

Essa função personalizada será implementada em **Apps Script**, a plataforma de scripts da Google baseada em **JavaScript**, que permite automatizar tarefas e estender as funcionalidades do Google Workspace. O Apps Script utiliza uma versão baseada no **ECMAScript 5**, o que significa que algumas funcionalidades mais modernas do JavaScript podem não estar disponíveis, mas fornece robustez para criar soluções personalizadas.

<!--
-->

## Apresentação em vídeo

<p align="center">
  <a href="https://www.youtube.com/@renato-coelho" target="_blank"><img src="imagens/thumbnail/thumbnail-google-sheet.png" alt="Vídeo de apresentação"></a>
</p>

### Requisitos

+ ![Conta Google](https://img.shields.io/badge/Conta%20Google-Necessária-E3E3E3)

+ ![Navegador](https://img.shields.io/badge/Navegador-Atualizado-E3E3E3)

+ ![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Ativo-E3E3E3)

+ ![Apps Script](https://img.shields.io/badge/Apps%20Script-Habilitado-E3E3E3)

## Criando a Função Personalizada

### Passos

1. **Abra o Google Sheets**
   - Crie ou abra uma planilha existente.

2. **Acesse o Apps Script**
   - Clique em **Extensões** > **Apps Script**.

3. **Escreva o Código da Função**
   Substitua o conteúdo do editor por este código:

   ```javascript
   function calcularIdade(dataNascimento) {
     const hoje = new Date();
     const nascimento = new Date(dataNascimento);
     let idade = hoje.getFullYear() - nascimento.getFullYear();
     const mes = hoje.getMonth() - nascimento.getMonth();

     if (mes < 0 || (mes === 0 && hoje.getDate() < nascimento.getDate())) {
       idade--;
     }

     return idade;
   }
   ```

4. **Salve e Implante o Script**
   - Clique em **Salvar** e dê um nome ao projeto.

5. **Utilize a Função no Google Sheets**
   - Em uma célula, digite:
     ```
     =calcularIdade("1990-01-01")
     ```
   - Substitua a data pelo valor desejado.

6. **Exemplo Adicional: Busca de CEP**
   Também é possível criar funções personalizadas mais complexas. Por exemplo, uma função para buscar informações de um CEP via API:

   ```javascript
   function buscaCEP(cep) {
     if (!cep) return [["CEP inválido ou não informado"]];

     cep = cep.toString().padStart(8, '0');

     const url = `https://viacep.com.br/ws/${cep}/json/`;
     
     try {
       const response = UrlFetchApp.fetch(url);
       const data = JSON.parse(response.getContentText());
       
       if (data.erro) {
         return [[`Erro: CEP ${cep} não encontrado`]];
       }
       
       return [[
         data.cep || "N/A",
         data.logradouro || "N/A",
         data.complemento || "N/A",
         data.bairro || "N/A",
         data.localidade || "N/A",
         data.uf || "N/A",
         data.ibge || "N/A",
         data.gia || "N/A",
         data.ddd || "N/A",
         data.siafi || "N/A"
       ]];
     } catch (e) {
       return [[`Erro ao acessar a API: ${e.message}`]];
     }
   }
   ```

   Para utilizar esta função, insira na célula do Google Sheets:
   ```
   =buscaCEP("01001000")
   ```

## Demonstração

A função `calcularIdade` é invocada diretamente em uma célula do Google Sheets, retornando a idade com base na data de nascimento informada. De forma similar, a função `buscaCEP` realiza a consulta de informações baseadas no CEP fornecido.

### Exemplo de Resultado:

| Data de Nascimento | Idade | CEP       | Logradouro   | Localidade |
|---------------------|-------|-----------|--------------|------------|
| 1990-01-01         | 34    | 01001000  | Praça da Sé | São Paulo  |
| 2000-05-15         | 24    | 30140071  | Rua Curitiba | Belo Horizonte |

## Referências

Automatize e estenda o Google Workspace com um código simples, ***Google Workspace.*** Disponível em: <https://developers.google.com/apps-script?hl=pt-br>. Acesso em: 02 Jan. 2025.

Funções personalizadas no Planilhas Google, ***Google Workspace.*** Disponível em: <https://developers.google.com/apps-script/guides/sheets/functions?hl=pt-br>. Acesso em: 02 Jan. 2025.


ECMAScript Language Specification, ***ECMA International.*** Disponível em: <https://262.ecma-international.org/5.1/>. Acesso em: 02 Jan. 2025.
