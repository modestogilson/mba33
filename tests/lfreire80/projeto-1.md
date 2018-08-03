# Sistema de Supervisão Predial

### ENGSOFT 33
### Aluno: Leonardo Freire
---

## Objetivo

Coletar informações de até 5000 sensores de temperatura espalhados em determinados pontos do prédio.

## Requisitos

Cada pontos tem um perfil de temperatura pré definido, os pontos devem ser monitorados a cada 5 segundos, deverá existir um interface para o usuário mostrando um mapa dos pontos e os alarmes.

## Proposta

Seram instalados nos pontos de controle um Raspberry Pi 3 B+ equipados com sensor de temperatura DHT22

![Imagem do Raspberry Pi 3 B](https://image.ibb.co/jiyemK/Raspberry_B_DHT22.png)

Nele teremos instalados além do sistema operacional o Docker CE para executarmos a imagem da aplicação.

Teremos um servidor central para agregação dos dados coletados dos sensores, controle dos sensores e emissor de alertar.

![](https://image.ibb.co/gwMEOz/Untitled_Diagram.jpg)

### Aplicações dos sensores

Nos Raspberry Pi terão dois serviços instalados. 

O primeiro será desenvolvido em .NET Core 2.1 Console Application que fará a leitura dos sensores e armazenamento em memória, para diminuir a latência de resposta dos sensores.

O Segundo será desenvolvido em .NET Core 2.1 Web API para consulta dos dados dos sensores gravados em memória.

Ontem devera tem como resposta um JSON no formato abaixo:

```JSON
{
  "ponto": "1",
  "temperatura": "25",
  "data": "01/07/2018",
  "hora": "13:23"
}
```

### Aplicações do servidor

Uma aplicação ficará responsável por monitorar os dados dos sensores cadastrados no banco de dados e disponibilizar as informações para o a aplicação MVC e para o Alarme.

Outra aplicação do servidor será desenvolvida em .Net Core 2.1 ASP.Net Core 2.1 - MVC em C#, será dividida em duas partes, a primeira será um responsável por controlar o cadastro dos sensores instalados no prédio, será permitido também consulta dos históricos de temperaturas.

A alarme ficará responsável para verificar se algum sensor esta fora dos padrões estabelecidos.







