# API para Rastreio
versão 1.0

## Visão Geral
Através desta API é possível integrar seu sistema/plataforma de maneira simples e descomplicada com a Frete Rápido.

O Rastreio se dará pelos seguintes passos:

- Simulação da oferta: Ao criar o pedido na Frete Rápido, nós precisaremos de pelo menos 1 oferta de transportadora vinculada a ele, por isso primeiro nós criamos as ofertas.
- Contratação da oferta: Na sequência, essa oferta é confirmada junto com o input das demais informações do pedido. Nesta etapa nós vamos devolver o código de rastreio, bem como a URL da página de rastreio desse pedido.
- Rastreio pelas transportadoras: A transportadora manterá nosso sistema atualizado do rastreio via integração ou via nosso aplicativo de rastreio em tempo real.
- Devolução do rastreio: Nós disponibilizamos o rastreio tanto por consulta ativa via GET, quanto por disparo via Webhook, ou por consulta via página do rastreio

### Formato de Comunicação
Toda a comunicação da API do Frete Rápido é através do formato JSON.

```json
Content-Type: "Application/JSON"
Accept: "Application/JSON"
```

É considerado uma boa prática definir que todas as requisições sejam no formato **​Application/JSON**. Mesmo que este não seja definido, as requisições serão realizadas nesse formato.

### Token de Integração
Todas as requisições realizadas ao Frete Rápido devem incluir o token de integração para validação do método. O token fica disponível em "Dados da Empresa" dentro do painel de controle.

```json
token: "AA73388183D2B215CF39491E2B74AAAA"
```
Caso haja algum erro com o **token de integração**, será retornado a mensagem **401 - Não autorizado (Token inválido)**.

Cada empresa tem apenas um único token de integração. Caso não possua seu token de integração, entre em contato conosco pelo canal integracoes@freterapido.com e solicite o seu.

É preciso ter cadastro na plataforma Frete Rápido previamente, a fim de permitir a integração da sua empresa.

***Destacamos que a sua integração será considerada apta para funcionamento, após passar pelo processo de Testes e Homologação da Frete Rápido.***

## Tipos de Volumes
Os Tipos de Volumes do Frete Rápido permite indicar o tipo de produto (categoria) que deseja transportar.

Observação: Nem todas as categorias da sua loja podem corresponder diretamente a relação do Frete Rápido, mas é possível relacioná-las de forma ampla.

- Exemplo 1: Moda feminina –> Vestuário
- Exemplo 2: CDs –> CD / DVD / Blu-Ray
- Exemplo 3: Violões –> Instrumento Musical

Lista dos tipos de volumes e seus códigos de referência, utilizados nas cotações:

