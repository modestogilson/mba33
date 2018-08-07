# Sistema de Supervisão Predial

### ENGSOFT 33
### Alunos: Luís César da Costa
            Leno Campos
---

## Objetivo

Coletar informações de até 5000 sensores de temperatura espalhados em determinados pontos do prédio. (Manter o tempo de resposta em 0.5s)

## Requisitos

Cada dispositivo móvel tem um perfil de temperatura pré definido, os dispositivos devem se comunicar informando os dados, deverá ser mantido um tempo de reposta de cada dispoisitivo menor a 0.2s. Recebendo essa informação teremos um servidor que fará a armazenagem dos dados e deve garantir através de um serviço que caso algum dispositivo móvel informe a temperatura acima de 30 graus ou demore mais que 0,8s para responder os alarmes do local onde o mesmo se encontra serão acionados.

## Proposta

Seram instalados nos dispositivos de controle um Raspberry Pi 3 B+ equipados com sensor de temperatura DHT22, onde teremos uma aplicação Leitor que visa uma comunicação direta com o Interceptador que será o centralizador dos dados enviados por cada dispositivo e ficará encarregado do processo de acionamento dos alarmes físicos, obedecendo os requisitos.
Nele teremos instalados além do sistema operacional um servidor de conteúdo com um banco de dados que ficará rodando uma api rest e o serviço de acionamento dos alarmes físicos.
Para acionamento dos alarmes físicos teremos que fazer a identificação de onde o dispoisitivo móvel está para isso usaremos o nome do dispositivo. 

Obedecendo a seguinte regra: 

Andar_Sala_Localização

Andar: O Andar em que o dispositivo está localizado.

Sala: A Sala em que o dispositivo está localizado. 

Localização: será no caso de termos mais de um dispositivo na mesma sala.

1  3

2  4


![](https://image.ibb.co/mdXLbK/Desenho_sem_t_tulo_2.jpg)

### Leitor

A aplicação Leitor será um programa em linguagem baixa (C/C++), que fará a leitura dos dados da temperatura através do componente de leitura acoplado a placa, o programa ao aferir os dados já fará o acionamento do Interceptador.

Segue um exemplo de chamada do Interceptador:

$ curl_time -X GET "http://lima:5000/interceptor/add/{"id": "1", "name":"Mnemonico", "temperatureValue":"23.68", "humidityValue":"75.12", "pressureValue":"101746", "units":"celsius", "timestamp":"2018-07-24T00.99222529+00:00"} -H "accept: text/plain"

Os tempos de cada requisição, estando numa mesma rede gigabit ethernet, e com a latência entre os pontos controlada (esse controle deverá sempre passar por testes afim de garantir os tempos acordados no projeto):

Verificação do dispositivo (0.015s estimativa de tempo)

Conteudo: 

{"Roger that!"}

Requisição das informações (0.18s estimativa de tempo)

Conteudo:

{"id": "1",
 "name":"Mnemonico",
 "temperatureValue":"23.68",
 "humidityValue":"75.12",
 "pressureValue":"101746",
 "units":"celsius",
 "timestamp":"2018-07-24T00.99222529+00:00"
}


### Interceptador

O Interceptador será o programa centralizador dos dados enviados por cada dispositivo (Servidor REST), ficando localizado no mesma estrutura físicados Leitores, encarregado do processo de acionamento dos alarmes físicos, obedecendo os requisitos.
O interceptador recebe através de uma url definida por exemplo http://lima:5000/intercepter/add/, os dados capturados pelo leitor no ambiente onde o mesmo estiver para que sejam armazenados no banco de dados.  

*Ps.: Aqui poderemos criar algum mecanismo para compartilhar a base dos dados (NoSQL) com a aplicação web, de forma que o serviço possa estar disponível mesmo que o usuário esteja fora do ambiente onde estão sendo aferidos os dados.

### Aplicação Web 

Aplicação para exibição dos dados e elaboração dos relatórios, esse serviço será feito usando a arquitetura MVC, com um servidor de aplicação usando Java Server Faces (JSF), Enterprise Java Beans (EJB) e Java Persistence API(JPA).
Usaremos alguns componentes para facilitar a visualização dos dados assim que os mesmos são inseridos na base. 



