
# BOT Monitor de Certidões

Projeto desenvolvido como portfolio para o Projeto de Extensão II do curso de Arquitetura de Dados da Faculdade UNOPAR (2024). Voltado para a comunidade, visa atender a necessidade de um Analista de Licitações (pessoa participante) em acompanhar/manter as certidões de seus clientes atualizadas.

A aplicação permite monitorar, extrair informações, organizar e atualizar o status e informações de certidões em uma planilha. É possível acompanhar as certidões com precisão, destacando aquelas que estão vencidadas ou pendentes, além de manter os dados atualizados em um arquivo Excel.



### Mais informações do Projeto de Extensão

**1. Monitorar as principais certidões elencadas pela pessoa participante (Analista de Licitações), a saber:**

 - [Certificado de Regularidade do FGTS - CRF](https://consulta-crf.caixa.gov.br/consultacrf/pages/consultaEmpregador.jsf)
 - [Certidão Negativa de Distribuição (ações de Falências e Recuperaçõse Judiciais - 1ª e 2ª isntâncias)](https://cnc.tjdft.jus.br/solicitacao-externa)
 - [Certidão Negativa Correcional (ePAD, CGU-PJ, CEIS, CNEP e CEPIM)](https://certidoes.cgu.gov.br/)
- [Certidão Negativa de Débitos Relativos aos Tributos Federais e à Dívida Ativa da União](https://solucoes.receita.fazenda.gov.br/servicos/certidaointernet/pj/emitir)
- [Certidão Negativa de Débitos - GDF](https://ww1.receita.fazenda.df.gov.br/cidadao/certidoes/Certidao)
- [Cadastro Fiscal do Distrito Federal - Comprovante de Inscrição e de Situação no Cadastro Fiscal do Distrito Federal - DIF](https://agnet.fazenda.df.gov.br/area.cfm?id_area=1140)
- [Certidão Negativa de Débitos Trabalhistas](https://cndt-certidao.tst.jus.br/inicio.faces)
- [Certidão Negativa de Improbidade Administrativa e Inelegibilidade](https://www.cnj.jus.br/improbidade_adm/consultar_requerido.php?validar=form)

**2. Clientes Cadastrados**
O participante pode cadastrar seus clientes na planilha `config_clientes` do arquivo `gestao_monitoramento.xlsx`.
Já estão registrados no .xlsx do projeto os clientes fictícios: `Auto data LTDA`, `Bot de Certidao MEI` e `Teste Limitado LTDA`, que servirão de referencia para a criação de "certidões exemplos" baseadas nas elencadas pelo participante.

Também estão resgistrados como clientes os dois primeiros colocados (`Drogaria Rosario` e `BigBox Supermercados`) da lista do [ECONODATA](https://www.econodata.com.br/maiores-empresas/df/supermercados). Foram baixadas suas respectivas certidões para que a aplicação lide tanto com as "certidões exemplos" criadas pelo `gerador_certidoes.ipynb` quanto as originais.





## Funcionalidades
__1. Monitoramento de Certidões:__
* Utiliza parâmetros configuráveis para dectectar automaticamente novas certidões em formato .pdf em uma pasta específica e as adiciona para a lista de monitoramento;
* Renomeia os arquivos para fácil visualização da data de vencimento, caso o arquivo esteja vencido é movido para outra pasta (ex: 'certidoes_vencidas');
* Aponta certidões faltantes.

__2. Extração de Informações:__
* Lê o conteúdo de cada certidão .pdf para extrair seus respectivos dados: data de criação do arquivo; data de início da cetidão; número/código de controle; data de validade; 'nada consta'.

__3. Atualização em Planilha Excel:__
- Insere e organiza os dados extraídos em uma planilha Excel;

__4. Relatórios (/TODO):__
- Gera relatórios com informações de novas certidões, certidões faltantes e certidões vencidas;
- Certidões faltantes ou vencidas: Relatório acompanha url do site para obter a certidão, bem como os dados necessários para obtê-las (CNPJ, nome completo) e nome do arquivo para ser salvo;
- Apresenta lista detalhada com o número de certidões em processo de monitoramento;

## Tecnologias Utilizadas

- **Python:** Linguagem principal do projeto.
- **Pandas:** manipulação de dados no DataFrame para análise e atualização.
- **pdfplumber:** extração de texto de arquivos PDF.
- **openpyxl:** manipulação de arquivos Excel.
- **OS e Datetime:** gerenciamento de arquivos e manipulação de datas.
- **FPDF e Babel:** criação das "certidões exemplo" e formatação das datas destas certidões.

## Instalação

__1. Configuração do Ambiente:__
- Clone o repositório e instale as bibliotecas do projeto executando:
```bash
pip install -r requirements.txt
```

__2. Execução do script gerador_certidões__
- Esse script irá gerar certidões com data de início e vencimento de acordo com os parâmetros de configuração, utilizando o arquivo 'gestao_monitoramento.xlsx' como referência.

```bash
python src/gerador_certidoes.
```

__3. Monitoramento de certidões:__
- Para iniciar o script de monitoramento, execute:
```bash
python src/xxxxxxxxxxxxxxxxxx main.py
```

__4. /TODO Relatório completo:__
- Para gerar relatório completo sobre do estado atual da planilha de monitoramento, execute o script:
```bash
/TODO
```
    
## Estrutura do Banco de Dados no Excel

Este projeto utliza um arquivo .xlsx como banco de dados principal para monitoramento e registros das certidões. Essa escolha foi adotada para atender a preferência do Analista de Licitações, proporcionando uma solução mais familiar e prática para o seu tratalho diário. O arquivo possui as seguintes planilhas:

- `config_certidoes`: Nesta planilha estão presentes os parâmetros das certidões que serão monitoradas, garantindo que o sistema de monitoramento tenha acesso aos detalhes específicos para cada tipo de documento.

| Coluna | Tipo | Descrição|
| :-------- | :--- | :--------|
| `CERTIDAO_ID` | `str` | **Obrigatório**. O ID referente a certidão |
| `NOME_ARQUIVO` | `str` | **Obrigatório**. Nome utilizado como referência para localizar os arquivos em PDF |
| `URL` | `str` | **Obrigatório**. Endereço do site para obter a certidão
| `ORGAO` | `str` | Órgão responsável por emitir a certidão
| `TITULO_CERTIDAO` | `str` | **Obrigatório** Informa o nome / tíulo da certidão

No momento o projeteo funciona apenas com as certidões já elencadas acima.

.......
- `config_clientes`: Aqui é possível adicionar e gerenciar informações dos clientes, facilitando o acompanhamento e a organização de seus documentos e assegurando que os dados estejam estruturados e prontos para o monitoramento.

| Coluna | Tipo | Descrição|
| :-------- | :--- | :--------|
| `CLIENTE_ID` | `str` | **Obrigatório**. O ID referente ao cliente |
| `NOME_CLIENTE` | `str` | **Obrigatório**. Nome (curto) utilizado para identicar o cliente |
| `ATIVO` | `bool` | **Obrigatório**. Se `VERDADEIRO`, então o cliente e suas certidões devem ser monitoradas
| `CNPJ` | `str` | **Obrigatório**. Cadastro Nacional de Pessoa Jurídica - CNPJ utilizado nas certidões
| `NOME_COMPLETO` | `str` | **Obrigatório** Informa o nome completo da pessoa jurídica (é necessário ao criar/validar determinadas certidões)
| `PASTA_DESTINO` | `str` | **Obrigatório**. Aponta qual pasta do sistema podem ser encontradas as certidões referentes deste cliente
| `CERTIDOES_CADASTRADAS` | `str` | **Obrigatório**. Contem uma lista com as ID's das certidões cadastradas relacionadas ao cliente que devem existir o arquivo e serem monitoradas

Os clientes podem ser adicionados livremente nesta planilha. Ela também serve de referência para o script `gerar_certidoes.ipynb` criar certidões fictícias para testar o monitoramento.

A coluna `CERTIDOES_CADASTRADAS` deve ser preenchida com a função do excel `=UNIRTEXTO()`, utilizando `', '` como delimitador, apontando o intervalo da coluna `CERTIDAO_ID` da planilha `cert_config` para concatenar cada item em um texto.

.......
- `db_monitor`: Esta planilha é dedicada ao monitoramento contínuo das certidões. Cada registro atualizado reflete o estado atual de cada certidão monitorada, facilitando a visualização e a gestão do do vencimento. Esta planilha não deve receber dados do usuário.

| Coluna | Tipo | Descrição|
| :-------- | :--- | :--------|
| `CERTIDAO_ID` | `str` | ID referente ao tipo de certidão |
| `CLIENTE_ID` | `str` | ID do cliente a qual pertence a certidão|
| `PASTA_DESTINO` | `str` | O local onde o arquivo da certidão está
| `ARQUIVO` | `str` | Nome do arquivo encontrado
| `STATUS` | `str` | Status da certidão, pode ser: `adicionada`, `monitorando`, `VENCIDA`
| `DATA_INICIO` | `datetime` | Data do início da validade da certidão ou de sua emissão extraída do documento .pdf
| `DATA_VENCIMENTO` | `datetime` | Data de vencimento extraída do documento .pdf.
| `NUMERO_CERTIDAO` | `str` | Número da certidão / Código de autenticação extraído do .pdf
| `NADA_CONSTA` | `bol` | Se `VERDADEIRO` indica que a certidão não possui pendencias/irregularidas naquela certidão (Certidão Negativa) ou é uma Certidão Positiva com Efeitos de Negativa
| `CREATED_AT` | `datetime` | Extrai metadados da data de criação do arquivo .pdf no sistema
| `UPDATED_AT` | `datetime` | Contem a data/hora referente a última atualização do registro dessa certidão
