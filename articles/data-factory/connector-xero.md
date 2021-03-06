---
title: Copiar dados do Xero usando o Azure Data Factory
description: Saiba como copiar dados do Xero para armazenamentos de dados de coletor com suporte usando uma atividade de cópia em um pipeline do Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: shwang
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 10/29/2020
ms.author: jingwang
ms.openlocfilehash: 342d0aabe2222393f33aa4ce93646da9f29cf1fb
ms.sourcegitcommit: dd45ae4fc54f8267cda2ddf4a92ccd123464d411
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2020
ms.locfileid: "92926454"
---
# <a name="copy-data-from-xero-using-azure-data-factory"></a>Copiar dados do Xero usando o Azure Data Factory

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Este artigo descreve como usar a atividade de cópia no Azure Data Factory para copiar dados de e para o Xero. Ele amplia o artigo [Visão geral da atividade de cópia](copy-activity-overview.md) que apresenta uma visão geral da atividade de cópia.

## <a name="supported-capabilities"></a>Funcionalidades com suporte

Este conector do Xero tem suporte para as seguintes atividades:

- [Atividade de cópia](copy-activity-overview.md) com [matriz de fonte/coletor com suporte](copy-activity-overview.md)
- [Atividade de pesquisa](control-flow-lookup-activity.md)

