# Trabalho 2 - Design de Software

Nessa trabalho foi utilizado a execução sem o docker e postgres, com banco local.
Implementamos com o loopback uma nova classe que chamos de __Informações__, e os seguintes propriedades
podem ser encontradas.

1. __Mensagem__: Contém a mensagem de um professor/servidor. (obrigatório)
2. __Responsável__: Pessoa que inseriu a informação. (obrigatório)
3. __Sala__: Se a mensagem possuir alguma informação em relação alguma sala.
4. __Turma__: Se a mensagem possuir alguma informação em relação alguma sala.
5. __Orgão__: Orgão responsável.
6. __Data__: Data da publicação.
7. __Validade__: Informa se está valida a mensagem.

Após a criação da classe foi alterado o arquivo informacao.json, sendo os principais campos alterados são __relations__ e __acls__.

As relações criadas foram: 

    "orgao": {
      "type": "embedsOne",
      "model": "Orgao",
      "foreignKey": "orgaoId",
      "required": true
    },

    "salas": {
      "type": "embedsMany",
      "model": "Sala",
      "foreignKey": "salaId",      
      "required": false
    },
    "turmas": {
      "type": "embedsMany",
      "model": "Turma",
      "foreignKey": "turmaId",
      "required": false,
      "options": {
        "validate": false
      }
    },
    "responsavel": {
      "type": "belongsTo",
      "model": "Usuario",
      "foreignKey": "usuarioId",
      "required": true
    } 

As permissões forma setadas para que todos os usuários possam ler, apenas professores/servidores podem adicionar novas informações. As permissões criadas foram:

"acls": [
{
      "principalType": "WRITE",
      "principalId": "servidor",
      "permission": "ALLOW",
      "property": ""
    },
    {
      "principalType": "READ",
      "principalId": "$everyone",
      "permission": "ALLOW",
      "property": ""
    },
    {
      "principalType": "WRITE",
      "principalId": "secretario",
      "permission": "ALLOW",
      "property": ""
    },
    {
      "principalType": "WRITE",
      "principalId": "professor",
      "permission": "ALLOW",
      "property": ""
    }
]