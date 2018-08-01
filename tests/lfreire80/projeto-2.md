# Sistema de Coleta de Clima

### ENGSOFT 33
### Aluno: Leonardo Freire
---

## Objetivo

Coletar informações de até 50000 sensores de temperatura espalhados em determinados do mapa.


## Requisitos

Cada pontos tem um perfil de temperatura pré definido, as estações devem enviar os dados para um servidor central, deverá existir um interface para o usuário mostrando um mapa dos pontos e os alarmes.

## Proposta

Serão instalados nos pontos de controle um Raspberry Pi 3 B+ equipados com sensor de temperatura DHT22 e Geo Localização

![Imagem do Raspberry Pi 3 B](https://image.ibb.co/jiyemK/Raspberry_B_DHT22.png)

Nele teremos instalados além do sistema operacional e o Python 2.5

Teremos um servidor central na nuvem para agregação dos dados coletados dos sensores, e emissor de alertar.

![](https://image.ibb.co/g6x1iz/Desenho_sem_t_tulo_3.jpg)

### Aplicação dos sensores

A aplicação será desenvolvida python a mesma fará a leitura dos sensores e criara logs com os dados necessários.
Nas estações teremos instalado o Filebeat para envio dos logs para um servidor remoto no nuvem.

```JSON
{
  "estacao": "000001",
  "temperatura": "25",
  "data": "01/07/2018",
  "hora": "13:23",
  "localizacao": "-22.8718846,-43.3605381"
}
```

### Aplicação do servidor

A aplicação servidor ficara hospedada em um servidor de nuvem com a Stack ELK (Logstash, ElasticSearch e Kibana) pronta para receber os logs enviados pelo Filebeat, que receberam os dados emitidos pelas estações espalhadas pelo mundo, onde será possível configurar através do Kibana os dashboards de acompanhamento.


