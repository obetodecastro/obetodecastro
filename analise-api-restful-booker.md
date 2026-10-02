Análise da API Restful Booker

Para esta atividade, escolhi a API Restful Booker, que é uma API criada para praticar testes e integração de APIs.

A API trabalha com reservas de hotel. Para entender melhor como funciona a comunicação entre um sistema e uma API, analisei dois endpoints:

GET /booking/{id} — para consultar uma reserva.

POST /booking — para criar uma nova reserva.

A URL principal da API é:

https://restful-booker.herokuapp.com

A documentação utilizada foi:

https://restful-booker.herokuapp.com/apidoc/index.html

1. GET — Consultar uma reserva
Identificação e finalidade

Endpoint/Rota:

/booking/{id}

Objetivo de negócio:

Esse endpoint serve para consultar uma reserva específica. Em um sistema real de hotel, poderia ser usado para buscar os dados de uma reserva já cadastrada, usando o ID dela.

Neste teste, utilizei a reserva de número 1.

Estrutura do Request

Método HTTP:

GET

URL completa:

https://restful-booker.herokuapp.com/booking/1

Headers:

Para receber a resposta em JSON, utilizei:

Accept: application/json

Body:

N/A

Como estou apenas consultando uma informação, não preciso enviar um JSON no corpo da requisição.

Estrutura do Response

Status Code esperado:

200 OK

A requisição foi realizada com sucesso e a API retornou os dados da reserva.

Payload de retorno:

Este foi o JSON que recebi no Postman:

{
    "firstname": "Jim",
    "lastname": "Wilson",
    "totalprice": 850,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2017-11-19",
        "checkout": "2018-06-02"
    },
    "additionalneeds": "Breakfast"
}


Nesse retorno podemos perceber que algumas informações são simples, como firstname, lastname e totalprice.

Também existe o campo bookingdates, que é um objeto dentro do JSON principal e possui duas outras informações: checkin e checkout.

2. POST — Criar uma reserva
Identificação e finalidade

Endpoint/Rota:

/booking

Objetivo de negócio:

Esse endpoint serve para criar uma nova reserva de hotel.

Em uma situação real, seria utilizado quando um cliente realiza uma nova reserva, enviando seus dados, o valor da reserva, as datas da hospedagem e outras informações.

Estrutura do Request

Método HTTP:

POST

URL completa:

https://restful-booker.herokuapp.com/booking

Headers:

Como estou enviando um JSON para a API, utilizei:

Content-Type: application/json

Esse header informa para a API que o conteúdo enviado está no formato JSON.

Body:

O JSON que enviei foi:

{
    "firstname": "Joao",
    "lastname": "Silva",
    "totalprice": 150,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2026-10-10",
        "checkout": "2026-10-15"
    },
    "additionalneeds": "Breakfast"
}


Nesse caso, estou enviando para a API os dados da pessoa e da reserva que quero criar.

Uma parte que achei interessante é o bookingdates. Ele é um objeto dentro do JSON principal e possui as datas de entrada e saída:

"bookingdates": {
    "checkin": "2026-10-10",
    "checkout": "2026-10-15"
}

Estrutura do Response

Status Code esperado:

200 OK

A requisição foi realizada com sucesso e a API criou uma nova reserva.

Payload de retorno:

Este foi o JSON que recebi no Postman:

{
    "bookingid": 126,
    "booking": {
        "firstname": "Joao",
        "lastname": "Silva",
        "totalprice": 150,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2026-10-10",
            "checkout": "2026-10-15"
        },
        "additionalneeds": "Breakfast"
    }
}


A informação que mais chamou minha atenção nesse retorno foi o bookingid.

Nesse caso, a API criou a reserva e retornou o ID:

126

Esse ID foi gerado pela própria API. Eu não precisei enviar o bookingid no Body da requisição.

Depois de criar a reserva, esse ID pode ser utilizado para consultar os dados dela usando o endpoint GET:

https://restful-booker.herokuapp.com/booking/126

Dessa forma, é possível relacionar as duas operações:

POST /booking
       ↓
Cria uma nova reserva
       ↓
API retorna o bookingid: 126
       ↓
GET /booking/126
       ↓
Consulta a reserva criada

3. Resumo do que foi aprendido

Com esses dois endpoints, consegui entender melhor como acontece uma comunicação básica com uma API.

No GET, envio uma requisição para consultar uma informação. Nesse caso, o ID da reserva é colocado na própria URL.

No POST, envio informações para a API dentro de um JSON, com o objetivo de criar uma nova reserva.

Também foi possível perceber que uma API pode receber e retornar objetos JSON dentro de outros objetos, como acontece com bookingdates.

Outra coisa que consegui entender foi que a API pode gerar um ID automaticamente quando uma nova informação é criada. No meu teste, a nova reserva recebeu o bookingid 126.

Esse ID pode ser usado posteriormente para consultar a reserva criada através do endpoint GET.

O fluxo que entendi com essa atividade foi:

POST /booking
       ↓
Envia os dados da nova reserva
       ↓
API cria a reserva
       ↓
API retorna o bookingid: 126
       ↓
GET /booking/126
       ↓
Consulta a reserva criada


Essa atividade me ajudou a entender melhor como um sistema envia informações para uma API e como a API devolve uma resposta. Esse conhecimento será importante para a próxima etapa, que será a criação de testes automatizados para verificar se a API está respondendo corretamente.
