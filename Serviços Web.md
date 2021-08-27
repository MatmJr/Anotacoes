# Fundamentos de Arquitetura de Sistemas

## O que são serviços Web?

São soluções para aplicações se comunicarem independente de linguagem, softwares e hardwares utilizados. Podemos dizer que os serviços web são API's que se comunicam por meio de redes sobre o protocolo HTTP.

<b>Obs.:</b> Os principais métodos HTTP são: GET - solicita a representação de um recurso, POST - solicita a criação de um recurso, DELETE - solicita a exclusão de um recurso, PUT - solicita a atualização de um recurso. Os principais códigos de Estado, são: 1xx - Informativo, 2xx - Sucesso, 3xx-Redirecionamento, 4xx - Erro do Cliente, 5xx - Erro do Servidor. 

<b>Def.: </b> XML (Extensible Markup Language): é uma linguagem de marcação criada na década de 90 pela W3C para facilitar a separação de conteúdo sem limitações na criação de tags. Linguagem comum para integração entre aplicações.

<b> Obs </b>  .: foram criados para a troca de mensagem utilizando XML sobre o protocolo HTTP com identificação URI.

Vantagens: 

- Linguagem Comum
- Integração
- Reutilização de implementação
- Segurança
- Custos

Principais Tecnologias:

- SOAP (Simple Object Access Protocol)): protocolo baseado em xml para acessar serviços web por HTTP. Foi desenvolvido para facilitar a integração entre aplicações. 

  Vantagens: 

  <i> 1 </i>.  Permite integração entre aplicações, independente de linguagem, pois usa o XML como linguagem comum.

  <i> 2</i>.  É independente de plataforma e Software

  <i>3</i>.  Meio de transporte genérico, pode ser usados por outros protocolos além do HTTP.

  

  Estrutura SOAP:

  i. SOAP Envelope: é o primeiro elemento do documento e é usado para encapsular toda a mensagem SOAP.

  ii. SOAP Header: é o elemento que possui informações de atributos e metadados da requisição.

  iii. SOAP Body: é o elemento que contém os detalhes da mensagem.  

  

  <b>Def: </b> XSD (XML Schema Definition): é um schema no formato XML usado para definir a estrutura de dados que será validada no XML. O XSD funciona como uma documentação de como se deve ser montado o SOAP Message que será enviado através do serviço Web.

  

  <b>Def.:</b> WSDL (Web Services Description Language): usado para descrever Web Services, funciona como um contrato do serviço. A descrição é feita em um documento XML, onde é descrito o serviço, especificações de acesso , operações e métodos. 

  

- REST (Representational State Transfer): é um estilo de arquitetura de software que define a implementação de um serviço web. Podem trabalhar com os formatos XML, JSON ou outros.

- API (Application Programming Interface): São conjuntos de rotinas documentados e disponibilizados por uma aplicação para que outras aplicações possam consumir suas funcionalidades. Ficou popular com o aumento dos serviços web.  

  <b>Obs.:</b> Quando uma aplicação web disponibiliza um conjunto de rotinas e padrões através de serviços web ela é chamada de API

- JSON (JavaScript Object Notation): Possui formatação leve utilizada para troca de mensagens entre sistemas. Usa-se de uma estrutura de chave e valor e também de listas ordenadas. Um dos formatos mais populares e mais utilizados para troca de mensagens entre sistemas.

EXTRA: **ACID** é um conceito que se refere às quatro propriedades de transação de um sistema de banco de dados: **A**tomicidade, **C**onsistência, **I**solamento e **D**urabilidade.

- Atomicidade: Em uma transação envolvendo duas ou mais partes de informações  discretas, ou a transação será executada totalmente ou não será  executada, garantindo assim que as transações sejam atômicas.

- Consistência: A transação cria um novo estado válido dos dados ou em caso de falha  retorna todos os dados ao seu estado antes que a transação foi iniciada.

- Isolamento: Uma transação em andamento mas ainda não validada deve permanecer  isolada de qualquer outra operação, ou seja, garantimos que a transação  não será interferida por nenhuma outra transação concorrente.

- Durabilidade: Dados validados são registados pelo sistema de tal forma que mesmo no  caso de uma falha e/ou reinício do sistema, os dados estão disponíveis  em seu estado correto.

## Conceitos de arquitetura em aplicações para Internet

Tipos de Arquitetura

- Monolito: 
  	<b>Prós</b>: Baixa Complexidade e Monitoramento Simplificado

  ​	<b>Contras</b>: Stack Única, Compartilhamento de Recursos, Acoplamento, Escalabilidade mais Complexa



- Microserviços: Serviçoes em paralelo (pode ter , ou não, um gerenciador).

  ​	<b> Prós</b>: Stack Dinâmica Simples Escalabidade

  ​	<b> Contras</b>: Acoplamento, Monitoramento mais Complexo, Provisionamento mais complexo

Micro serviços é uma maneira particular de desenvolver aplicações de  maneira que cada módulo do software é um serviço standalone cujo deploy e escala acontecem de maneira independentes da “aplicação principal”.  Enquanto na arquitetura tradicional de software, chamada monolítica,  quebramos uma grande aplicação em bibliotecas, cujos objetos são  utilizados in-process, em uma aplicação modular como proposta na  arquitetura de microservices cada módulo recebe requisições, as processa e devolve ao seu requerente o resultado, geralmente via HTTP.

A ideia não é exatamente nova, é usada em ambientes Unix desde a  década de 60, mas recentemente se tornou o epicentro de uma grande  revolução na forma como as empresas estão desenvolvendo software ágil  baseado em equipes enxutas responsáveis por componentes  auto-suficientes.

## Conceitos de Internet das Coisas (IoT)

Os principais elementos da internet das coisas são: Things, Cloud, Intelligence.

<b> Computação Ubíqua: </b> A primeira foi a fase da computação foi a era dos Mainframes, a segunda foi a era da Computação Pessoal (pessoas e máquinas disputando espaço) e a próxima fase a tecnologia irá recuar para o pano de fundo de nossas vidas começará, assim, computação Ubíqua a terceira era da computação.

Para determinar as tecnologias a serem usadas na camada de Things, deve-se levar em consideração os seguintes atributos: Baixo Consumo Energético, Rede de dados, Resiliência, Segurança, Customização, Baixo Custo.

Modelos Usadas na camada Things:

- Modelo Cliente/servidor: Servidor não conhece o cliente, modelo sincrono.

- Modelo Publish/Subscribe: Sepação entre fonecedor e consumidor da Mensagem, grande poder de escalabilidade.

  Exemplo : GPS em Carros

  Envio das informações

  ​	GPS -- PUBLISH --> MQTT Broker 

  Tópico: pub mqtt://my-tracker.com/d7k9a1/gps/position {localização}

  Estrutura do Tópico: protocolo -> Broker -> usr ID -> sensor -> Information 

  Consumo das Informações

  ​	sub mqtt://broker/user/gps/position

  obs.: '+' todos os usuários e '#' todas as informações.

  ​		