| Código | Produto                              |
|--------|--------------------------------------|
| 1      | Abrasivos                            |
| 109    | Acessório para decoração (com vidro) |
| 110    | Acessório para decoração (sem vidro) |
| 111    | Acessórios automotivos               |
| 69     | Acessórios de Airsoft / Paintball    |
| 73     | Acessórios de Arquearia              |
| 149    | Acessórios de montaria               |
| 70     | Acessórios de Pesca                  |
| 112    | Acessórios para bicicleta            |
| 90     | Acessórios para celular              |
| 130    | Acessórios para Narguilés            |
| 132    | Acessórios para Tabacaria            |
| 2      | Adubos / Fertilizantes               |
| 74     | Alimentos não perecíveis             |
| 3      | Alimentos perecíveis                 |
| 145    | Armações de óculos                   |
| 72     | Arquearia                            |
| 113    | Artesanatos (com vidro)              |
| 93     | Artesanatos (sem vidro)              |
| 152    | Artigos de festas                    |
| 82     | Artigos para Camping                 |
| 4      | Artigos para Pesca                   |
| 5      | Auto Peças                           |
| 133    | Banheira Acrílico                    |
| 134    | Banheira de Aço Esmaltada            |
| 135    | Banheira Fibra de Vidro              |
| 128    | Bebedouros e Purificadores           |
| 6      | Bebidas / Destilados                 |
| 114    | Bicicletas (desmontada)              |
| 99     | Bijuteria                            |
| 7      | Brindes                              |
| 8      | Brinquedos                           |
| 146    | Caixa d'água (Completa)              |
| 75     | Caixa de embalagem                   |
| 136    | Caixa Plástica                       |
| 9      | Calçados                             |
| 115    | Cama / Mesa / Banho                  |
| 62     | Cargas refrigeradas/congeladas       |
| 137    | Cartucho de Gás                      |
| 10     | CD / DVD / Blu-Ray                   |
| 122    | Celulares e Smartphones              |
| 116    | Chapas de madeira                    |
| 121    | Chip de celular                      |
| 102    | Cocção Industrial                    |
| 66     | Colchão                              |
| 11     | Combustíveis / Óleos                 |
| 12     | Confecção                            |
| 13     | Cosméticos                           |
| 14     | Couro                                |
| 15     | Derivados Petróleo                   |
| 16     | Descartáveis                         |
| 17     | Editorial                            |
| 19     | Eletrodomésticos                     |
| 125    | Eletrodomésticos industriais         |
| 150    | Eletroportáteis                      |
| 18     | Eletrônicos                          |
| 20     | Embalagens                           |
| 138    | Equipamento oftalmológico            |
| 107    | Equipamentos de cozinha industrial   |
| 88     | Equipamentos de Segurança / API      |
| 151    | Equipamentos para solda              |
| 84     | Estiletes / Materiais Cortantes      |
| 106    | Estufa térmica                       |
| 21     | Explosivos / Pirotécnicos            |
| 126    | Expositor industrial                 |
| 87     | Extintores                           |
| 23     | Ferragens                            |
| 24     | Ferramentas                          |
| 25     | Fibras Ópticas                       |
| 26     | Fonográfico                          |
| 27     | Fotográfico                          |
| 28     | Fraldas / Geriátricas                |
| 29     | Higiene                              |
| 30     | Impressos                            |
| 31     | Informática / Computadores           |
| 32     | Instrumento Musical                  |
| 100    | Joia                                 |
| 144    | Lentes de contato                    |
| 86     | Limpeza                              |
| 77     | Linha Branca                         |
| 33     | Livro(s)                             |
| 79     | Malas / Mochilas                     |
| 117    | Manequins                            |
| 104    | Maquina de algodão doce              |
| 105    | Maquina de chocolate                 |
| 34     | Materiais Escolares                  |
| 35     | Materiais Esportivos                 |
| 36     | Materiais Frágeis                    |
| 97     | Materiais hidráulicos / Encanamentos |
| 37     | Material de Construção               |
| 38     | Material de Irrigação                |
| 154    | Material de Jardinagem               |
| 141    | Material de laboratório              |
| 39     | Material Elétrico / Lâmpada(s)       |
| 40     | Material Gráfico                     |
| 41     | Material Hospitalar                  |
| 42     | Material Odontológico                |
| 139    | Material oftalmológico               |
| 43     | Material Pet Shop                    |
| 50     | Material Plástico                    |
| 44     | Material Veterinário                 |
| 127    | Maçanetas                            |
| 22     | Medicamentos                         |
| 46     | Moto Peças                           |
| 47     | Mudas / Plantas                      |
| 80     | Máquina / Equipamentos               |
| 68     | Móveis com peças de vidro            |
| 64     | Móveis desmontados                   |
| 45     | Móveis montados                      |
| 129    | Narguilés                            |
| 999    | Outros                               |
| 48     | Papelaria / Documentos               |
| 63     | Papelão                              |
| 49     | Perfumaria                           |
| 98     | Pia / Vasos                          |
| 83     | Pilhas / Baterias                    |
| 92     | Pisos (cerâmica) / Revestimentos     |
| 96     | Placa de Energia Solar               |
| 51     | Pneus e Borracharia                  |
| 95     | Porta / Janelas (sem vidro)          |
| 118    | Portas / Janelas (com vidro)         |
| 124    | Portáteis industriais                |
| 85     | Produto Químico classificado         |
| 52     | Produtos Cerâmicos                   |
| 143    | Produtos de SexShop                  |
| 53     | Produtos Químicos Não Classificados  |
| 54     | Produtos Veterinários                |
| 94     | Quadros / Molduras                   |
| 81     | Rações / Alimento para Animal        |
| 101    | Refrigeração Industrial              |
| 153    | Relógios                             |
| 55     | Revistas                             |
| 148    | Selas e Arreios de montaria          |
| 56     | Sementes                             |
| 71     | Simulacro de Arma / Airsoft          |
| 65     | Sofá                                 |
| 57     | Suprimentos Agrícolas / Rurais       |
| 131    | Tabacaria                            |
| 147    | Tampa de Caixa d'água                |
| 108    | Tapeçaria / Cortinas / Persianas     |
| 123    | Telefonia Fixa e Sem Fio             |
| 142    | Tinta                                |
| 91     | Toldos                               |
| 119    | Torneiras                            |
| 67     | Travesseiro                          |
| 76     | TV / Monitores                       |
| 58     | Têxtil                               |
| 103    | Utensílios industriais               |
| 89     | Utilidades domésticas                |
| 59     | Vacinas                              |
| 120    | Vasos de polietileno                 |
| 60     | Vestuário                            |
| 61     | Vidros / Frágil                      |
| 78     | Vitaminas / Suplementos nutricionais |
| 140    | Óculos e acessórios                  |

## Ocorrências do Frete Rápido
As ocorrências do Frete Rápido definem o fluxo de rastreabilidade dos objetos embarcados:

| Código | Ocorrência                            |
|--------|---------------------------------------|
| 0      | Solicitado / Aguardando aceitação     |
| 1      | Aceito / Aguardando coleta            |
| 2      | Em trânsito                           |
| 3      | Entregue                              |
| 4      | Recusado                              |
| 5      | Entrega não realizada                 |
| 6      | Reentrega / Nova tentativa de entrega |
| 7      | Devolução / Retorno                   |
| 8      | Em trânsito para devolução            |
| 9      | Devolvido ao remetente                |
| 10     | Recusado 72h                          |
| 11     | Entrega parcial                       |
| 12     | Devolução parcial                     |
| 13     | Em trânsito para devolução parcial    |
| 14     | Devolvido parcialmente                |
| 15     | Coletado                              |
| 16     | Em transferência                      |
| 17     | Em rota para entrega                  |
| 18     | Sinistro ou Extravio                  |
| 19     | Disponível para retirada              |
| 97     | Problemas com endereço de entrega     |
| 98     | Problemas com a carga                 |
| 99     | Cancelado                             |