Você pode copiar dados de um Xero para qualquer armazenamento de dados de coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens/coletores da atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](copy-activity-overview.md#supported-data-stores-and-formats).

Especificamente, esse conector do Xero fornece suporte para:

- O [aplicativo privado](https://developer.xero.com/documentation/getting-started/getting-started-guide) Xero, mas não aplicativo público.
- Todas as tabelas Xero (pontos de extremidade de API), exceto "Relatórios".
- Autenticação OAuth 1,0 e OAuth 2,0.

Azure Data Factory fornece um driver interno para habilitar a conectividade, portanto, não é necessário instalar manualmente qualquer driver usando esse conector.

## <a name="getting-started"></a>Introdução

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

As seções a seguir fornecem detalhes sobre as propriedades usadas para definir entidades do Data Factory específicas ao conector do Xero.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado

As propriedades a seguir têm suporte para o serviço vinculado do Xero:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type | A propriedade type deve ser definida como: **Xero** | Yes |
| connectionProperties | Um grupo de propriedades que define como se conectar ao Xero. | Yes |
| **_Em `connectionProperties` :_* _ | | |
| host | O ponto de extremidade do servidor Xero (`api.xero.com`).  | Sim |
| authenticationType | Os valores permitidos são `OAuth_2.0` e `OAuth_1.0` . | Yes |
| consumerKey | A chave de consumidor associada ao aplicativo Xero. Marque este campo como uma SecureString para armazená-la com segurança no Data Factory ou [faça referência a um segredo armazenado no Azure Key Vault](store-credentials-in-key-vault.md). | Sim |
| privateKey | A chave privada do arquivo .pem que foi gerada para o aplicativo privado Xero, consulte [Criar um par de chaves pública/privada](https://developer.xero.com/documentation/auth-and-limits/create-publicprivate-key). Observação para _ *gerar o PrivateKey. pem com numbits de 512* * usando `openssl genrsa -out privatekey.pem 512` , não há suporte para 1024. Inclua todo o texto do arquivo .pem, incluindo as terminações de linha Unix (\n), consulte o exemplo abaixo.<br/>Marque este campo como uma SecureString para armazená-la com segurança no Data Factory ou [faça referência a um segredo armazenado no Azure Key Vault](store-credentials-in-key-vault.md). | Sim |
| tenantId | A ID do locatário associada ao aplicativo Xero. Aplicável para autenticação OAuth 2,0.<br>Saiba como obter a ID do locatário de [verificar os locatários que você está autorizado a acessar seção](https://developer.xero.com/documentation/oauth2/auth-flow). | Sim para autenticação OAuth 2,0 |
| refreshToken | Aplicável para autenticação OAuth 2,0.<br/>O token de atualização do OAuth 2,0 está associado ao aplicativo Xero e usado para atualizar o token de acesso; o token de acesso expira após 30 minutos. Saiba mais sobre como funciona o fluxo de autorização do Xero e como obter o token de atualização deste [artigo](https://developer.xero.com/documentation/oauth2/auth-flow). Para obter um token de atualização, você deve solicitar o [escopo de offline_access](https://developer.xero.com/documentation/oauth2/scopes). <br/>**Identificar limitação** : Observe que o Xero redefine o token de atualização depois de ser usado para a atualização do token de acesso. Para a carga de trabalho operacional, antes da execução de cada atividade de cópia, você precisa definir um token de atualização válido para o ADF usar.<br/>Marque este campo como uma SecureString para armazená-la com segurança no Data Factory ou [faça referência a um segredo armazenado no Azure Key Vault](store-credentials-in-key-vault.md). | Sim para autenticação OAuth 2,0 |
| useEncryptedEndpoints | Especifica se os endpoints de fonte de dados são criptografados usando HTTPS. O valor padrão é true.  | No |
| useHostVerification | Especifica se o nome do host é necessário no certificado do servidor para corresponder ao nome do host do servidor ao se conectar via TLS. O valor padrão é true.  | No |
| usePeerVerification | Especifica se a identidade do servidor deve ser verificada ao se conectar via TLS. O valor padrão é true.  | No |

**Exemplo: Autenticação OAuth 2,0**

```json
{
    "name": "XeroLinkedService",
    "properties": {
        "type": "Xero",
        "typeProperties": {
            "connectionProperties": { 
                "host": "api.xero.com",
                "authenticationType":"OAuth_2.0", 
                "consumerKey": {
                    "type": "SecureString",
                    "value": "<consumer key>"
                },
                "privateKey": {
                    "type": "SecureString",
                    "value": "<private key>"
                },
                "tenantId": "<tenant ID>", 
                "refreshToken": {
                    "type": "SecureString",
                    "value": "<refresh token>"
                }, 
                "useEncryptedEndpoints": true, 
                "useHostVerification": true, 
                "usePeerVerification": true
            }            
        }
    }
}
```

**Exemplo: Autenticação OAuth 1,0**

```json
{
    "name": "XeroLinkedService",
    "properties": {
        "type": "Xero",
        "typeProperties": {
            "connectionProperties": {
                "host": "api.xero.com", 
                "authenticationType":"OAuth_1.0", 
                "consumerKey": {
                    "type": "SecureString",
                    "value": "<consumer key>"
                },
                "privateKey": {
                    "type": "SecureString",
                    "value": "<private key>"
                }, 
                "useEncryptedEndpoints": true,
                "useHostVerification": true,
                "usePeerVerification": true
            }
        }
    }
}
```

**Valor de chave privada de exemplo:**

Inclua todo o texto do arquivo .pem incluindo as terminações de linha do Unix (\n).

```
"-----BEGIN RSA PRIVATE KEY-----\nMII***************************************************P\nbu****************************************************s\nU/****************************************************B\nA*****************************************************W\njH****************************************************e\nsx*****************************************************l\nq******************************************************X\nh*****************************************************i\nd*****************************************************s\nA*****************************************************dsfb\nN*****************************************************M\np*****************************************************Ly\nK*****************************************************Y=\n-----END RSA PRIVATE KEY-----"
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados

Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira o artigo sobre [conjuntos de dados](concepts-datasets-linked-services.md). Esta seção fornece uma lista das propriedades com suporte pelo conjunto de dados do Xero.

Para copiar dados do Xero, defina a propriedade type do conjunto de dados como **XeroObject** . Há suporte para as seguintes propriedades:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type | A propriedade Type do conjunto de conjuntos deve ser definida como: **XeroObject** | Sim |
| tableName | Nome da tabela. | Não (se "query" na fonte da atividade for especificada) |

**Exemplo**

```json
{
    "name": "XeroDataset",
    "properties": {
        "type": "XeroObject",
        "typeProperties": {},
        "schema": [],
        "linkedServiceName": {
            "referenceName": "<Xero linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia

Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Pipelines](concepts-pipelines-activities.md). Esta seção fornece uma lista das propriedades com suporte pela fonte do Xero.

### <a name="xero-as-source"></a>Xero como fonte

Para copiar dados de Xero, defina o tipo de fonte na atividade de cópia como **XeroSource** . As propriedades a seguir têm suporte na seção **source** da atividade de cópia:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type | A propriedade type da fonte da atividade de cópia deve ser definida como: **XeroSource** | Sim |
| Consulta | Utiliza a consulta SQL personalizada para ler os dados. Por exemplo: `"SELECT * FROM Contacts"`. | Não (se "tableName" no conjunto de dados for especificado) |

**Exemplo:**

```json
"activities":[
    {
        "name": "CopyFromXero",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Xero input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "XeroSource",
                "query": "SELECT * FROM Contacts"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

Observe o seguinte ao especificar a consulta Xero:

- Tabelas com itens complexos serão divididas em várias tabelas. Por exemplo, as transações bancárias possuem uma estrutura de dados complexa "LineItems", portanto, os dados de transação bancária são mapeados para a tabela `Bank_Transaction` e `Bank_Transaction_Line_Items`, com `Bank_Transaction_ID` como chave estrangeira para vinculá-los.

- Os dados do Xero estão disponíveis através de dois esquemas: `Minimal` (padrão) e `Complete`. O esquema completo contém tabelas de chamadas prévias que requerem dados adicionais (por exemplo, Coluna de ID) antes de fazer a consulta desejada.

As tabelas a seguir possuem a mesma informação no esquema Mínimo e Completo. Para reduzir o número de chamadas à API, use o esquema Mínimo (padrão).

- Bank_Transactions
- Contact_Groups 
- Contatos 
- Contacts_Sales_Tracking_Categories 
- Contacts_Phones 
- Contacts_Addresses 
- Contacts_Purchases_Tracking_Categories 
- Credit_Notes 
- Credit_Notes_Allocations 
- Expense_Claims 
- Expense_Claim_Validation_Errors
- Faturas 
- Invoices_Credit_Notes
- Invoices_ Prepayments 
- Invoices_Overpayments 
- Manual_Journals 
- Pagamentos a maior 
- Overpayments_Allocations 
- Pagamento antecipado 
- Prepayments_Allocations 
- Recebimentos 
- Receipt_Validation_Errors 
- Tracking_Categories

As tabelas a seguir somente podem ser consultadas com o esquema completo:

- Complete.Bank_Transaction_Line_Items 
- Complete.Bank_Transaction_Line_Item_Tracking 
- Complete.Contact_Group_Contacts 
- Complete.Contacts_Contact_ Persons 
- Complete.Credit_Note_Line_Items 
- Complete.Credit_Notes_Line_Items_Tracking 
- Complete.Expense_Claim_ Payments 
- Complete.Expense_Claim_Receipts 
- Complete.Invoice_Line_Items 
- Complete.Invoices_Line_Items_Tracking
- Complete.Manual_Journal_Lines 
- Complete.Manual_Journal_Line_Tracking 
- Complete.Overpayment_Line_Items 
- Complete.Overpayment_Line_Items_Tracking 
- Complete.Prepayment_Line_Items 
- Complete.Prepayment_Line_Item_Tracking 
- Complete.Receipt_Line_Items 
- Complete.Receipt_Line_Item_Tracking 
- Complete.Tracking_Category_Options

## <a name="lookup-activity-properties"></a>Pesquisar propriedades de atividade

Para saber detalhes sobre as propriedades, verifique [Pesquisar atividade](control-flow-lookup-activity.md).


## <a name="next-steps"></a>Próximas etapas
Para obter uma lista de armazenamentos de dados com suporte pela atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](copy-activity-overview.md#supported-data-stores-and-formats).
