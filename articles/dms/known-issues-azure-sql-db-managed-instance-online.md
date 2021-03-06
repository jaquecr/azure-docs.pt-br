---
title: Problemas conhecidos e limitações com migrações online para o Azure SQL Instância Gerenciada
description: Saiba mais sobre problemas conhecidos/limitações de migração associadas a migrações online para o Azure SQL Instância Gerenciada.
services: database-migration
author: pochiraju
ms.author: rajpo
manager: craigg
ms.reviewer: craigg
ms.service: dms
ms.workload: data-services
ms.custom: mvc
ms.topic: troubleshooting
ms.date: 02/20/2020
ms.openlocfilehash: 6393624cb4520ccd28dff41dd97746873bc13f59
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91330291"
---
# <a name="known-issuesmigration-limitations-with-online-migrations-to-azure-sql-managed-instance"></a>Problemas conhecidos/limitações de migração com migrações online para o Azure SQL Instância Gerenciada

Os problemas conhecidos e as limitações associadas a migrações online do SQL Server para o SQL Instância Gerenciada do Azure são descritos abaixo.

> [!IMPORTANT]
> Com as migrações online do SQL Server para o banco de dados SQL do Azure, não há suporte para a migração de tipos de dado de SQL_variant.

## <a name="backup-requirements"></a>Requisitos de backup

- **Backups com soma de verificação**

    O serviço de migração de banco de dados do Azure usa o método de backup e restauração para migrar seus bancos de dados locais para o SQL Instância Gerenciada. O serviço de migração de banco de dados do Azure só dá suporte a backups criados usando checksum

    [Habilitar ou desabilitar somas de verificação de backup durante backup ou restauração (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server?view=sql-server-2017)

    > [!NOTE]
    > Se você levar os backups de banco de dados com compactação, a soma de verificação será um comportamento padrão, a menos que explicitamente desabilitado.

    Com as migrações offline, se você escolher, **deixarei o serviço de migração de banco de dados do Azure...**, o serviço de migração de banco de dados do Azure pegará o backup do banco de dados com a opção checksum habilitada

- **Mídia de backup**

    Certifique-se de fazer cada backup em uma mídia de backup separada (arquivos de backup). O serviço de migração de banco de dados do Azure não dá suporte a backups que são anexados a um único arquivo de backup. Faça backups completos de log e logs para separar arquivos de backup.

## <a name="data-and-log-file-layout"></a>Layout do arquivo de dados e log

- **Número de arquivos de log**

    O serviço de migração de banco de dados do Azure não dá suporte a bancos de dados com vários arquivos de log. Se você tiver vários arquivos de log, reduza-os e reorganize-os em um único arquivo de log de transações. Como não é possível realizar o log remoto de arquivos que não estão vazios, você precisa fazer backup do arquivo de log primeiro.

## <a name="sql-server-features"></a>recursos do SQL Server

- **FileStream/filetables**

    Atualmente, o SQL Instância Gerenciada não dá suporte a FileStream e filetables. Para cargas de trabalho dependentes desses recursos, recomendamos que você opte por servidores SQL em execução em VMs do Azure como seu destino do Azure.

- **Tabelas na memória**

    O OLTP na memória está disponível nas camadas Premium e Comercialmente Crítico para SQL Instância Gerenciada; a camada de Uso Geral não dá suporte a OLTP na memória.

## <a name="migration-resets"></a>Redefinições de migração

- **Implantações**

    O SQL Instância Gerenciada é um serviço PaaS com aplicação automática de patches e atualizações de versão. Durante a migração do seu Instância Gerenciada SQL, atualizações não críticas são mantidas por até 36 horas. Posteriormente (e para atualizações críticas), se a migração for interrompida, o processo será redefinido para um estado de restauração completa.

    A transferência de migração só pode ser chamada depois que o backup completo é restaurado e é atualizado com todos os backups de log. Se seus migrações de migração de produção forem afetados, contate o [alias de comentários do Azure DMS](mailto:dmsfeedback@microsoft.com).