## Limite de requisições
Para evitar gargalos e imprevistos que possam influenciar sua operação, a API da Frete Rápido permite até 120 requisições por minuto, exceto o método de simulação da oferta permanece sem limites de requisições.

# **[POST]** Validação e Autenticação de Acesso
    https://freterapido.com/api/external/embarcador/v1/check-status

Permite verificar a autenticidade de acesso junto a API Frete Rápido.

## Envio:
Parâmetros do corpo da requisição:
    * Obrigatório
| Nome              | Descrição                                                                                                          | Formato / Exemplo                      | Obrigatório |
|-------------------|--------------------------------------------------------------------------------------------------------------------|----------------------------------------|-------------|
| cnpj              | CNPJ que possui cadastro na Frete Rápido                                                                           | String de 14 caracteres sem formatação | *           |
| token             | Chave de acesso gerada no seu Painel Frete Rápido                                                                  | String de 32 caracteres                | *           |
| codigo_plataforma | Código da plataforma de E-commerce que você utiliza. Solicite o seu código pelo canal integracoes@freterapido.com. | String                                 | *           |

### Exemplo de envio:
```json
{
    "cnpj": "",
    "token": "",
    "codigo_plataforma": ""
}
```

## Resposta:
Se a requisição obtiver sucesso, deve retornar o código de resposta **HTTP 200** conforme exemplo abaixo.

| Nome     | Descrição                             | Formato / Exemplo                                      | Retornado |
|----------|---------------------------------------|--------------------------------------------------------|-----------|
| bloqueio | status de bloqueio                    | Boolean: True para bloqueado e False para desbloqueado | Sempre    |
| saldo    | Quantidade de envios ainda disponível | Numérico (inteiro)                                     | Sempre    |

### Exemplo de resposta:
```json
    {
      "bloqueio": true,
      "saldo": 0
    }
```

# **[POST]** Simulação da oferta
    https://freterapido.com/api/external/embarcador/v1/quote-simulator

Método que permite realizar a simulação de ofertas para o pedido.

Basta enviar os dados abaixo em uma requisição POST para a URL do método.

Para esse método, você pode utilizar, se preferir, o protocolo de comunicação GRPC, conforme o nosso SDK de comunicação GRPC no GitHub. (Consulte o suporte)

## Envio:

### Parâmetros do corpo da requisição:
    * Obrigatório
