# prj_uiPath_DownloadCNPJGovernoFederal

## 💻 Pré-requisitos
> Software Desenvolvido em UiPath Studio Community 2025.0.157

prj_DispatcherDownloadDadosCNPJGovernoFederal (Processo):
 - UiPath.System.Activities: v23.10.6;
 - UiPath.Mail.Activities: v1.23.11;
 - UiPath.UIAutomations.Activities: v24.10.10 ( Tive Problemas em utilizar a atividade de "Extração de Tabela" em versões menores que essa, por isso, foi necessário o update ).
  
prj_PerformerDownloadCNPJGovernoFederal (Robotic Enterprise Framework):
 - UiPath.System.Activities: v23.10.6;
 - UiPath.Mail.Activities: v1.23.11;
 - UiPath.Excel.Activities: v2.24.4;
 - UiPath.Testing.Activities: v24.10.3;
 - UiPath.UIAutomations.Activities: v23.10.13.

Arquivos com nome da Fila do Orchestrator (Fila_prjDownloadDadosCNPJGovernoFederal):
  - prj_DispatcherDownloadDadosCNPJGovernoFederal\FilaOrchestrator.csv;
  - prj_PerformerDownloadCNPJGovernoFederal\Data\Config.xlsx.

Plataforma de E-mail utilizada:
 * https://ethereal.email/
 * Credenciais do e-mail salvas em: "prj_PerformerDownloadCNPJGovernoFederal\Data\Config.xlsx" e "prj_DispatcherDownloadDadosCNPJGovernoFederal\credentials.csv";

Site Principal para Automação:
 * https://dados.gov.br/dados/conjuntos-dados/cadastro-nacional-da-pessoa-juridica---cnpj


## Apresentação
> O Processo foi dividido em 2 projetos, no modelo Dispatcher e Permorfer. A ideia além de separar as responsabilidades, também foi de pensar em alguns pontos como:
- Programação de horários diferentes para a execução de cada processo no orchestrator;
- Exemplo, verificar se o site atualizou as informações, programar para executar o processo do dispatcher às 17h00 horas. Porém o Permorfer executar às 02h00 da manhã, por ser um processo de download de dados e alguns horários podem ter menos instabilidades;
- Programar para executar o processo do Performer após algum item ser adicionado na Fila.


## prj_DispatcherDownloadDadosCNPJGovernoFederal

> O processo é feito a partir do acesso ao site coletando os dados necessários para prenchimento da Fila. A Fila é preenchida com os nomes, links e datas de atualização de cada arquivo. Há uma regra de negócio validando o prenchimento da fila, caso exista o mesmo item na fila marcado como "New" ou "Sucesso" é verificado a "Data de Atualização" desse arquivo novo que acabou de ser buscado no site. Caso o dado que acabou de ser buscado no site a data de utilização seja diferente do item que está na fila, esse dado foi atualizado no site e por isso precisa ser adicionado na Fila de processamento ( Foi feito essa lógica de validação, pois verificar a última data de modificação do arquivo na pasta da rede, poderia apresentar falhas na lógica pois o usuário poderia alterar a pasta, adiconando dados e alterando os itens. E como os arquivos "zip" são excluídos não seria possível verificar a hora exata do download daquele arquivo ).
Caso nenhum Item seja adicionado (ou seja, a data de atualização tenha sido alterada) é enviado um E-mail informando que "Não Há arquivos novos disponíveis". 

Componentes utilizados:
- Seletores;
- Âncoras;
- GetText (Coleta de informações, como "nome do arquivo", "url" , "link de acesso", "data de modificação");
- Extração de Tabela (Extração de dados do site para preenchimento e organização de Fila de Processamento "https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/2025-01/");
- Envio de E-mail.

Execução do processo prj_DispatcherDownloadDadosCNPJGovernoFederal:

https://github.com/user-attachments/assets/8b1b585a-69b5-4e73-9f97-d884b8278e58


Caso nenhum Item seja adicionado na Fila o E-mail é enviado:
![Email_Sem_Itens](https://github.com/user-attachments/assets/8244dbcd-2d67-4d58-98cb-09044563d136)


## prj_DispatcherDownloadDadosCNPJGovernoFederal:
> O Processo é feito através do processamento de itens da Fila. As Urls com os links para downloads são feitos e também é verificado se o item é do "zip", caso seja, o arquivo é descompactado e excluído o arquivo ".zip".

Componentes utilizados:
- Download File From URL (Busca diretamente através da URL, atividade fica aguardando até o download ser concluído);
- Extract Unzip Files;
- Delete File;
- Envio de E-mail (End Process).

Execução do Processo prj_PerformerDownloadCNPJGovernoFederal

https://github.com/user-attachments/assets/b2787130-9ebf-408b-bb49-1277b51583a0


Envio de E-mail informando que novos itens foram baixados:

> ![Email_ItemsBaixados](https://github.com/user-attachments/assets/844f5614-1e8f-4688-be7c-e1851c07d90c)


Pasta com os arquivos baixados:
> ![PastaRedeArquivosBaixados](https://github.com/user-attachments/assets/2f7f8b70-3b07-4cea-b528-a2f160617485)


## Pontos de melhorias para ajustes futuros:
> * Melhorar a lógica do Performer para execução em modo Paralelo do download de dados;
> * Utilizar as credenciais e dados de e-mail e site em Assets no Orchestrator;
> * Refinar a lógica do Dispatcher para validação de arquivos que não foram atualizados no site e não precisam de downloads.
<!---
Seja um dos contribuidores<br>



