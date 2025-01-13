# prj_uiPath_DownloadCNPJGovernoFederal

## 💻 Pré-requisitos

* Software Desenvolvido em UiPath Studio Community 2025.0.157
* prj_DispatcherDownloadDadosCNPJGovernoFederal (Processo)
        - UiPath.System.Activities: v23.10.6
        - UiPath.Mail.Activities: v1.23.11
        - UiPath.UIAutomations.Activities: v24.10.10 (Tive Problemas em utilizar a Extração de Tabela em versões menores, por isso foi necessário o update)
  
* prj_PerformerDownloadCNPJGovernoFederal (Robotic Enterprise Framework)
        - UiPath.System.Activities: v23.10.6
        - UiPath.Mail.Activities: v1.23.11
        - UiPath.Excel.Activities: v2.24.4
        - UiPath.Testing.Activities: v24.10.3
        - UiPath.UIAutomations.Activities: v23.10.13

* Arquivos com Nome da Fila Orchestrator "Fila_prjDownloadDadosCNPJGovernoFederal" :
  - prj_DispatcherDownloadDadosCNPJGovernoFederal\FilaOrchestrator.csv
  - prj_PerformerDownloadCNPJGovernoFederal\Data\Config.xlsx

Plataforma de E-mail utilizada:
 * https://ethereal.email/
 * Site Principal para Automação: https://acme-test.uipath.com/](https://dados.gov.br/dados/conjuntos-dados/cadastro-nacional-da-pessoa-juridica---cnpj)


## Apresentação

Acesso a plataformar https://acme-test.uipath.com/login para leitura de dados "Items de Trabalho". É feito a leitura, classificação e armazenamento desses dados em arquivos.

Componentes utilizados:
- Leitura e Gravação de arquivos Excel;
- Navegação em Browser;
- Seletores;
- Credenciais (Login e Senha)
- Data Scraping (Leitura de Dados de Página Web)

## Vídeo de Apresentação 
https://github.com/user-attachments/assets/68e77a50-6352-4bf0-888a-176232f1dd0d


![WorkItems](https://github.com/user-attachments/assets/ede4477f-33e4-4a89-bfdb-a4324dca489e)



## Pontos de melhorias não Implementados


<!---
Seja um dos contribuidores<br>