| Nome                  | Descrição                                                                                                                                                                                                                                                                     | Formato / Exemplo                                                                                                           | Obrigatório                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| remetente             | Objeto com alguns dados do remetente/origem                                                                                                                                                                                                                                   | Objeto em json                                                                                                              | *                                   |
| cnpj                  | CNPJ do remetente da carga                                                                                                                                                                                                                                                    | String Numérica de 14 caracteres sem formatação                                                                             | *                                   |
| expedidor¹            | Objeto com alguns dados do expedidor                                                                                                                                                                                                                                          | Objeto em json                                                                                                              | Se houver expedidor                 |
| cnpj                  | CNPJ do expedidor da carga. Também será utilizado para realizar a consolidação de volumes com as caixas cadastradas na Frete Rápido.                                                                                                                                          | String Numérica de 14 caracteres sem formatação                                                                             | Se houver expedidor                 |
| endereco              | -                                                                                                                                                                                                                                                                             | Objeto em json                                                                                                              | Se houver expedidor                 |
| cep                   | CEP do expedidor da carga                                                                                                                                                                                                                                                     | String Numérica de 8 caracteres sem formatação                                                                              | Se houver expedidor                 |
| destinatario          | Objeto com alguns dados do destinatário                                                                                                                                                                                                                                       | Objeto em json                                                                                                              | *                                   |
| tipo_pessoa           | Define o tipo de destinatário (Pessoa Jurídica ou Pessoa Física)                                                                                                                                                                                                              | Numérico (inteiro), 1 = pessoa física, 2 = pessoa jurídica                                                                  | *                                   |
| cnpj_cpf              | CNPJ ou CPF do destinatário da carga                                                                                                                                                                                                                                          | String Numérica de 11 ou 14 caracteres sem formatação                                                                       | Se destinatário for Pessoa Jurídica |
| inscricao_estadual    | Inscrição Estadual do destinatário da carga                                                                                                                                                                                                                                   | String                                                                                                                      | Se destinatário for Pessoa Jurídica |
| endereco              | Objeto com dados de endereço do destinatário da carga                                                                                                                                                                                                                         | Objeto em json                                                                                                              | *                                   |
| cep                   | CEP do destinatário / destino da carga                                                                                                                                                                                                                                        | String de 8 caracteres sem formatação                                                                                       | *                                   |
| volumes               | Array com um ou mais objetos dos volumes informados                                                                                                                                                                                                                           | Array em json                                                                                                               | *                                   |
|                       | Objeto com as características do volume informado                                                                                                                                                                                                                             | Objeto em json                                                                                                              | *                                   |
| tipo                  | Tipo do volume/produto informado (vide tabela de tipo de volumes)                                                                                                                                                                                                             | Numérico (inteiro)                                                                                                          | *                                   |
| sku                   | SKU do volume/produto informado                                                                                                                                                                                                                                               | String                                                                                                                      | Opcional                            |
| descricao             | Descrição do volume/produto informado                                                                                                                                                                                                                                         | String                                                                                                                      | Opcional                            |
| quantidade            | Quantidade de volumes/produtos iguais e do mesmo tipo                                                                                                                                                                                                                         | Numérico (inteiro)                                                                                                          | *                                   |
| altura                | Altura em Metros do volume/produto unitário                                                                                                                                                                                                                                   | Numérico (float)                                                                                                            | *                                   |
| largura               | Largura em Metros do volume/produto unitário                                                                                                                                                                                                                                  | Numérico (float)                                                                                                            | *                                   |
| comprimento           | Comprimento em Metros do volume/produto unitário                                                                                                                                                                                                                              | Numérico (float)                                                                                                            | *                                   |
| peso                  | Peso total (em Kg) da quantidade de volumes informados Exemplo: 6 volumes com 0.5 Kg cada, então o valor informado deve ser 3 Kg                                                                                                                                              | Numérico (float)                                                                                                            | *                                   |
| valor                 | Valor total da quantidade de volumes informados Exemplo: 6 volumes custando R$20,00 cada, então o valor informado deve ser R$120,00                                                                                                                                           | Numérico (float)                                                                                                            | *                                   |
| volumes_produto       | Quantidade de volumes do produto ao qual este volume pertence. Ex.: Este volume percente a um jogo de sofá que é composto por quatro volumes no mesmo SKU, então o campo deve ser preenchido com 4. Nós usaremos esta informação para agrupar os volumes de um mesmo produto. | Numérico (inteiro)                                                                                                          | Opcional                            |
| consolidar            | Consolidar volume? Default: false                                                                                                                                                                                                                                             | Boolean                                                                                                                     | Opcional                            |
| sobreposto            | Sobrepor volume sobre outro? Default: false                                                                                                                                                                                                                                   | Boolean                                                                                                                     | Opcional                            |
| tombar                | Tombar volume? Default: false                                                                                                                                                                                                                                                 | Boolean                                                                                                                     | Opcional                            |
| filtro                | Permite parametrizar o retorno das cotações                                                                                                                                                                                                                                   | Numérico (inteiro), 1 = Retornar somente a oferta com menor preço, 2 = Retornar somente a oferta com menor prazo de entrega | Opcional                            |
| canal                 | Permite filtrar a regra de frete pelo canal                                                                                                                                                                                                                                   | String (Texto)                                                                                                              | Opcional                            |
| limite                | Define a quantidade de cotações que deve retornar                                                                                                                                                                                                                             | Numérico (inteiro)                                                                                                          | Opcional                            |
| codigo_plataforma     | Informar código da plataforma de ecommerce. Solicite o código da sua plataforma ao Frete Rápido.                                                                                                                                                                              | String                                                                                                                      | *                                   |
| cotacao_plataforma    | Identificador da cotação na plataforma de ecommerce. Podendo agilizar a consulta de valores em caso de várias chamadas do mesmo carrinho de compras.                                                                                                                          | Numérico (inteiro)                                                                                                          | Opcional                            |
| token                 | Token de integração                                                                                                                                                                                                                                                           | String de 32 caracteres                                                                                                     | *                                   |
| retornar_consolidacao | Caso true retornará os volumes consolidados                                                                                                                                                                                                                                   | Boolean                                                                                                                     | Opcional                            |

¹ Expedidor é utilizado quando a transportadora deve coletar a mercadoria em outro local diferente do local do remetente, muito utilizado por empresas onde o remetente é de outro estado mas a mercadoria deve ser coletada no estado onde se encontra a transportadora. Exemplo: Uma empresa remetente de RS, Transportadora de SP, mercadoria deve ser coletada na filial da empresa que está em SP para ser entregue em BA. Nesse caso, o expedidor deve ser a filial de SP para que o conhecimento de transporte saia com origem SP, destino BA, ao invés de RS como origem.

### Exemplo de envio:

```json
{
    "remetente": {
        "cnpj": ""
    },
    "destinatario": {
        "tipo_pessoa": 2,
        "cnpj_cpf": "",
        "inscricao_estadual": "",
        "endereco": {
            "cep": ""
        }
    },
    "volumes": [
        {
            "tipo": 0,
            "sku": "",
            "descricao": "",
            "quantidade": ,
            "altura": 0.00,
            "largura": 0.00,
            "comprimento": 0.00,
            "peso": 0.00,
            "valor": 0.00,
            "volumes_produto": 0,
            "consolidar": false,
            "sobreposto": false,
            "tombar": false 
        },
        {
            "tipo": 0,
            "sku": "",
            "descricao": "",
            "quantidade": 0,
            "altura": 0.00,
            "largura": 0.00,
            "comprimento": 0.00,
            "peso": 0.00,
            "valor": 0.00,
            "volumes_produto": 0,
            "consolidar": false,
            "sobreposto": false,
            "tombar": false            
        }
    ],
    "codigo_plataforma": "",
    "token": "",
    "retornar_consolidacao": true 
}
```

