# Projeto Estação Remota

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

![](https://image.ibb.co/mdXLbK/Desenho_sem_t_tulo_2.jpg)

### Aplicação dos sensores

A aplicação será desenvolvida em .NET Core 2.1 utilizando ASP.NET Core 2.1 - Web API em C#, sua função básica será expor um API para leitura dos dados do sensor.

Este API deverá ser acessada através do caminho  https://<ip_do_ponto>/api/v1/temperatura

Ontem devera tem como resposta um JSON no formato abaixo:

```JSON
{
  "ponto": "1",
  "temperatura": "25",
  "data": "01/07/2018",
  "hora": "13:23"
}
```

### Aplicação do servidor

A aplicação do servidor será desenvolvida em .Net Core 2.1 ASP.Net Core 2.1 - MVC em C#, será dividida em duas partes, a primeira será um responsável por acessar os pontos de medições cadastrados a cada 5 segundos, coletar suas informações e registrá-las em um banco de dados MongoDb. A segunda parte será reponsável por gerencias as pontos de acessos, seus alarmes assim como o dashboard de monitoramento. A aplicação poderá ser acessada via navegador web mediante a autenticação de login e senha, de qualquer maquina na rede.






