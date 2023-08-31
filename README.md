# weareables-aws-architecture

<div align="center">
<img src="https://github.com/arthurmeirelessm/weareables-aws-architecture/assets/78212769/d127ff84-3c9e-4d4d-93ca-2179ca90e47d"
" />
</div>



Essa é uma solução que arquitetei envolvendo principalmente de serviços de serveless da AWS, consiste em usos de SDKs externos de weareables de marcas como Apple, Hauwei e xioami, que são marcas referência quando o assunto é pulseira ou relógio inteligente. Em um contexto voltado pra Healthcare, essa arquitetura é basicamante dividida em treze etapas que moldam o que pode ser feito com ela no fim das contas. São elas: 

* **1 - Tratamento e moldagem de dados antes de ser enviado pra AWS:** Trata-se de toda extração de dados dos dispositivos weareables usando SDKs, bibliotecas ou CSVs. Nessa solução, essa etapa se passa por baixo dos panos de um aplicativo mobile como exemplo, que uniria as formas de extração de dados de dispositivos e posteriormente usaria o SDk da AWS pra enviar os dados em qualquer formato específico.

* **2 - Ingestão de dados na AWS:**  