## Resposta:
Se a requisição obtiver sucesso, será retornado o código de resposta **HTTP 200** com as ofertas que atendem a rota, conforme os dados e exemplo abaixo.

| Nome              | Descrição                                                                                                                                   | Formato / Exemplo                                  | Retornado                    |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|------------------------------|
| token_oferta      | Token único de identificação do cálculo de valores da simulação. Utilizado para contratação da oferta no método “Contratação”.              | String                                             | Sempre                       |
|                   |                                                                                                                                             |                                                    |                              |
| transportadoras   | Objeto com as ofertas das transportadoras                                                                                                   | Objeto em json                                     | Sempre                       |
| oferta            | Código de identificação da oferta. Utilizada na contratação da oferta.                                                                      | Numérico (inteiro)                                 | Sempre                       |
| cnpj              | CNPJ da transportadora                                                                                                                      | String numérica com 14 caracteres e sem formatação | Sempre                       |
| logotipo          | URL de caminho do logotipo da transportadora                                                                                                | String                                             | Sempre                       |
| nome              | Nome fantasia da transportadora                                                                                                             | String                                             | Sempre                       |
| servico           | Nome de serviço                                                                                                                             | String                                             | Sempre                       |
| descricao_servico | Descrição do serviço                                                                                                                        | String                                             | Eventualmente                |
| prazo_entrega     | Quantidade de dias úteis de previsão de entrega                                                                                             | Numérico (inteiro)                                 | Sempre                       |
| validade          | Data de validade da oferta da transportadora                                                                                                | String                                             | Sempre                       |
| custo_frete       | Custo real do frete calculado. Valor que deverá ser pago à transportadora.                                                                  | Numérico (float)                                   | Sempre                       |
| preco_frete       | Preço do frete que deverá ser apresentando ao cliente da loja. Obs.: Poderá ser diferente do custo_frete caso haja regra de frete aplicada. | Numérico (float)                                   | Sempre                       |
|                   |                                                                                                                                             |                                                    |                              |
| volumes           | Array com um ou mais objetos dos volumes informados ou consolidados                                                                         | Array em json                                      | retronar_consolidacao = true |
| tipo              | Tipo do volume (vide tabela de tipo de volumes)                                                                                             | Numérico (inteiro)                                 | Sempre                       |
| sku               | SKU do volume                                                                                                                               | String                                             | Eventualmente                |
| descricao         | Descrição do volume                                                                                                                         | String                                             | Eventualmente                |
| quantidade        | Quantidade de volumes/produtos iguais e do mesmo tipo                                                                                       | Numérico (inteiro)                                 | Sempre                       |
| altura            | Altura em Metros do volume                                                                                                                  | Numérico (float)                                   | Sempre                       |
| largura           | Largura em Metros do volume                                                                                                                 | Numérico (float)                                   | Sempre                       |
| comprimento       | Comprimento em Metros do volume                                                                                                             | Numérico (float)                                   | Sempre                       |
| peso              | Peso total (em Kg) da quantidade de volumes informados                                                                                      | Numérico (float)                                   | Sempre                       |
| valor             | Valor total da quantidade de volumes informados                                                                                             | Numérico (float)                                   | Sempre                       |
| volumes_produto   | Quantidade de volumes do produto ao qual este volume pertence.                                                                              | Numérico (inteiro)                                 | Eventualmente                |
|                   |                                                                                                                                             |                                                    |                              |
| itens             | Array com um ou mais objetos pertencentes ao volume consolidado                                                                             | Array em json                                      | Eventualmente                |
| tipo              | Tipo do volume (vide tabela de tipo de volumes)                                                                                             | Numérico (inteiro)                                 | Sempre                       |
| sku               | SKU do volume                                                                                                                               | String                                             | Eventualmente                |
| descricao         | Descrição do volume                                                                                                                         | String                                             | Eventualmente                |
| quantidade        | Quantidade de volumes/produtos iguais e do mesmo tipo                                                                                       | Numérico (inteiro)                                 | Sempre                       |
| altura            | Altura em Metros do volume                                                                                                                  | Numérico (float)                                   | Sempre                       |
| largura           | Largura em Metros do volume                                                                                                                 | Numérico (float)                                   | Sempre                       |
| comprimento       | Comprimento em Metros do volume                                                                                                             | Numérico (float)                                   | Sempre                       |
| peso              | Peso total (em Kg) da quantidade de volumes informados                                                                                      | Numérico (float)                                   | Sempre                       |
| valor             | Valor total da quantidade de volumes informados                                                                                             | Numérico (float)                                   | Sempre                       |
| volumes_produto   | Quantidade de volumes do produto ao qual este volume pertence.                                                                              | Numérico (inteiro)                                 | Eventualmente                |

