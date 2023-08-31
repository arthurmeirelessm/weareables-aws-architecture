# weareables-aws-architecture

<br> 

<div align="center">
<img src="https://github.com/arthurmeirelessm/weareables-aws-architecture/assets/78212769/d127ff84-3c9e-4d4d-93ca-2179ca90e47d"
" />
</div>

<br> 

<br> 

This is a solution that I have designed, predominantly employing AWS serverless services. It encompasses the utilization of external wearable SDKs from renowned brands such as Apple, Huawei, and Xiaomi, which are eminent in the realm of smartwatches and wristbands. In a healthcare-oriented context, this architecture is fundamentally segmented into thirteen distinct phases, collectively shaping the comprehensive scope of its capabilities. Three of these phases concentrate on diverse output avenues, comprising APIs, dashboards, and even predictive models generated through machine learning-driven recommendations.



* **1 - Weareables ativos:** São os dispositivos ou pulseira que mandaram informações constantes de pacientes.

<br> 

* **2 - Tratamento e moldagem de dados antes de ser enviado pra AWS:** Trata-se de toda extração de dados dos dispositivos weareables usando SDKs, bibliotecas ou CSVs. Nessa solução, essa etapa se passa por baixo dos panos de um aplicativo mobile como exemplo, que uniria as formas de extração de dados de dispositivos e posteriormente usaria o SDk da AWS pra enviar os dados em qualquer formato específico.

<br> 

* **3 - Ingestão de dados na AWS:**  Após o tratamento externo pré-envio ter sido feito, por ser uma arquitetura que poderá abrigar a chegada de dados inúmeros weareables simultaneos, é usado o AWS IoT Core, aqui ele tem a responsabilidade de ser o ponto de chegada e de armazenamento desses dados que chegam em tempo real via MQTT ou HTTP/HTTPS com uma base de segurança feita por certificados x.509 ou KMS.

<br> 
  
* **4 - Tratamento pós ingestão e armazenamento:** Consiste em um lambda que é acionado por uma regra do AWS IoT Core e assim, trata ou molda os dados que vem da ingestão, posteriormente armazenando esses dados em um bucket do AWS S3.

<br> 

* **5 - Endpoint (API) disponibilizada:** Nessa etapa, é usado um Lambda para extrair e fazer um segundo tratamento, agora voltado para disponibilizar dados em um formato REST

<br> 

* **6 - Gerenciador de APIs que faz comunicação com o Lambda:** A etapa seis se refere ao uso da AWS API Gateway que irá gerenciar nosso endpoint GET de busca a dados especificos passando parâmetros como Id de usuário e Id de Weareable

<br> 

* **7 - Análise de dados:**  Aqui é usado serviços com AWS Glue que extrai dados do bucket S3 que guarda os payloads dos weareables e os tranforma em modelos estruturados de dados. Logo após, é usado o AWS Athena, que faz consultas com SQL voltados pra dados puxados diretamente do AWS S3 ou do AWS Glue, que é o que é usado nesa arquitetura.

<br> 

* **8 - Dashboard:** O responsável pelo dashboard se chama AWS QuickSigth, que nessa situação consegue extrair dados consultados do AWS Athena e transforma esses dados em insights para dashboard, podendo usar o mecanismo de autorização e autenticação chamado AWS Cognito, para o acesso restrito de usuários a sua URL de produção.  

<br> 

* **9 - Modelo de Machine Learning para recomendações:** Aqui temos o cérebro da nossa solução, esse modelo de Machine Learning que usa o AWS Sagemaker é responsável por fazer análises constantes de dados de wearebles e ser capaz de detectar mudanças suspeitas nesses dados podendo identificar doenças, riscos e monitoramento em pacientes, tudo isso, através desses dados que podem levar nível de estresse, batimento cardiaco, anomalias, sono, eletrocardiogramas, temperaturas corporais anormais, calendário mesntrual, pressão arterial e mais.

<br> 

* **10 - Notificador:** Nessa etapa, temos o AWS SNS que será capaz de distribuir esses dados através de tópicos e posteriormente notificando filas do AWS SQS, assim, organizando cada tipo de recomendação por usuário ou Id de weareable feita pelo modelo de Machine Learning.

<br> 

* **11 - Microserviços (Filas):** Após passar pelo notificador AWS SNS, o sistema de filas AWS SQS entra em ação guardando essas respostas de recomendações em filas separadas para que assim cada Lambda possa extrair essas informações de forma independente.

<br> 

* **12 - Notificar usuário:** AWS SES faz a ação de notificar usuários tanto por Email, SMS

<br> 

* **13 - Área de campanhas de saúde:** Área designada a campanhas como recomendações pra venda de planos de saúde, recomendação ou alerta de ida ao médico, alerta de riscos de saúde e etc.       
