# Introdução
A estrutura do controlador é definida pelo objeto [CONTROLADOR](#controlador) que incluí seus dados básicos e listas de objetos associados. Para evitar referência cruzadas e problemas de navegação no grafo de objetos, adotou-se uma estratura de JSON desnormatizada. Sendo assim, todos os objetos são escritos diretamente na raiz do controlador e não internamente de forma hierarquica. Em compensação os objetos internos trazem referências para os objetos externos.


A figura abaixo apresenta dos os objetos que fazem parte da configuração de um controlador. A setas representam referências entre esses objetos.


![Controlador](/img/controlador.png)

## Controlador

É o equipamento que fica em campo (na rua), sendo responsável pelo gerenciamento e controle dos semáforos. As programações semafóricas são inseridas neste equipamento.

### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador do Controlador |
| numeroSMEE | String||N| Número SMEE do Controlador |
| numeroSMEEConjugado1 |String|N| Número SMEE do controlador conjugado 1 |
| numeroSMEEConjugado2 |String|N| Número SMEE do controlador conjugado 2 |
| numeroSMEEConjugado3 |String|N| Número SMEE do controlador conjugado 3 |
| nomeEndereco | String|N| Descrição da localização do controlador |
| dataCriacao | Data|N| Data de Criação do Controlador |
| dataAtualizacao | Data|N| Data da última atualização do controlador |
| CLC | String|N| Código de Localização do Controlador |
| aneis | vetor de [anel](#anel)|S| Lista dos anéis do controlador |
| estagios | vetor de [estagio](#estagio)|S| Lista dos estágios do controlador |
| gruposSemaforicos | vetor de [grupos semáforico](#grupo-semaforico)|S| Lista dos grupos semafóricos do controlador |
| detectores | vetor de [detector](#detector)|S| Lista dos detectores do controlador |
| transicoesProibidas | vetor de [transição proibada](#transicao-proibida)|S| Lista das transições proibidas |
| estagiosGruposSemaforicos | vetor de [estágio grupo semáforico](#estagio-grupo-semaforico)|S| Lista de estágios grupos semafóricos|
| transicoes | vetor de [transição](#transicao)|S| Lista de transições|
| verdesConflitantes | vetor de [verde conflitante](#verde-conflitante)|S| Lista de verdes conflitantes|
| tabelaEntreVerdes | vetor de [tabela entre verdes](#tabela-entre-verdes)|S| Lista de tabelas de entre verdes|
| tabelasEntreVerdesTransicoes | vetor de [tabela entre verdes transição](#tabela-entre-verdes-transicao)|S| Lista de tabelas de entre verdes transições|


### Exemplo JSON
```JSON
{
  "id": "bdf5005e-9aa3-40a4-b0de-2e38a8aef48e",
  "numeroSMEE": "123",
  "numeroSMEEConjugado1": "123",
  "numeroSMEEConjugado2": "123",
  "numeroSMEEConjugado3": "123",
  "nomeEndereco": "R. Dr. Cícero de Castro com R. Carlos Chagas",
  "dataCriacao": "12/08/2016 11:27:34",
  "dataAtualizacao": "15/08/2016 09:44:03",
  "CLC": "1.000.0001",
  "aneis": [],
  "estagios": [],
  "gruposSemaforicos": [],
  "detectores": [],
  "transicoesProibidas": [],
  "estagiosGruposSemaforicos": [],
  "verdesConflitantes": [],
  "transicoes": [],
  "tabelasEntreVerdes": [],
  "tabelasEntreVerdesTransicoes": []
}
```

## Anel

Característica que permite a um controlador operar como se fossem vários controladores independentes. Cada anel é responsável pelo controle de certo número de grupos focais e a programação semafórica que ocorre nesses grupos focais é totalmente independente da programação semafórica dos demais grupos focais do controlador, a menos do tempo de ciclo, que tem de ser igual para o controlador e todos os seus anéis.

### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador do Anel |
| idJson | String GUUID |S| Identificador do Anel para referências dentro do JSON |
| numeroSMEE | String||N| Número SMEE do Anel |
| CLA | String|N| Código de Localização do Anel |
| estagios | vetor de referência aos [estagios](#estagio)|S| Lista com as referências de estágios desse anel |
| gruposSemaforicos | vetor de referência aos [grupos Semaforicos](#grupo-semaforico)|S| Lista com as referências de grupos semafóricos desse anel |
| detectores | vetor de referência aos [detectores](#detector)|S| Lista com as referências de detectores desse anel |


### Exemplo JSON

```JSON
    {
      "id": "ffba71d1-3918-41c8-af69-f8cf36f059a4",
      "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729",
      "numeroSMEE": "123",
      "CLA": "1.000.0001.1",
      "estagios": [
        {
          "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
        },
        {
          "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
        }
      ],
      "gruposSemaforicos": [
        {
          "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
        },
        {
          "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
        }
      ],
      "detectores": [
        {
          "idJson": "b935f1a1-73fa-446f-aed9-dffc80c0f006"
        },
        {
          "idJson": "73441af8-3fc1-4276-b74a-eab268b135e9"
        }
      ]
    }
```





## Grupo Semáforico

 Conjunto de grupos focais com indicações luminosas idênticas que controlam grupos de movimentos que recebem simultaneamente o direito de passagem e que possuem as mesmas fases. Utiliza-se a notação Gn para identificar tanto nos projetos como nas programações semafóricas o grupo semafórico de número "n". Quanto aos tipos temos: grupo semafórico veicular composto de 3 fases (vermelha, amarela e verde) e grupo semafórico de pedestre composto de 2 fases (vermelha e verde).

### Especificação 

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id   | String GUUID |S| Identificador do Grupo Semáforico |
| idJson | String GUUID |S| Identificador do Grupo Semáforico para referências dentro do JSON |
| tipo | String||S| PEDESTRE ou VEICULAR |
| descricao | String||S| Descrição do Grupo Semafórico |
| faseVermelhaApagadaAmareloIntermitente | Booleano |S| Define se caso houver uma falha na fase vermelha do grupo semáforico o anel entrar em amarelo intermitente |
| tempoVerdeSeguranca | Inteiro||S| Tempo de verde de segurança do grupo semáforico |
| anel | referência ao [anel](#anel)|S| Referência ao anel que essse grupo semáforico faz parte |
| verdesConflitantesOrigem | vetor de referência de [verdes conflitantes](#verde-conflitante)|S| Lista com as referências de verdes conflitantes que tem esse grupo semáforico como origem|
| verdesConflitantesDestino | vetor de referência de [verdes conflitantes](#verde-conflitante)|S| Lista com as referências de verdes conflitantes que tem esse grupo semáforico como destino|
| estagiosGruposSemaforicos | vetor de referência de [estágio grupo semafórico](#estagio-grupo-semaforico)|S| Lista com as referências de estágios grupos semafóricos associado a esse grupo semáforico|
| transicoes | vetor de referência de [transições](#transicao)|S| Lista com as referências de transições dsse grupo semáforico|
| tabelasEntreVerdes | vetor de referência de [tabelas de entre verdes](#tabela-entre-verdes)|S| Lista com as referências de tabelas de entre verdes dsse grupo semáforico|


### Exemplo JSON

```JSON
    {
      "id": "508a9e13-3669-4d82-a948-5577d75745eb",
      "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1",
      "tipo": "PEDESTRE",
      "descricao": "Grupos semafóricos  de pedestres Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 4,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "2b9327f7-d070-45bf-9ce9-7cc1ac5c09ad"
        }
      ],
      "verdesConflitantesDestino": [

      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "0c58556f-3ac9-4dbf-9048-b234e550fda6"
        }
      ],
      "transicoes": [
        {
          "idJson": "78472e8e-71e6-473e-b942-c8a54c51974d"
        },
        {
          "idJson": "1e89b323-0ae5-4c71-81b0-b88296277dfe"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8"
        }
      ]
    }
```


## Estágio

Intervalo de tempo em que um ou mais grupos semafóricos recebem simultaneamente o direito de passagem. O estágio compreende o tempo de verde e o entreverdes que o segue.


### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador do Estágio |
| idJson | String GUUID |S| Identificador do Estágio para referências dentro do JSON |
| tempoMaximoPermanencia | Inteiro||S| O tempo máximo que o estágio pode ter direito de passagem |
| tempoMaximoPermanenciaAtivado | Booleano||S| Define se o tempo máximo de permanencia será monitorado |
| demandaPrioritaria | Booleano||S| Define se o estágio é de demanda prioritária |
| anel | referência ao [anel](#anel)|S| Referência ao anel que essse estágio faz parte |
| origemDeTransicoesProibidas | vetor de referência das [transições proibidas](#transicao-proibida)|S| Lista com as referências de transições proibidas que tem esse estágio como origem|
| destinoDeTransicoesProibidas | vetor de referência das [transições proibidas](#transicao-proibida)|S| Lista com as referências de transições proibidas que tem esse estágio como destino|
| alternativaDeTransicoesProibidas | vetor de referência das [transições proibidas](#transicao-proibida)|S| Lista com as referências de transições proibidas que tem esse estágio como destino alternativa|
| gruposSemaforicos | vetor de referência de [grupos semáforicos](#grupo-semafórico)|S| Lista com as referências de grupos semáforicos que estão associados a esse estágio|


### Exemplo JSON

```JSON
    {
      "id": "6ba39589-fdc9-421d-a743-7d82d64ba013",
      "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "origemDeTransicoesProibidas": [
      ],
      "destinoDeTransicoesProibidas": [
        {
          "idJson": "ac8c11e2-4d05-4624-b199-ddac68f507a1"
        }
      ],
      "alternativaDeTransicoesProibidas": [
        {
          "idJson": "b395227a-ec5d-4443-9181-f71072cccfe1"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "24b112e6-c89f-41ce-b429-19f282a84aa3"
        }
      ]
    }
```

## Detector
Dispositivo de atuação acoplado ao controlador podendo ser:

1. Detector Veicular
    - Sensor destinado a registrar a presença ou passagem de veículos.
2. Botoeira 
    - Dispositivo dotado de um botão que, ao ser acionado, envia um sinal ao controlador solicitando a implementação de um estágio dispensável.

### Especificação


| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id   | String GUUID |S| Identificador do Detector |
| idJson | String GUUID |S| Identificador do Detector para referências dentro do JSON |
| tipo | String||S| PEDESTRE ou VEICULAR |
| monitorado | Booleano |S| Define se o detector será monitorado |
| anel | referência ao [anel](#anel)|S| Referência ao anel que essse detector faz parte |
| estagio | referência ao [estágio](#estagio)|S| Referência ao estágio que essse detector faz parte |

TODO: Incluir campos de monitoramento


### Exemplo JSON

```JSON
    {
      "id": "774b6233-9d7b-41e6-9c5a-799bd479f39f",
      "idJson": "00cbf727-94d8-4e8b-a4af-b419c107c6cd",
      "tipo": "VEICULAR",
      "monitorado": true,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "estagio": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      }
    }
```


## Transição
Representa a transição entre o estágio que está perdendo o direito de passagem e o estágio que irá ganhar o direito de passagem.

### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador da Transição |
| idJson | String GUUID |S| Identificador da Transição para referências dentro do JSON |
| origem | referência a [estágio](#estagio)|S| Referência ao estágio de origem |
| destino | referência a [estágio](#estagio)|S| Referência ao estágio de destino |
| tabelaEntreVerdesTransicoes | vetor de referência das [tabela de entre verdes transição proibidas](#tabela-entre-verdes-transicao)|S| Lista com as referências de tabelas de entre verdes transições|
| grupoSemaforico | referência a [grupo semáforico](#grupo-semaforico)|S| Referência ao grupo semafórico |

### Exemplo JSON

```JSON
    {
      "id": "091e5195-98cf-4644-be10-417197055847",
      "idJson": "63b8c923-1317-45c8-b93c-fd67541dd554",
      "origem": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "destino": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "38ffe4d7-eff1-48e3-8b27-5b39b5d9141c"
        }
      ],
      "grupoSemaforico": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      }
    }
```


## Transição Proibida
Representa a proibição de transição entre dois estágios.
### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador da Transição Proibida |
| idJson | String GUUID |S| Identificador da Transição Proibida para referências dentro do JSON |
| origem | referência a [estágio](#estagio)|S| Referência ao estágio de origem |
| destino | referência a [estágio](#estagio)|S| Referência ao estágio de destino |
| alternativo | referência a [estágio](#estagio)|S| Referência ao estágio alternativo |


### Exemplo JSON

```JSON
    {
      "id": "40253953-a75e-4c2b-8574-c1a2f1d10bc2",
      "idJson": "ac8c11e2-4d05-4624-b199-ddac68f507a1",
      "origem": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "destino": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "alternativo": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      }
    }
```

## Tabela Entre Verdes
Agrupamento de Tabela Entre Verdes Transição.
### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id   | String GUUID |S| Identificador da Tabela de Entre Verdes |
| idJson | String GUUID |S| Identificador da Tabela de Entre Verdes para referências dentro do JSON |
| descricao | String||S| Descrição da Tabela de Entre Verdes |
| grupoSemaforico | referência a [grupo semáforico](#grupo-semaforico)|S| Referência ao grupo semafórico |
| tabelaEntreVerdesTransicoes | vetor de referência de [tabelas de entre verdes transições](#tabela-entre-verdes-transicao)|S| Lista com as referências de tabelas de entre verdes transições dessa tabela de entre verdes|


### Exemplo JSON

```JSON
    {
      "id": "943934ba-a8b5-4014-8795-84240f21b75b",
      "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8",
      "descricao": "PADRÃO",
      "grupoSemaforico": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9cc359ee-a47e-44f9-8098-750c114f8d32"
        },
        {
          "idJson": "18a6bd08-9d8c-4fc1-b089-9aa8c390bfe1"
        }
      ]
    }
```


## Tabela Entre Verdes Transição
Intervalo de tempo compreendido entre o final do verde de um estágio e o início do verde do estágio subsequente inserido com o propósito de evitar acidentes entre os usuários que estão perdendo seu direito de passagem e aqueles que vão passar a ganhá-lo. No caso de grupos focais veiculares, compõe-se do período de amarelo seguido do período de vermelho geral. No caso de grupos focais de pedestres consiste do período de vermelho intermitente de pedestre seguido do período de vermelho geral.



### Especificação


| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador da Tabela de Entre Verdes Transições |
| idJson | String GUUID |S| Identificador da Tabela de Entre Verdes Transições para referências dentro do JSON |
| tempoAmarelo | Inteiro||N| Tempo de amarelo do entre verdes |
| tempoVermelhoIntermitente | Inteiro||N| Tempo de vermelho intermitente |
| tempoVermelhoLimpeza | Inteiro||S| Tempo de vermelho de limpeza do entre verdes |
| tempoAtrasoGrupo | Inteiro||S| Tempo de atraso de grupo |
| tabelaEntreVerdes | referência a [tabela de entre verdes](#tabela-entre-verdes)|S| Referência a tabela de entre verdes |
| transicao | referência a [transição](#transicao)|S| Referência a transição |

### Exemplo JSON

```JSON
    {
      "id": "de33f221-f7f0-4118-90d4-49d3dd21ba3a",
      "idJson": "9c912de8-9ca5-411f-af6a-768c172da0a3",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "3a0bb61c-492f-4727-ac7e-785d270f4b2f"
      },
      "transicao": {
        "idJson": "91882aea-8354-4526-955f-69d3c999ae8d"
      }
    }
```


## Estágio Grupo Semáforico
Objeto que representa a associação entre grupos semafóricos x estágios.

### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador do Estágio Grupo Semafórico |
| idJson | String GUUID |S| Identificador do Estágio Grupo Semafórico para referências dentro do JSON |
| ativo | Booleano||S| Define se um grupo semáforico estará ativo durante o estágio|
| estagio | referência a [estágio](#estagio)|S| Referência ao estágio |
| grupoSemaforico | referência a [grupo semáforico](#grupo-semaforico)|S| Referência ao grupo semafórico |

todo: revisar o campo ativo

### Exemplo JSON

```JSON
    {
      "id": "eee3b305-7e8e-4c1e-bd46-8f83f462b506",
      "idJson": "4530082c-744e-47ee-b5c2-a0e042d7f0d7",
      "ativo": false,
      "estagio": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "grupoSemaforico": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      }
    }
```



## Verde Conflitante
Representa um conflito entre dois grupos semafóricos que não têm permissão de movimento simultâneo.

### Especificação

| Campo| Tipo | Obrigatorio| Descrição |
| -----|----- | ---------- | --------- |
| id | String GUUID |S| Identificador do Verde Conflitante |
| idJson | String GUUID |S| Identificador do Verde Conflitante para referências dentro do JSON |
| origem | referência a um [grupo semáforico](#grupo-semaforico)|S| Referência ao grupo semáforico de origem |
| destino | referência a um [grupo semáforico](#grupo-semaforico)|S| Referência ao grupo semáforico de destino |

### Exemplo JSON

```JSON
    {
      "id": "6bd31d57-933c-4113-aed4-583b692568aa",
      "idJson": "2b9327f7-d070-45bf-9ce9-7cc1ac5c09ad",
      "origem": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      },
      "destino": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      }
    }
```





## Exemplo Completo


```JSON
{
  "id": "bdf5005e-9aa3-40a4-b0de-2e38a8aef48e",
  "numeroSMEE": "123",
  "numeroSMEEConjugado1": "123",
  "numeroSMEEConjugado2": "123",
  "numeroSMEEConjugado3": "123",
  "nomeEndereco": "R. Dr. Cícero de Castro com R. Carlos Chagas",
  "dataCriacao": "12/08/2016 11:27:34",
  "dataAtualizacao": "15/08/2016 09:44:03",
  "CLC": "1.000.0001",
  "aneis": [
    {
      "id": "4eec5335-0e72-4b71-84f4-3b6a570c9114",
      "numeroSMEE": "123",
      "ativo": true,
      "CLA": "1.000.0001.3",
      "estagios": [
        {
          "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
        },
        {
          "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
        },
        {
          "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
        }
      ],
      "gruposSemaforicos": [
        {
          "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
        },
        {
          "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
        },
        {
          "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
        }
      ],
      "detectores": [

      ],
    },
    {
      "id": "ffba71d1-3918-41c8-af69-f8cf36f059a4",
      "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729",
      "numeroSMEE": "123",
      "CLA": "1.000.0001.1",
      "estagios": [
        {
          "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
        },
        {
          "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
        },
        {
          "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
        },
        {
          "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
        }
      ],
      "gruposSemaforicos": [
        {
          "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
        },
        {
          "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
        },
        {
          "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
        },
        {
          "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
        }
      ],
      "detectores": [
        {
          "idJson": "b935f1a1-73fa-446f-aed9-dffc80c0f006"
        },
        {
          "idJson": "73441af8-3fc1-4276-b74a-eab268b135e9"
        },
        {
          "idJson": "00cbf727-94d8-4e8b-a4af-b419c107c6cd"
        },
        {
          "idJson": "f3a48209-a29c-4c9a-a2c6-ef87949e9b39"
        }
      ]
    }
  ],
  "estagios": [
    {
      "id": "6e3a509d-c942-40cb-8d70-d2f1c73c087b",
      "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "fb777bef-8034-4f44-87c7-864de478fc2a"
      },
      "origemDeTransicoesProibidas": [
      ],
      "destinoDeTransicoesProibidas": [
      ],
      "alternativaDeTransicoesProibidas": [
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "918ca0c6-3776-4b18-93ff-913c690f7479"
        }
      ]
    },
    {
      "id": "96da6a35-5231-4072-b17b-833b230cff05",
      "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "origemDeTransicoesProibidas": [
      ],
      "destinoDeTransicoesProibidas": [
      ],
      "alternativaDeTransicoesProibidas": [
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "42cc21a7-42d6-4523-a14f-7655d939e896"
        }
      ]
    },
    {
      "id": "b7a0c26d-8ddb-4341-ba1d-338a5cf2c151",
      "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "origemDeTransicoesProibidas": [
      ],
      "destinoDeTransicoesProibidas": [
      ],
      "alternativaDeTransicoesProibidas": [
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "0c58556f-3ac9-4dbf-9048-b234e550fda6"
        }
      ]
    },
    {
      "id": "6ba39589-fdc9-421d-a743-7d82d64ba013",
      "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "origemDeTransicoesProibidas": [
      ],
      "destinoDeTransicoesProibidas": [
        {
          "idJson": "ac8c11e2-4d05-4624-b199-ddac68f507a1"
        }
      ],
      "alternativaDeTransicoesProibidas": [
        {
          "idJson": "b395227a-ec5d-4443-9181-f71072cccfe1"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "24b112e6-c89f-41ce-b429-19f282a84aa3"
        }
      ]
    },
    {
      "id": "4804f66d-1ade-459e-bcae-211065d7a8fc",
      "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0",
      "tempoMaximoPermanencia": 60,
      "tempoMaximoPermanenciaAtivado": true,
      "demandaPrioritaria": false,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "origemDeTransicoesProibidas": [
        {
          "idJson": "b395227a-ec5d-4443-9181-f71072cccfe1"
        },
        {
          "idJson": "ac8c11e2-4d05-4624-b199-ddac68f507a1"
        }
      ],
      "destinoDeTransicoesProibidas": [

      ],
      "alternativaDeTransicoesProibidas": [

      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "a1ff5d61-5fa3-4103-9958-1a0f34fcfcc1"
        }
      ]
    }
  ],
  "gruposSemaforicos": [
    {
      "id": "508a9e13-3669-4d82-a948-5577d75745eb",
      "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1",
      "tipo": "PEDESTRE",
      "descricao": "Grupos semafóricos  de pedestres Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 4,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "2b9327f7-d070-45bf-9ce9-7cc1ac5c09ad"
        }
      ],
      "verdesConflitantesDestino": [

      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "0c58556f-3ac9-4dbf-9048-b234e550fda6"
        }
      ],
      "transicoes": [
        {
          "idJson": "78472e8e-71e6-473e-b942-c8a54c51974d"
        },
        {
          "idJson": "1e89b323-0ae5-4c71-81b0-b88296277dfe"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8"
        }
      ]
    },
    {
      "id": "be1f8f57-1623-4069-b942-a62483a26578",
      "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos  de pedestres Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "fb777bef-8034-4f44-87c7-864de478fc2a"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "04020879-fbec-4747-90d1-c4a034cc707f"
        }
      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "fba2557f-32a6-4176-a516-63901c8cb3fd"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "918ca0c6-3776-4b18-93ff-913c690f7479"
        }
      ],
      "transicoes": [
        {
          "idJson": "eb51dfdd-dc60-4842-8e5e-d6dab1c32508"
        },
        {
          "idJson": "91882aea-8354-4526-955f-69d3c999ae8d"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "3a0bb61c-492f-4727-ac7e-785d270f4b2f"
        }
      ]
    },
    {
      "id": "a4745500-c239-463c-95ed-bfb026598285",
      "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de",
      "tipo": "PEDESTRE",
      "descricao": "Grupos semafóricos  de pedestres da França Campos",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 4,
      "anel": {
        "idJson": "fb777bef-8034-4f44-87c7-864de478fc2a"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "fba2557f-32a6-4176-a516-63901c8cb3fd"
        }
      ],
      "verdesConflitantesDestino": [

      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "f6a8bfb6-e108-473f-a804-ef9b09b79102"
        }
      ],
      "transicoes": [
        {
          "idJson": "9a0cbff0-7a77-43e3-968b-c8aaa9f62907"
        },
        {
          "idJson": "0bead9e0-ebac-42e6-b2db-ffd751c286f7"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "31f8a81c-afd8-4e13-8d29-34ecd0376585"
        }
      ]
    },
    {
      "id": "afa80501-616c-4bb7-a273-0cfbcb2c3808",
      "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos  veiculares Gabriel de Andrade",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "0b8481c6-9e64-472b-8cb5-599ba578980e"
        }
      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "2b9327f7-d070-45bf-9ce9-7cc1ac5c09ad"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "42cc21a7-42d6-4523-a14f-7655d939e896"
        }
      ],
      "transicoes": [
        {
          "idJson": "5492976d-2504-4d95-97a6-3f191e86d7cc"
        },
        {
          "idJson": "bcf0ac62-0a40-4889-a0f3-bf1664e8f7d7"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "ded06a03-d592-4181-a859-5aad31e0417f"
        }
      ]
    },
    {
      "id": "7e92c0b2-a234-4298-8033-cd8af873c39a",
      "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos  veiculares Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "verdesConflitantesOrigem": [

      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "7df0dd5f-684d-4160-ad04-e9122bce1f66"
        },
        {
          "idJson": "172cf9d7-bb6f-4305-95ea-43189996e4e0"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "cdbddff1-ccaf-4188-9e45-5360236a4a68"
        }
      ],
      "transicoes": [
        {
          "idJson": "8ad5d2f9-28d9-4df6-a161-d494cbe2ee59"
        },
        {
          "idJson": "4322e973-d657-4c8f-91f8-2c92226f4530"
        },
        {
          "idJson": "2baa63af-3b8c-4eba-96f8-ef827659544e"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "d10b5fb2-017e-4ba4-9aa6-42f99074bf28"
        }
      ]
    },
    {
      "id": "8683ed5e-0bc4-4cfb-9656-8299b86b8469",
      "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos  veiculares Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "7cf6c92c-6831-49b0-a366-ac44cfa65d77"
      },
      "verdesConflitantesOrigem": [

      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "0b8481c6-9e64-472b-8cb5-599ba578980e"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "74f23b48-a550-49fc-9bd0-ec9d6a949277"
        }
      ],
      "transicoes": [
        {
          "idJson": "63b8c923-1317-45c8-b93c-fd67541dd554"
        },
        {
          "idJson": "9f8ac533-48ed-4b61-88e2-0dcfbc7f41eb"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "0e9acd45-ef9c-4f13-a384-fdd8c1ff5895"
        }
      ]
    },
    {
      "id": "eb2d3e92-75b3-4ed5-a408-769f573ae752",
      "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos veiculares Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "fb777bef-8034-4f44-87c7-864de478fc2a"
      },
      "verdesConflitantesOrigem": [

      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "04020879-fbec-4747-90d1-c4a034cc707f"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "4530082c-744e-47ee-b5c2-a0e042d7f0d7"
        }
      ],
      "transicoes": [
        {
          "idJson": "c880480c-7edb-43a4-b22c-f450f4664cf5"
        },
        {
          "idJson": "b0cb13d1-f984-47b3-b0df-6cec3540cb34"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "e029f3a5-4b4f-4221-8db2-0146ac6238ac"
        }
      ]
    },
    {
      "id": "8ecc49a7-6db2-4b4c-8a32-dc2f4a6e39c5",
      "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b",
      "tipo": "VEICULAR",
      "descricao": "Grupos semafóricos veiculares Carlos Chagas",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 10,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "7df0dd5f-684d-4160-ad04-e9122bce1f66"
        }
      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "29d44b62-cc55-46ac-b943-c7d2fca5234b"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "a1ff5d61-5fa3-4103-9958-1a0f34fcfcc1"
        }
      ],
      "transicoes": [
        {
          "idJson": "dd76570b-b68f-4e75-8958-e51c48d405ba"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "0c4c07b3-a76b-433e-a607-e8a73c3fe112"
        }
      ]
    },
    {
      "id": "28f5efe6-4a23-438c-8358-b0ca4b72c1b2",
      "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10",
      "tipo": "PEDESTRE",
      "descricao": "Grupos semafóricos de pedestres Cícero de castro",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 4,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "29d44b62-cc55-46ac-b943-c7d2fca5234b"
        }
      ],
      "verdesConflitantesDestino": [
        {
          "idJson": "049b26a3-dd09-4631-9846-2c885f5cacc0"
        }
      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "24b112e6-c89f-41ce-b429-19f282a84aa3"
        }
      ],
      "transicoes": [
        {
          "idJson": "54c491d2-d57c-4848-a3b1-c91ee586c644"
        },
        {
          "idJson": "f91c7398-376b-4688-9260-977ebda02857"
        },
        {
          "idJson": "257cb278-122a-4452-aaf2-af37417b7a46"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "6c002dfc-3c25-4ba9-99f4-c80139e8897d"
        }
      ]
    },
    {
      "id": "a5a2c4b5-3b40-4d60-ae22-0b603d90e533",
      "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413",
      "tipo": "PEDESTRE",
      "descricao": "Grupos semafóricos de pedestres Carlos Chagas",
      "faseVermelhaApagadaAmareloIntermitente": false,
      "tempoVerdeSeguranca": 4,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "verdesConflitantesOrigem": [
        {
          "idJson": "049b26a3-dd09-4631-9846-2c885f5cacc0"
        },
        {
          "idJson": "172cf9d7-bb6f-4305-95ea-43189996e4e0"
        }
      ],
      "verdesConflitantesDestino": [

      ],
      "estagiosGruposSemaforicos": [
        {
          "idJson": "335e071f-e1a4-45b9-971f-e64109377f89"
        }
      ],
      "transicoes": [
        {
          "idJson": "a4058516-6bdd-497a-934a-8db37275187b"
        },
        {
          "idJson": "09fe244e-74d5-463f-97e1-11e1c3e05d40"
        },
        {
          "idJson": "a296531e-e704-4726-a07f-88b5e44cf195"
        }
      ],
      "tabelasEntreVerdes": [
        {
          "idJson": "1d34871b-3ac9-4e18-b11a-cf4cd24e17e2"
        }
      ]
    }
  ],
  "detectores": [
    {
      "id": "774b6233-9d7b-41e6-9c5a-799bd479f39f",
      "idJson": "00cbf727-94d8-4e8b-a4af-b419c107c6cd",
      "tipo": "VEICULAR",
      "monitorado": true,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "estagio": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      }
    },
    {
      "id": "6a980321-4be7-4b43-83a8-7effb89b6baf",
      "idJson": "73441af8-3fc1-4276-b74a-eab268b135e9",
      "tipo": "PEDESTRE",
      "monitorado": true,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "estagio": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      }
    },
    {
      "id": "f0e6ad7a-f34e-4b92-a27b-fedafad5fc0b",
      "idJson": "f3a48209-a29c-4c9a-a2c6-ef87949e9b39",
      "tipo": "PEDESTRE",
      "monitorado": true,
      "tempoAusenciaDeteccaoMinima": 0,
      "tempoAusenciaDeteccaoMaxima": 0,
      "tempoDeteccaoPermanenteMinima": 0,
      "tempoDeteccaoPermanenteMaxima": 0,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "estagio": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      }
    },
    {
      "id": "29267bfd-a488-4453-8d11-7c14d00c9a0d",
      "idJson": "b935f1a1-73fa-446f-aed9-dffc80c0f006",
      "tipo": "VEICULAR",
      "posicao": 2,
      "monitorado": true,
      "anel": {
        "idJson": "eeb76ef2-54f6-4eb8-b7e5-08ac7edad729"
      },
      "estagio": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      }
    }
  ],
  "transicoesProibidas": [
    {
      "id": "40253953-a75e-4c2b-8574-c1a2f1d10bc2",
      "idJson": "ac8c11e2-4d05-4624-b199-ddac68f507a1",
      "origem": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "destino": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "alternativo": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      }
    },
    {
      "id": "18924afa-e8df-4426-b0f0-4163f3c4bdaa",
      "idJson": "b395227a-ec5d-4443-9181-f71072cccfe1",
      "origem": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "destino": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "alternativo": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      }
    }
  ],
  "estagiosGruposSemaforicos": [
    {
      "id": "eee3b305-7e8e-4c1e-bd46-8f83f462b506",
      "idJson": "4530082c-744e-47ee-b5c2-a0e042d7f0d7",
      "ativo": false,
      "estagio": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "grupoSemaforico": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      }
    },
    {
      "id": "ac720b95-a323-4253-8f77-dfda70e47d8c",
      "idJson": "74f23b48-a550-49fc-9bd0-ec9d6a949277",
      "ativo": false,
      "estagio": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "grupoSemaforico": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      }
    },
    {
      "id": "768afa1e-2006-46bc-b03a-d6764f1e83e3",
      "idJson": "335e071f-e1a4-45b9-971f-e64109377f89",
      "ativo": false,
      "estagio": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "grupoSemaforico": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      }
    },
    {
      "id": "19227489-fd78-49bd-b415-f6e522622ed3",
      "idJson": "42cc21a7-42d6-4523-a14f-7655d939e896",
      "ativo": false,
      "estagio": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "grupoSemaforico": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      }
    },
    {
      "id": "db3d00be-1279-4d97-b200-c90e5a9d9f62",
      "idJson": "a1ff5d61-5fa3-4103-9958-1a0f34fcfcc1",
      "ativo": false,
      "estagio": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "grupoSemaforico": {
        "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
      }
    },
    {
      "id": "2ad6c64c-4306-4326-897c-6ffd600695cd",
      "idJson": "0c58556f-3ac9-4dbf-9048-b234e550fda6",
      "ativo": false,
      "estagio": {
        "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e"
      },
      "grupoSemaforico": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      }
    },
    {
      "id": "94f85c95-4783-4cac-b18b-5f70aea9de36",
      "idJson": "24b112e6-c89f-41ce-b429-19f282a84aa3",
      "ativo": false,
      "estagio": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "grupoSemaforico": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      }
    },
    {
      "id": "de4ce0ac-3f14-43ff-a248-7487aef5b073",
      "idJson": "918ca0c6-3776-4b18-93ff-913c690f7479",
      "ativo": false,
      "estagio": {
        "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
      },
      "grupoSemaforico": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      }
    },
    {
      "id": "f92c039d-ffed-4bc4-9d27-49d3bdc2792b",
      "idJson": "f6a8bfb6-e108-473f-a804-ef9b09b79102",
      "ativo": false,
      "estagio": {
        "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
      },
      "grupoSemaforico": {
        "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
      }
    },
    {
      "id": "4ce9da27-5b81-494c-966e-8427413c4ba3",
      "idJson": "cdbddff1-ccaf-4188-9e45-5360236a4a68",
      "ativo": false,
      "estagio": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "grupoSemaforico": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    }
  ],
  "verdesConflitantes": [
    {
      "id": "6bd31d57-933c-4113-aed4-583b692568aa",
      "idJson": "2b9327f7-d070-45bf-9ce9-7cc1ac5c09ad",
      "origem": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      },
      "destino": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      }
    },
    {
      "id": "983ee6bd-e77e-4bd5-9ae2-37bc48e1c44e",
      "idJson": "04020879-fbec-4747-90d1-c4a034cc707f",
      "origem": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      },
      "destino": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      }
    },
    {
      "id": "eb6446a9-613f-411c-a34d-1bef62287551",
      "idJson": "29d44b62-cc55-46ac-b943-c7d2fca5234b",
      "origem": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      },
      "destino": {
        "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
      }
    },
    {
      "id": "922c929f-6528-4f4b-b754-1c3baa3644b6",
      "idJson": "172cf9d7-bb6f-4305-95ea-43189996e4e0",
      "origem": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      },
      "destino": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    },
    {
      "id": "90fddcd5-24f3-43d1-9902-7b29b99f93e2",
      "idJson": "0b8481c6-9e64-472b-8cb5-599ba578980e",
      "origem": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      },
      "destino": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      }
    },
    {
      "id": "252fbf11-fea0-4826-9fe1-f59767b32a0c",
      "idJson": "7df0dd5f-684d-4160-ad04-e9122bce1f66",
      "origem": {
        "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
      },
      "destino": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    },
    {
      "id": "5db43c07-ca8b-4fd5-ad65-14d7ddb5a578",
      "idJson": "fba2557f-32a6-4176-a516-63901c8cb3fd",
      "origem": {
        "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
      },
      "destino": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      }
    },
    {
      "id": "24a92566-1fc1-45ed-acc7-8ec2a4ecb149",
      "idJson": "049b26a3-dd09-4631-9846-2c885f5cacc0",
      "origem": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      },
      "destino": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      }
    }
  ],
  "transicoes": [
    {
      "id": "091e5195-98cf-4644-be10-417197055847",
      "idJson": "63b8c923-1317-45c8-b93c-fd67541dd554",
      "origem": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "destino": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "38ffe4d7-eff1-48e3-8b27-5b39b5d9141c"
        }
      ],
      "grupoSemaforico": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      }
    },
    {
      "id": "11d00fc1-83a4-46c8-961e-4dc55d9d1b64",
      "idJson": "9f8ac533-48ed-4b61-88e2-0dcfbc7f41eb",
      "origem": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "destino": {
        "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "c383e022-7dbc-4423-bd71-2a5f2e1ce765"
        }
      ],
      "grupoSemaforico": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      }
    },
    {
      "id": "9a70bfd2-5ede-4074-8f05-cfbd73cbff76",
      "idJson": "eb51dfdd-dc60-4842-8e5e-d6dab1c32508",
      "origem": {
        "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
      },
      "destino": {
        "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "f5fc0766-db98-4c84-8f45-6e3c370fc81f"
        }
      ],
      "grupoSemaforico": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      }
    },
    {
      "id": "c52d371b-b346-4cde-9be6-3e831fc80407",
      "idJson": "f91c7398-376b-4688-9260-977ebda02857",
      "origem": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "destino": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "e33d95a7-4ac7-4be1-8531-35ec08afaa4b"
        }
      ],
      "grupoSemaforico": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      }
    },
    {
      "id": "cd61a85c-43ee-4b50-8ade-74a8a5804169",
      "idJson": "bcf0ac62-0a40-4889-a0f3-bf1664e8f7d7",
      "origem": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "destino": {
        "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "640c6923-6f57-4a2f-8110-f5665b6466ac"
        }
      ],
      "grupoSemaforico": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      }
    },
    {
      "id": "23916208-1182-4649-931d-11b40888c153",
      "idJson": "a4058516-6bdd-497a-934a-8db37275187b",
      "origem": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "destino": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "d69ed23c-ecca-4840-bb57-5a9c8e603ece"
        }
      ],
      "grupoSemaforico": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      }
    },
    {
      "id": "ea938d22-8ecc-4c3f-86fe-0b299dc2fdeb",
      "idJson": "a296531e-e704-4726-a07f-88b5e44cf195",
      "origem": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "destino": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "7651cfbf-522b-4c5c-9b07-d4af29087b90"
        }
      ],
      "grupoSemaforico": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      }
    },
    {
      "id": "951eaeda-896e-4e4d-8818-f6e26cae2760",
      "idJson": "0bead9e0-ebac-42e6-b2db-ffd751c286f7",
      "origem": {
        "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
      },
      "destino": {
        "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "716c177e-156d-409e-a659-cf4ee3ad9249"
        }
      ],
      "grupoSemaforico": {
        "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
      }
    },
    {
      "id": "b548b31e-5107-4f73-9c16-b8a89c14a3f6",
      "idJson": "54c491d2-d57c-4848-a3b1-c91ee586c644",
      "origem": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "destino": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "0377fc38-593b-4bb1-b598-d917ffcf5e55"
        }
      ],
      "grupoSemaforico": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      }
    },
    {
      "id": "467744ee-ebf9-4655-bc37-8ddbf76024cb",
      "idJson": "8ad5d2f9-28d9-4df6-a161-d494cbe2ee59",
      "origem": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "destino": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "a55a24d6-c437-4818-9083-4d596c4cdb92"
        }
      ],
      "grupoSemaforico": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    },
    {
      "id": "bf50f4b2-3296-404b-9ef6-6a5b63b269da",
      "idJson": "4322e973-d657-4c8f-91f8-2c92226f4530",
      "origem": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "destino": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "4880b0db-dbea-40ff-aef7-8f93df6035e9"
        }
      ],
      "grupoSemaforico": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    },
    {
      "id": "93e87909-3582-4d58-8d37-7615c7fe97c4",
      "idJson": "c880480c-7edb-43a4-b22c-f450f4664cf5",
      "origem": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "destino": {
        "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "8f6bf63f-3ed0-4368-bb5a-8b6890ba3bcd"
        }
      ],
      "grupoSemaforico": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      }
    },
    {
      "id": "aebf7ce1-6690-4762-a5fd-21fe443f9c04",
      "idJson": "b0cb13d1-f984-47b3-b0df-6cec3540cb34",
      "origem": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "destino": {
        "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "792982f9-fd9c-430f-a04d-69e4c656701c"
        }
      ],
      "grupoSemaforico": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      }
    },
    {
      "id": "cf909be3-7cd0-4029-9f07-c5d2a4ad1ce4",
      "idJson": "257cb278-122a-4452-aaf2-af37417b7a46",
      "origem": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "destino": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "3ec67e12-6551-4b73-9fe7-7cdf03764def"
        }
      ],
      "grupoSemaforico": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      }
    },
    {
      "id": "b675a61b-a07c-4566-8223-467888494709",
      "idJson": "91882aea-8354-4526-955f-69d3c999ae8d",
      "origem": {
        "idJson": "175f92b5-2b94-4657-bfc8-2099c8b3ab3e"
      },
      "destino": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9c912de8-9ca5-411f-af6a-768c172da0a3"
        }
      ],
      "grupoSemaforico": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      }
    },
    {
      "id": "dec03f83-936c-4a8d-88b7-1389fe5ab584",
      "idJson": "dd76570b-b68f-4e75-8958-e51c48d405ba",
      "origem": {
        "idJson": "b6a7553a-bb45-4d49-9cf3-9979f6ffb9a0"
      },
      "destino": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "5bbcf0e0-e61e-4291-9f6c-cf1bfbf915a7"
        }
      ],
      "grupoSemaforico": {
        "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
      }
    },
    {
      "id": "dfcc0fd8-6fb6-49f9-975a-aa3e4728cea6",
      "idJson": "1e89b323-0ae5-4c71-81b0-b88296277dfe",
      "origem": {
        "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e"
      },
      "destino": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9cc359ee-a47e-44f9-8098-750c114f8d32"
        }
      ],
      "grupoSemaforico": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      }
    },
    {
      "id": "dba4a742-d05f-4c5d-b0b9-2ae225022dc3",
      "idJson": "2baa63af-3b8c-4eba-96f8-ef827659544e",
      "origem": {
        "idJson": "810b2ab2-7559-4e86-b3ec-b53e137354b2"
      },
      "destino": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "cec18b18-5fa7-4b38-99d4-8ac3f6ebfda4"
        }
      ],
      "grupoSemaforico": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      }
    },
    {
      "id": "3f83a327-d4e4-4745-a1c9-2a1aa2e1ed4b",
      "idJson": "09fe244e-74d5-463f-97e1-11e1c3e05d40",
      "origem": {
        "idJson": "849ed858-d3c5-48a5-97fc-32f8ce4cc14e"
      },
      "destino": {
        "idJson": "0aa7c531-f3bf-4c5e-98b9-75fb02a9b44b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "aca75afc-b144-46da-98f4-44ab1b703e11"
        }
      ],
      "grupoSemaforico": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      }
    },
    {
      "id": "22053bcf-23f4-4f23-83e7-7609cc80022d",
      "idJson": "78472e8e-71e6-473e-b942-c8a54c51974d",
      "origem": {
        "idJson": "b31ef721-6c59-4c5c-9556-27470ed33c4e"
      },
      "destino": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "18a6bd08-9d8c-4fc1-b089-9aa8c390bfe1"
        }
      ],
      "grupoSemaforico": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      }
    },
    {
      "id": "40b72f7a-3dbd-4838-9e04-6c6e6e5488c3",
      "idJson": "5492976d-2504-4d95-97a6-3f191e86d7cc",
      "origem": {
        "idJson": "0ec953fb-11fd-4921-b24e-f8cd5b81d21b"
      },
      "destino": {
        "idJson": "7c24d0b4-dbab-452f-abfc-65291792828d"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "35744209-94db-4ae8-aa47-f07b31b908e5"
        }
      ],
      "grupoSemaforico": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      }
    },
    {
      "id": "0ed3addf-c3d0-4b60-8c75-61b376e5879c",
      "idJson": "9a0cbff0-7a77-43e3-968b-c8aaa9f62907",
      "origem": {
        "idJson": "acc473a8-0cfb-4537-821e-3d767e52b7df"
      },
      "destino": {
        "idJson": "090768c2-4e9f-4247-9c64-d73425c31a29"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9c7d2c3e-42b7-4150-8a75-5ca307bf5677"
        }
      ],
      "grupoSemaforico": {
        "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
      }
    }
  ],
  "tabelasEntreVerdes": [
    {
      "id": "943934ba-a8b5-4014-8795-84240f21b75b",
      "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "41f04b7e-742f-4722-8e73-689d9c0ef6f1"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9cc359ee-a47e-44f9-8098-750c114f8d32"
        },
        {
          "idJson": "18a6bd08-9d8c-4fc1-b089-9aa8c390bfe1"
        }
      ]
    },
    {
      "id": "72a3f15c-1918-45f4-ba0c-722110b5f5ec",
      "idJson": "d10b5fb2-017e-4ba4-9aa6-42f99074bf28",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "6cb0ee2a-e095-4175-b488-540ed4cb4f54"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "a55a24d6-c437-4818-9083-4d596c4cdb92"
        },
        {
          "idJson": "cec18b18-5fa7-4b38-99d4-8ac3f6ebfda4"
        },
        {
          "idJson": "4880b0db-dbea-40ff-aef7-8f93df6035e9"
        }
      ]
    },
    {
      "id": "d0f64123-a3bc-4ad7-8d4f-4eba12bde9c2",
      "idJson": "e029f3a5-4b4f-4221-8db2-0146ac6238ac",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "873c4c1b-b518-4919-a937-3812f9fe9017"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "792982f9-fd9c-430f-a04d-69e4c656701c"
        },
        {
          "idJson": "8f6bf63f-3ed0-4368-bb5a-8b6890ba3bcd"
        }
      ]
    },
    {
      "id": "718b3482-9442-4422-8f0f-4f1c9278b2ba",
      "idJson": "31f8a81c-afd8-4e13-8d29-34ecd0376585",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "65c236cc-223f-45d4-9eab-33b2977f93de"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "9c7d2c3e-42b7-4150-8a75-5ca307bf5677"
        },
        {
          "idJson": "716c177e-156d-409e-a659-cf4ee3ad9249"
        }
      ]
    },
    {
      "id": "858feab4-3f0d-449d-a79c-ee7e7a8997a8",
      "idJson": "ded06a03-d592-4181-a859-5aad31e0417f",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "6102fc65-b3fb-48ca-bd5f-35365a6bb284"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "35744209-94db-4ae8-aa47-f07b31b908e5"
        },
        {
          "idJson": "640c6923-6f57-4a2f-8110-f5665b6466ac"
        }
      ]
    },
    {
      "id": "e4917a9a-2e12-4121-bc70-beaf4e2fdb6c",
      "idJson": "1d34871b-3ac9-4e18-b11a-cf4cd24e17e2",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "f897bf75-a052-46eb-8cb8-8aeffe434413"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "d69ed23c-ecca-4840-bb57-5a9c8e603ece"
        },
        {
          "idJson": "7651cfbf-522b-4c5c-9b07-d4af29087b90"
        },
        {
          "idJson": "aca75afc-b144-46da-98f4-44ab1b703e11"
        }
      ]
    },
    {
      "id": "f7803029-6ec1-474e-a470-790bef1e850b",
      "idJson": "3a0bb61c-492f-4727-ac7e-785d270f4b2f",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "43c3579c-12a2-48b5-a1b3-17adc640bdee"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "f5fc0766-db98-4c84-8f45-6e3c370fc81f"
        },
        {
          "idJson": "9c912de8-9ca5-411f-af6a-768c172da0a3"
        }
      ]
    },
    {
      "id": "1de8bfc2-6565-41a0-8924-b64c37ce49bc",
      "idJson": "0e9acd45-ef9c-4f13-a384-fdd8c1ff5895",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "7515a3be-ff91-4e2b-8e84-115e55fe1a00"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "38ffe4d7-eff1-48e3-8b27-5b39b5d9141c"
        },
        {
          "idJson": "c383e022-7dbc-4423-bd71-2a5f2e1ce765"
        }
      ]
    },
    {
      "id": "fbc479c1-a122-4f3c-b953-8a15f991316c",
      "idJson": "6c002dfc-3c25-4ba9-99f4-c80139e8897d",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "cf1774a4-bbbc-4555-8fe9-111e13871c10"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "3ec67e12-6551-4b73-9fe7-7cdf03764def"
        },
        {
          "idJson": "e33d95a7-4ac7-4be1-8531-35ec08afaa4b"
        },
        {
          "idJson": "0377fc38-593b-4bb1-b598-d917ffcf5e55"
        }
      ]
    },
    {
      "id": "cf61c20a-fc32-482a-8d1b-6fbee965099c",
      "idJson": "0c4c07b3-a76b-433e-a607-e8a73c3fe112",
      "descricao": "PADRÃO",
      "posicao": 1,
      "grupoSemaforico": {
        "idJson": "90410e1f-bdda-4700-952d-f24b623b6f6b"
      },
      "tabelaEntreVerdesTransicoes": [
        {
          "idJson": "5bbcf0e0-e61e-4291-9f6c-cf1bfbf915a7"
        }
      ]
    }
  ],
  "tabelasEntreVerdesTransicoes": [
    {
      "id": "de33f221-f7f0-4118-90d4-49d3dd21ba3a",
      "idJson": "9c912de8-9ca5-411f-af6a-768c172da0a3",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "3a0bb61c-492f-4727-ac7e-785d270f4b2f"
      },
      "transicao": {
        "idJson": "91882aea-8354-4526-955f-69d3c999ae8d"
      }
    },
    {
      "id": "158545bf-4654-4e6d-a769-ccacba240485",
      "idJson": "5bbcf0e0-e61e-4291-9f6c-cf1bfbf915a7",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "0c4c07b3-a76b-433e-a607-e8a73c3fe112"
      },
      "transicao": {
        "idJson": "dd76570b-b68f-4e75-8958-e51c48d405ba"
      }
    },
    {
      "id": "ff76fd70-14c4-41bf-908d-4ef561c299be",
      "idJson": "0377fc38-593b-4bb1-b598-d917ffcf5e55",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "6c002dfc-3c25-4ba9-99f4-c80139e8897d"
      },
      "transicao": {
        "idJson": "54c491d2-d57c-4848-a3b1-c91ee586c644"
      }
    },
    {
      "id": "10b367d7-2dc7-48d4-85e2-c799f81aed8d",
      "idJson": "792982f9-fd9c-430f-a04d-69e4c656701c",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "e029f3a5-4b4f-4221-8db2-0146ac6238ac"
      },
      "transicao": {
        "idJson": "b0cb13d1-f984-47b3-b0df-6cec3540cb34"
      }
    },
    {
      "id": "4ff65729-ebe7-4d02-a58b-ce62d6178aaa",
      "idJson": "716c177e-156d-409e-a659-cf4ee3ad9249",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "31f8a81c-afd8-4e13-8d29-34ecd0376585"
      },
      "transicao": {
        "idJson": "0bead9e0-ebac-42e6-b2db-ffd751c286f7"
      }
    },
    {
      "id": "67ebad8a-cfcb-4d8f-8f39-e03f9b6110a8",
      "idJson": "a55a24d6-c437-4818-9083-4d596c4cdb92",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "d10b5fb2-017e-4ba4-9aa6-42f99074bf28"
      },
      "transicao": {
        "idJson": "8ad5d2f9-28d9-4df6-a161-d494cbe2ee59"
      }
    },
    {
      "id": "1d7e1d5a-da1e-4f16-876a-010827a001c4",
      "idJson": "9cc359ee-a47e-44f9-8098-750c114f8d32",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8"
      },
      "transicao": {
        "idJson": "1e89b323-0ae5-4c71-81b0-b88296277dfe"
      }
    },
    {
      "id": "c6715196-4319-49ba-87c9-10e98bda7d34",
      "idJson": "38ffe4d7-eff1-48e3-8b27-5b39b5d9141c",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "0e9acd45-ef9c-4f13-a384-fdd8c1ff5895"
      },
      "transicao": {
        "idJson": "63b8c923-1317-45c8-b93c-fd67541dd554"
      }
    },
    {
      "id": "b5192e49-cb33-4162-bf2c-883eeeacd492",
      "idJson": "640c6923-6f57-4a2f-8110-f5665b6466ac",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "ded06a03-d592-4181-a859-5aad31e0417f"
      },
      "transicao": {
        "idJson": "bcf0ac62-0a40-4889-a0f3-bf1664e8f7d7"
      }
    },
    {
      "id": "9e685b87-f19f-495e-b10f-84d4c444fb79",
      "idJson": "f5fc0766-db98-4c84-8f45-6e3c370fc81f",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "3a0bb61c-492f-4727-ac7e-785d270f4b2f"
      },
      "transicao": {
        "idJson": "eb51dfdd-dc60-4842-8e5e-d6dab1c32508"
      }
    },
    {
      "id": "38e588d6-3ca4-4b2f-b83e-b3e415c182ba",
      "idJson": "d69ed23c-ecca-4840-bb57-5a9c8e603ece",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "1d34871b-3ac9-4e18-b11a-cf4cd24e17e2"
      },
      "transicao": {
        "idJson": "a4058516-6bdd-497a-934a-8db37275187b"
      }
    },
    {
      "id": "2de93592-487b-4e3b-ae0e-35af894bc4b8",
      "idJson": "9c7d2c3e-42b7-4150-8a75-5ca307bf5677",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "31f8a81c-afd8-4e13-8d29-34ecd0376585"
      },
      "transicao": {
        "idJson": "9a0cbff0-7a77-43e3-968b-c8aaa9f62907"
      }
    },
    {
      "id": "87374644-cbce-493e-8cab-ccc532a4c7ea",
      "idJson": "7651cfbf-522b-4c5c-9b07-d4af29087b90",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "1d34871b-3ac9-4e18-b11a-cf4cd24e17e2"
      },
      "transicao": {
        "idJson": "a296531e-e704-4726-a07f-88b5e44cf195"
      }
    },
    {
      "id": "c68a177c-366b-47f4-af00-314b75c64ef2",
      "idJson": "8f6bf63f-3ed0-4368-bb5a-8b6890ba3bcd",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "e029f3a5-4b4f-4221-8db2-0146ac6238ac"
      },
      "transicao": {
        "idJson": "c880480c-7edb-43a4-b22c-f450f4664cf5"
      }
    },
    {
      "id": "8378f5fe-451b-4aab-bc17-46035278203b",
      "idJson": "3ec67e12-6551-4b73-9fe7-7cdf03764def",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "6c002dfc-3c25-4ba9-99f4-c80139e8897d"
      },
      "transicao": {
        "idJson": "257cb278-122a-4452-aaf2-af37417b7a46"
      }
    },
    {
      "id": "dbae841e-efbe-4911-a56c-f88cee88d64d",
      "idJson": "e33d95a7-4ac7-4be1-8531-35ec08afaa4b",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "6c002dfc-3c25-4ba9-99f4-c80139e8897d"
      },
      "transicao": {
        "idJson": "f91c7398-376b-4688-9260-977ebda02857"
      }
    },
    {
      "id": "14c9088d-a7aa-4ebe-b4b8-378fcb69e4c9",
      "idJson": "35744209-94db-4ae8-aa47-f07b31b908e5",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "ded06a03-d592-4181-a859-5aad31e0417f"
      },
      "transicao": {
        "idJson": "5492976d-2504-4d95-97a6-3f191e86d7cc"
      }
    },
    {
      "id": "8fe7151f-1b8e-4618-9b1d-1094da028e3d",
      "idJson": "cec18b18-5fa7-4b38-99d4-8ac3f6ebfda4",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "d10b5fb2-017e-4ba4-9aa6-42f99074bf28"
      },
      "transicao": {
        "idJson": "2baa63af-3b8c-4eba-96f8-ef827659544e"
      }
    },
    {
      "id": "cf4cb54d-b416-4eb7-8550-c4ab2c305503",
      "idJson": "c383e022-7dbc-4423-bd71-2a5f2e1ce765",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "0e9acd45-ef9c-4f13-a384-fdd8c1ff5895"
      },
      "transicao": {
        "idJson": "9f8ac533-48ed-4b61-88e2-0dcfbc7f41eb"
      }
    },
    {
      "id": "e12e0954-592c-4d1d-a295-a9e63d2fd15a",
      "idJson": "18a6bd08-9d8c-4fc1-b089-9aa8c390bfe1",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "0036f201-af00-4a82-bacf-1f8fe97281c8"
      },
      "transicao": {
        "idJson": "78472e8e-71e6-473e-b942-c8a54c51974d"
      }
    },
    {
      "id": "e4e72971-16f2-4f9a-bccb-9a08d45cb8f6",
      "idJson": "4880b0db-dbea-40ff-aef7-8f93df6035e9",
      "tempoAmarelo": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "d10b5fb2-017e-4ba4-9aa6-42f99074bf28"
      },
      "transicao": {
        "idJson": "4322e973-d657-4c8f-91f8-2c92226f4530"
      }
    },
    {
      "id": "97feb101-becb-47e8-bee1-580aef23d5e2",
      "idJson": "aca75afc-b144-46da-98f4-44ab1b703e11",
      "tempoVermelhoIntermitente": "3",
      "tempoVermelhoLimpeza": "0",
      "tempoAtrasoGrupo": "0",
      "tabelaEntreVerdes": {
        "idJson": "1d34871b-3ac9-4e18-b11a-cf4cd24e17e2"
      },
      "transicao": {
        "idJson": "09fe244e-74d5-463f-97e1-11e1c3e05d40"
      }
    }
  ]
}
```