### Exemplo de resposta:
```json
{
    "token_oferta": "769587e44bb8d663",
    "transportadoras": [
        {
            "oferta": 200,
            "cnpj": "11111111000111",
            "logotipo": "http://freterapido.app/logotipo/pac.png",
            "nome": "Correios",
            "servico": "PAC",
            "descricao_servico": "PAC contrato UO",
            "prazo_entrega": 5,
            "validade": "2018-08-19",
            "custo_frete": 36.19,
            "preco_frete": 38.79
        },
        {
            "oferta": 201,
            "cnpj": "22222222000122",
            "logotipo": "http://freterapido.app/logotipo/sedex.png",
            "nome": "Correios",
            "servico": "SEDEX",
            "descricao_servico": "SEDEX contrato UO",
            "prazo_entrega": 3,
            "validade": "2018-08-19",
            "custo_frete": 78.52,
            "preco_frete": 81.09
        },
        {
            "oferta": 202,
            "cnpj": "33333333000133",
            "logotipo": "http://freterapido.app/logotipo/transportadora.png",
            "nome": "TRANSPORTADORA A",
            "servico": "Rodoviário",
            "prazo_entrega": 6,
            "validade": "2018-06-19",
            "custo_frete": 100.77,
            "preco_frete": 103.34
        },
        {
            "oferta": 203,
            "cnpj": "44444444000144",
            "logotipo": "http://freterapido.app/logotipo/transportadora.png",
            "nome": "TRANSPORTADORA B",
            "servico": "Rodoviário",
            "prazo_entrega": 4,
            "validade": "2018-12-19",
            "custo_frete": 125.72,
            "preco_frete": 128.29
        }
      ],
      "volumes":[
        {
            "tipo": 64,
            "sku": "MTC-220-AM",
            "descricao": "Sofá Anjos Confortable 3 Lugares Retrátil E Reclinável Velud",
            "quantidade": 3,
            "altura": 0.52,
            "largura": 0.42,
            "comprimento": 0.30,
            "peso": 29.75,
            "valor": 542.56,
            "volumes_produto": 4
        },
        {
            "tipo": 64,
            "sku": "MTC-220-AM",
            "descricao": "Sofá Anjos Confortable 3 Lugares Retrátil E Reclinável Velud",
            "quantidade": 1,
            "altura": 0.52,
            "largura": 0.40,
            "comprimento": 0.30,
            "peso": 29.75,
            "valor": 542.56,
            "volumes_produto": 4
        },
        {
            "tipo": 999,
            "sku": null,
            "descricao": "Caixa pequena",
            "quantidade": 1,
            "altura": 0.20,
            "largura": 0.20,
            "comprimento": 0.30,
            "peso": 1.50,
            "valor": 2592.30,
            "volumes_produto": 1,
            "itens" :[
                {
                    "tipo": 18,
                    "sku": "SS-GJ8-MG",
                    "descricao": "Smartphone Samsung Galaxy J8 64GB Prata 4G - 4GB RAM",
                    "quantidade": 1,
                    "altura": 0.15,
                    "largura": 0.10,
                    "comprimento": 0.05,
                    "peso": 0.50,
                    "valor": 1079.10,
                    "volumes_produto": 1
                },
                {
                    "tipo": 18,
                    "sku": "SM-G7P-MG",
                    "descricao": "Smartphone Motorola G7 Play 32GB Indigo 4G - 2GB RAM",
                    "quantidade": 1,
                    "altura": 0.15,
                    "largura": 0.10,
                    "comprimento": 0.05,
                    "peso": 0.50,
                    "valor": 839.10,
                    "volumes_produto": 1
                },
                {
                    "tipo": 18,
                    "sku": "SLG-K12-MG",
                    "descricao": "Smartphone LG K12+ 32GB Platinum 4G 3GB RAM",
                    "quantidade": 1,
                    "altura": 0.15,
                    "largura": 0.10,
                    "comprimento": 0.05,
                    "peso": 0.50,
                    "valor": 674.10,
                    "volumes_produto": 1
                }
            ]
        }
    ]
}
```

# **[POST]** Contratação da oferta
    https://freterapido.com/api/external/embarcador/v1/quote/ecommerce/[token_oferta]/offer/[oferta]?token=[seu_token]

Método que permite realizar o registro da oferta para o pedido, com base em uma oferta anteriormente simulada. É aqui onde vamos receber as demais informações para finalização do pedido.

Basta enviar uma requisição do tipo POST com os parâmetros estabelecidos abaixo.

## Envio:

### Parâmetros da URL:
    * obrigatório

| Nome         | Descrição                        | Formato / Exemplo       | Obrigatório |
|--------------|----------------------------------|-------------------------|-------------|
| token_oferta | Token identificador da simulação | String de 16 caracteres | *           |
| oferta       | Identificador da oferta          | Numérico (inteiro)      | *           |
| token        | Token de integração              | String de 32 caracteres | *           |

### Parâmetros do corpo da requisição:
    * obrigatório

