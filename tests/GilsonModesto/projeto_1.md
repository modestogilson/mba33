# Sistema de Supervisão Predial

### ENGSOFT 33
### Aluno: Gilson Modesto
---

## Objetivo

Coletar informações de até 5000 sensores de temperatura espalhados em determinados pontos do prédio.

## Requisitos

Cada ponto será identifcado com uma tag, os pontos devem ser monitorados a cada 5 segundos, deverá existir um interface para o usuário mostrando um mapa dos pontos
 e os alarmes.

## Proposta

Seram instalados nos pontos de controle um Raspberry Pi 3 B+ equipados com sensor de temperatura DHT22

Arquitetura de cada estação:
	- Docker ce
	- Aplicação desenvolvida em .Net Core 2.1 que ficará responsável por ler os dados de temperaturas do sensor de segundo em segundo e reponder com a ultima
temperatura lida, quando solicitado através da api.	

A resposta da api é um JSON no formato abaixo:

```JSON
{
  "tag": "1",
  "temperatura": "25",
  "data": "01/07/2018",
  "hora": "13:23"
}
```

### Aplicações do servidor

Uma aplicação ficará responsável por monitorar os dados dos sensores cadastrados no banco de dados e disponibilizar as informações para o a aplicação MVC e para o Alarme.

Outra aplicação do servidor será desenvolvida em .Net Core 2.1 ASP.Net Core 2.1 - MVC em C#, será dividida em duas partes, a primeira será um responsável por controlar o cadastro dos sensores instalados no prédio, será permitido também consulta dos históricos de temperaturas.

A alarme ficará responsável para verificar se algum sensor esta fora dos padrões estabelecidos.







