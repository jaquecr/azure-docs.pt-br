---
title: Gerar uma cadeia de conexão com o PowerShell – Banco de Dados do Azure para MariaDB
description: Este artigo apresenta um exemplo do Azure PowerShell de como gerar uma cadeia de conexão para se conectar ao Banco de Dados do Azure para MariaDB.
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.custom: mvc, devx-track-azurepowershell
ms.topic: how-to
ms.date: 8/5/2020
ms.openlocfilehash: b08a1c60b1225b2786ea869f96ac40cc651c82f3
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "88185597"
---
# <a name="how-to-generate-an-azure-database-for-mariadb-connection-string-with-powershell"></a>Como gerar uma cadeia de conexão do Banco de Dados do Azure para MariaDB com o PowerShell

Este artigo demonstra como gerar uma cadeia de conexão para um servidor de Banco de Dados do Azure para MariaDB. Você pode usar uma cadeia de conexão para se conectar a um Banco de Dados do Azure para MariaDB em muitos diferentes aplicativos.

## <a name="requirements"></a>Requisitos

Este artigo usa os recursos criados no seguinte guia como ponto de partida:

* [Início Rápido: Criar um servidor do Banco de Dados do Azure para MariaDB usando o PowerShell](quickstart-create-mariadb-server-database-using-azure-powershell.md)

## <a name="get-the-connection-string"></a>Obtenha a cadeia de conexão

O cmdlet `Get-AzMariaDbConnectionString` é usado para gerar uma cadeia de conexão a fim de conectar aplicativos ao Banco de Dados do Azure para MariaDB. O exemplo a seguir retorna a cadeia de conexão para um cliente PHP de **mydemoserver**.

```azurepowershell-interactive
Get-AzMariaDbConnectionString -Client PHP -Name mydemoserver -ResourceGroupName myresourcegroup
```

```Output
$con=mysqli_init();mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL); mysqli_real_connect($con, "mydemoserver.mariadb.database.azure.com", "myadmin@mydemoserver", {your_password}, {your_database}, 3306);
```

Os valores válidos para o parâmetro `Client` incluem:

* ADO&#46;NET
* JDBC
* Node.js
* PHP
* Python
* Ruby
* WebApp

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Personalizar parâmetros do servidor do Banco de Dados do Azure para MariaDB usando o PowerShell](howto-configure-server-parameters-using-powershell.md)