| Nome               | Descrição                                                                                                           | Formato / Exemplo                                     | Obrigatório                         |
|--------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|-------------------------------------|
| remetente          | Objeto com alguns dados do remetente/origem                                                                         | Objeto em json                                        | *                                   |
| cnpj               | CNPJ do remetente                                                                                                   | String Numérica de 14 caracteres sem formatação       | *                                   |
| expedidor¹         | Objeto com dados de endereço do expedidor da carga                                                                  | Objeto em json                                        | Se houver expedidor                 |
| cnpj               | CNPJ do expedidor da carga                                                                                          | String Numérica de 14 caracteres sem formatação       | Se houver expedidor                 |
| razao_social       | Razão social do expedidor                                                                                           | String                                                | Se houver expedidor                 |
| inscricao_estadual | Inscrição Estadual do expedidor da carga                                                                            | String                                                | Se houver expedidor                 |
| endereco           |                                                                                                                     | Objeto em json                                        | Se houver expedidor                 |
| cep                | CEP do expedidor / origem da carga                                                                                  | String Numérica de 8 caracteres sem formatação        | Se houver expedidor                 |
| rua                | Logradouro do expedidor                                                                                             | String                                                | Se houver expedidor                 |
| numero             | Número do local do expedidor                                                                                        | String                                                | Se houver expedidor                 |
| bairro             | Bairro do expedidor                                                                                                 | String                                                | Se houver expedidor                 |
| complemento        | Complemento do endereço (se houver)                                                                                 | String                                                | Opcional                            |
| destinatario       | Objeto com dados de endereço do destinatário da carga                                                               | Objeto em json                                        | *                                   |
| cnpj_cpf           | CNPJ ou CPF do destinatário da carga                                                                                | String Numérica de 11 ou 14 caracteres sem formatação | *                                   |
| inscricao_estadual | Inscrição Estadual do destinatário da carga                                                                         | String                                                | Se destinatário for Pessoa Jurídica |
| nome               | Nome ou Razão Social do destinatário                                                                                | String de até 255 caracteres                          | *                                   |
| email              | Endereço de e-mail do destinatário para casos de necessidade de contato por parte da transportadora                 | String                                                | Se destinatário for Pessoa Jurídica |
| telefone           | Telefone do destinatário para casos de necessidade de contato pela transportadora                                   | String Numérica sem formatação                        | Opcional                            |
| endereco           | Endereço do destinatário                                                                                            | String                                                | *                                   |
| cep                | CEP do destinatário                                                                                                 | String Numérica de 8 caracteres sem formatação        | *                                   |
| rua                | Logradouro do destinatário                                                                                          | String                                                | *                                   |
| numero             | Número do local do destinatário                                                                                     | String                                                | *                                   |
| bairro             | Bairro do destinatário                                                                                              | String                                                | *                                   |
| complemento        | Complemento do endereço (se houver)                                                                                 | String                                                | Opcional                            |
| numero_pedido      | Número do pedido na loja                                                                                            | String Numérica                                       | Opcional                            |
| nota_fiscal        | Objeto com os dados da nota fiscal                                                                                  | Objeto em json                                        | Opcional                            |
| numero             | Número da nota fiscal                                                                                               | String Numérica                                       | Se Houver NF                        |
| serie              | Série da nota fiscal                                                                                                | String Numérica                                       | Se Houver NF                        |
| quantidade_volumes | Quantidade de Volumes da nota fiscal                                                                                | String Numérica                                       | Se houver NF                        |
| chave_acesso       | Chave de acesso da nota fiscal                                                                                      | String Numérica                                       | Se Houver NF                        |
| valor              | Valor da nota fiscal                                                                                                | Numérico (float)                                      | Se Houver NF                        |
| valor_itens        | Valor total dos itens da nota fiscal                                                                                | Numérico (float)                                      | Se houver NF                        |
| data_emissao       | Data da emissão da nota fiscal                                                                                      | Date ("YYYY-MM-DD HH:II:SS")                          | Se houver NF                        |
| data_coleta        | Data de possível coleta informada pelo Embarcador. Atenção! Este poderá ser aceito ou recusado pela Transportadora. | Date ("YYYY-MM-DD")                                   | Opcional                            |

### Exemplo de envio:

```json
{
    "remetente": {
        "cnpj": ""
    },
    "destinatario": {
        "cnpj_cpf": "",
        "nome": "",
        "email": "",
        "telefone": "",
        "endereco": {
            "cep": "",
            "rua": "",
            "numero": "",
            "bairro": "",
            "complemento": ""
        }
    },
    "numero_pedido": "",
    "nota_fiscal": {
        "numero": "",
        "serie": "",
        "quantidade_volumes": "",
        "chave_acesso": "",
        "valor": 0.00,
        "valor_itens": 0.00,
        "data_emissao": "2016-02-15 13:40:00"
    },
    "data_coleta": "2017-04-26"
}
```

# Resposta:
Se a requisição obtiver sucesso, será retornado o código de resposta **HTTP 200** com as ofertas que atendem a rota, conforme os dados e exemplo abaixo.
    * Obrigatório

| Nome     | Descrição                                                                                    | Formato / Exemplo       | Retornado |
|----------|----------------------------------------------------------------------------------------------|-------------------------|-----------|
| id_frete | Identificador do frete contratado no Frete Rápido. Pode ser utilizado para rastrear o frete. | String de 13 caracteres | sempre    |
| rastreio | URL de rastreio do frete pelo ID Frete Rápido.                                               | String                  | sempre    |


```json
    {
        "id_frete": "FR190830JGS1W",
        "rastreio": "https://ondeestameupedido.com.br/FR000000ABCD"
    }
```

