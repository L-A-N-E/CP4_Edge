<h1 align="center">CP4 - FIWARE e ESP32: Luminosidade :bulb:</h1> 

![banner](https://github.com/L-A-N-E/CP2_Edge_1SEM/assets/153787379/132308ff-27a0-45e7-8323-80d9103f2390)


## Índice :page_with_curl:

  * [Descrição do Projeto](#descrição-do-projeto-memo)
     * [Introdução](#introdução-left_speech_bubble)
     * [ESP32](#esp32-pager)
  * [Acesso ao projeto](#acesso-ao-projeto-file_folder)
  * [Ferramenta utilizada](#ferramenta-utilizada-hammer_and_wrench)
  * [Bibliotecas utilizadas](#bibliotecas-utilizadas-books)
  * [Componentes necessários](#componentes-necessários-toolbox)
  * [Montagem](#montagem-wrench)
     * [Cuidados durante a montagem](#cuidados-durante-a-montagem-warning)
  * [Reprodução](#reprodução-gear)
  * [Pessoas Desenvolvedoras do Projeto](#pessoas-desenvolvedoras-do-projeto-globe_with_meridians)

## Descrição do projeto :memo:

<h3>Introdução :left_speech_bubble:</h3>
<p>
  Nós, da L.A.N.E., após completar o Monitoramento de Ambiente de uma vinícola com o Arduino UNO, recebemos a solicitação de aprimorar o projeto. Para isso, usamos o ESP32 para criar um dispositivo IoT que envia os dados dos sensores para a nuvem, permitindo a visualização e acesso facilitados por meio de uma plataforma dedicada.
</p>
<p>
Decidimos primeiro testar o recebimento dos dados de luminosidade e o envio de instruções para ligar e desligar o LED embutido no ESP32 via Postman. 
</p>
<h3>ESP32 :pager:</h3>
<p>
O ESP32 é um microcontrolador avançado com suporte embutido para Wi-Fi e Bluetooth, facilitando a conexão com a Internet e outros dispositivos. Para coletar e enviar dados de maneira bidirecional, utilizamos uma combinação de tecnologias: o Fiware para gerenciamento de dados e a plataforma Docker no Microsoft Azure para orquestração e execução de containers. O Fiware é uma plataforma de código aberto que oferece uma gama de componentes para construir aplicações inteligentes, enquanto o Docker permite a criação e o gerenciamento de ambientes isolados e escaláveis para aplicações. A Microsoft Azure fornece a infraestrutura em nuvem necessária para hospedar e escalar esses serviços.
</p>
<p>
Para monitorar e visualizar o fluxo de dados do ESP32, utilizamos o Postman, uma ferramenta que facilita a execução de requisições HTTP e a análise de respostas. Com o Postman, podemos testar as APIs, verificar a integração dos dados e garantir que as postagens e consultas ao servidor estejam funcionando conforme o esperado.
</p>
 
## Acesso ao projeto :file_folder:

Você pode acessar o [código do projeto](CP4.ino) ou a [simulação feita no Wooki](https://wokwi.com/projects/406654345905426433)

## Ferramenta utilizada :hammer_and_wrench:

- ``Arduino IDE``
  
## Bibliotecas utilizadas :books:

- ``WiFi``
- ``PubSubClient``
  
## Componentes necessários :toolbox:

|   Componente   | Quantidade |
|:--------------:|:----------:|
| ESP32  |      1     |
| Módulo LDR - 4 terminais |      1     |
|      Jumper     |     3     |
|    Cabo USB    |      1     |

## Montagem :wrench:

<details>
  <summary>Imagem da Montagem</summary>
  <img src="https://github.com/user-attachments/assets/fd50f348-c41e-4aef-ab91-aeb9e24405e8">
</details>

<h3>Cuidados durante a montagem :warning:</h3>

- ``1.`` Conectando o Cabo USB:
  - ``1.1.``Na hora de conectar o cabo com o ESP32, é preciso ter muito cuidado, pois a solda pode descolar, então seja cuidadoso!

- ``2.`` Conectando o LDR:
  - ``2.1.`` Nesta segunda parte, mudamos o LDR para um Módulo LDR com 4 terminais no qual possui a opção da saída dos dados analógicos ou digitais. Com isso, nesse projeto, continuamos usando a entrada analógica. Então, verifique se o cabo que está conectado ao D34 do ESP32 está  conectado ao A0 do LDR.
  - ``2.2.`` Conecte o VCC no terminal positivo (3V3) e o GND no terminal negativo (GND);
  - ``2.3.`` Relaxe, um dos terminais do LDR ficará sem conectar, pois esse é onde sai os dados digitais;

## Reprodução :gear:

- ``1.`` Após a montagem do projeto, é necessário inserir o código por meio de um computador que possui o programa Arduino IDE instalado;
- ``2.``Ao abrir a IDE, é necessário fazer algumas coisas para selecionar o ESP32:
  - ``2.1.`` Clique em **Arquivo** > **Preferências**.
    - ``2.1.1.`` No campo **URLs Adicionais para Gerenciadores de Placas**, adicione o seguinte link: *https://dl.espressif.com/dl/package_esp32_index.json*;
  - ``2.2.`` Clique em **Ferramentas** > **Placas** > **Gerenciar Placas**.
    - ``2.2.1.`` Na janela que se abre, digite *ESP32* na caixa de pesquisa;
    - ``2.2.2.`` Selecione a plataforma *esp32* da lista e clique em Instalar;
  - ``2.3.`` Após a instalação, vá novamente em **Ferramentas** > **Placas**.
    - ``2.3.1.`` Você verá uma nova opção para selecionar as placas ESP32. Escolha a placa específica que você está usando;
- ``3.`` Baixe as [bibliotecas necessárias](#bibliotecas-utilizadas-books) no Arduino IDE;
- ``4.`` Faça as devidas modificações no código disponível:
  
  ```cpp
    const char* default_SSID = "SUA_INTERNET"; // Nome da rede Wi-Fi 
    const char* default_PASSWORD = "SENHA_DA_SUA_INTERNET"; // Senha da rede Wi-Fi 
    const char* default_BROKER_MQTT = "IP_PÚBLICO"; // IP do Broker MQTT 
  ```

  - ``4.1.`` Substitua a "SUA_INTERNET" pelo nome de sua internet;
  - ``4.2.`` Substitua a "SENHA_DA_SUA_INTERNET" pela senha de sua internet;
  - ``4.3.`` Substitua o "IP_PÚBLICO" pelo ip do servidor do Cloud Service de sua preferência:
    - ``4.3.1.`` Não disponibilizamos o IP por motivos de segurança. Para testar este código, você precisará de um serviço de nuvem, como Azure ou AWS. Além disso, será necessário instalar o FIWARE e o Docker nesse serviço e, por fim, abrir as portas necessárias. 
- ``5.`` Transferir o código do computador para  o ESP32 por meio do Cabo USB;
- ``6.`` Teste o sistema para verificar se ele está recebendo instruções e enviando dados via Postman;
- ``7.`` Com tudo montado e pronto, é necessário levá-lo para o ambiente em que será implementado e ligá-lo á uma fonte;

<p align='center'><i>OBS: Se o ESP32 for uma versão mais antiga, pode ser necessário pressionar o botão BOOT na placa durante a transferência do código </i></p>

## Pessoas Desenvolvedoras do Projeto :globe_with_meridians:

| [<img src="https://avatars.githubusercontent.com/u/101829188?v=4" width=115><br><sub>Alice Santos Bulhões</sub>](https://github.com/AliceSBulhoes) |  [<img src="https://avatars.githubusercontent.com/u/163866552?v=4" width=115><br><sub>Eduardo Oliveira Cardoso Madid</sub>](https://github.com/EduardoMadid) |  [<img src="https://avatars.githubusercontent.com/u/148162404?v=4" width=115><br><sub>Lucas Henzo Ide Yuki</sub>](https://github.com/LucasYuki1) | [<img src="https://avatars.githubusercontent.com/u/153787379?v=4" width=115><br><sub>Nicolas Haubricht Hainfellner</sub>](https://github.com/NicolasHaubricht) |
| :---: | :---: | :---: | :---: |
| RM:554499 | RM:556349 | RM:554865 | RM:556259 |