# **[GET]** Rastreamento / Ocorrências do frete
    https://freterapido.com/api/external/embarcador/v1/quotes/[id_frete]/occurrences?token=[seu_token]

Permite consultar todas as ocorrências de rastreio de um frete.

As ocorrências são apresentadas por ordem de acontecimento.

Através de um método **GET** basta informar o identificador do frete e o token de integração, conforme exemplo abaixo.

Se desejar, pode apresentar a URL de rastreio aos seus clientes composto da URL base + o identificador do frete, como: *https://ondeestameupedido.com.br/FR000000ABCD*

## Envio:

### Parâmetros da URL:
    * Obrigatório

| Nome     | Descrição                                                                                    | Formato / Exemplo       | Obrigatório |
|----------|----------------------------------------------------------------------------------------------|-------------------------|-------------|
| id_frete | Identificador do frete contratado no Frete Rápido. Pode ser utilizado para rastrear o frete. | String de 13 caracteres | *           |
| token    | Token de integração                                                                          | String de 32 caracteres | *           |

## Resposta:
Se a requisição obtiver sucesso, será retornado o código de resposta **HTTP 200**, juntamente com os dados de rastreio do frete informado.

| Nome             | Descrição                                                   | Formato / Exemplo              | Retornado            |
|------------------|-------------------------------------------------------------|--------------------------------|----------------------|
| codigo           | Código numérico da ocorrência no Frete Rápido               | Numérico (inteiro)             | Sempre               |
| nome             | Nome da ocorrência                                          | String                         | Sempre               |
| data_ocorrencia  | Data da ocorrência                                          | Datetime (YYYY-MM-DD HH:II:SS) | Sempre               |
| data_atualizacao | Data de atualização da ocorrência                           | Datetime (YYYY-MM-DD HH:II:SS) | Sempre               |
| data_reentrega   | Data em caso de nova tentativa de entrega                   | Date (YYYY-MM-DD)              | Em caso de reentrega |
| prazo_devolucao  | Quantidade de dias úteis para devolução da carga/mercadoria | String                         | Em caso de devolução |
| mensagem         | Mensagem livre para informação pela transportadora          | String até 255 caracteres      | Eventual             |

### Exemplo de resposta:

```json
[
    {
        "codigo": "1",
        "nome": "Aguardando coleta",
        "data_ocorrencia": "2016-10-14 17:49:37",
        "data_atualizacao": "2016-10-14 17:49:37",
        "data_reentrega": "2016-10-14",
        "prazo_devolucao": "",
        "mensagem": ""
    },
    {
        "codigo": "2",
        "nome": "Em trânsito",
        "data_ocorrencia": "2016-10-15 07:29:15",
        "data_atualizacao": "2016-10-15 07:29:15",
        "data_reentrega": "2016-10-14",
        "prazo_devolucao": "",
        "mensagem": ""
    },
    {
        "codigo": "3",
        "nome": "Entregue",
        "data_ocorrencia": "2016-10-20 08:35:29",
        "data_atualizacao": "2016-10-20 08:35:29",
        "data_reentrega": "2016-10-14",
        "prazo_devolucao": "",
        "mensagem": ""
    }
]
```

# **[POST]** Webhook de Ocorrências
    http://seusite.com/webhook/freterapido/v1/

O Webhook dispara à uma URL as alterações de ocorrências a medida em que ocorrem no sistema.

Assim, é possível criar uma URL esperando as notificações de um novo status, por meio de uma requisição **POST**, com os parâmetros listados abaixo.

## Envio:
### Parâmetros enviados no corpo da requisição:
    * obrigatório

| Nome               | Descrição                                                                                    | Formato / Exemplo              | Informado            |
|--------------------|----------------------------------------------------------------------------------------------|--------------------------------|----------------------|
| id_frete           | Identificador do frete contratado no Frete Rápido. Pode ser utilizado para rastrear o frete. | String de 13 caracteres        | *                    |
| numero_pedido      | Número do pedido                                                                             | String                         | *                    |
| codigo             | Código da ocorrência. Vide todas as ocorrências disponíveis no Frete Rápido.                 | Numérico (inteiro)             | *                    |
| nome               | Nome da ocorrência                                                                           | String                         | *                    |
| data_ocorrencia    | Data e hora da atualização da ocorrência pela transportadora ao Frete Rápido                 | Datetime (YYYY-MM-DD HH:II:SS) | *                    |
| data_reentrega     | Data de previsão de nova tentativa de entrega ao destinatário                                | Date (YYYY-MM-DD)              | Em caso de reentrega |
| prazo_devolucao    | Prazo em dias úteis para devolução da carga                                                  | Numérico (inteiro)             | Em caso de devolução |
| mensagem           | Mensagem de texto livre da transportadora                                                    | String de até 255 caracteres   | Eventual             |
| * Informado sempre |                                                                                              |                                |                      |

### Exemplo de envio:

```JSON
    {
        "id_frete": "",
        "numero_pedido": "",
        "codigo": 0,
        "nome": "",
        "data_ocorrencia": "2016-12-05 15:45",
        "data_reentrega": "2016-12-05",
        "prazo_devolucao": "",
        "mensagem": ""
    }
```

## Resposta:

Em caso de sucesso deverá ser retornado o código de resposta **HTTP 200**.
