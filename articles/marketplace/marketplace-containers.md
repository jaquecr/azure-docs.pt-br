---
title: Guia de publicação para ofertas de contêiner no Azure Marketplace
description: Este artigo descreve os requisitos para publicar ofertas de contêiner no Azure Marketplace.
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
author: keferna
ms.author: keferna
ms.date: 09/04/2020
ms.openlocfilehash: c52fabcfc2ff22df2de6dd93f2543d625310baef
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89484334"
---
# <a name="publishing-guide-for-container-offers"></a>Guia de publicação para ofertas de contêiner

O contêiner oferece ajuda para publicar sua imagem de contêiner no Azure Marketplace. Use este guia para compreender os requisitos dessa oferta. 

Ofertas de contêiner são ofertas de transações que são implantadas e cobradas por meio do Azure Marketplace. A opção de listagem que um usuário vê é "obter agora".

Use o tipo de oferta de *contêiner* quando sua solução for uma imagem de contêiner do Docker configurada como uma instância do serviço de contêiner do Azure baseada em kubernetes. 

> [!NOTE]
> Exemplos de instâncias do serviço de contêiner do Azure baseadas em kubernetes são o serviço kubernetes do Azure ou as instâncias de contêiner do Azure, a escolha de clientes do Azure para um tempo de execução de contêiner baseado em kubernetes.  

A Microsoft atualmente dá suporte a modelos de licenciamento BYOL (traga sua própria licença) e gratuito.

## <a name="container-offer-requirements"></a>Requisitos da oferta de contêiner

| Requisito | Detalhes |  
|:--- |:--- |  
| Cobrança e medição | Suporte a qualquer modelo de cobrança gratuito ou BYOL.<br><br> |  
| Imagem criada a partir de um Dockerfile | As imagens de contêiner devem ser baseadas na especificação de imagem do Docker e criadas a partir de um Dockerfile.<br> <br>Para obter mais informações sobre a criação de imagens do Docker, consulte a seção "uso" da [referência de Dockerfile](https://docs.docker.com/engine/reference/builder/#usage).<br><br> |  
| Hospedando em um repositório do registro de contêiner do Azure | As imagens de contêiner devem ser hospedadas em um repositório do registro de contêiner do Azure.<br> <br>Para obter mais informações sobre como trabalhar com o registro de contêiner do Azure, consulte [início rápido: criar um registro de contêiner privado usando o portal do Azure](../container-registry/container-registry-get-started-portal.md).<br><br> |  
| Marcação de imagens | As imagens de contêiner devem conter pelo menos uma marca (número máximo de marcas: 16).<br><br>Para obter mais informações sobre como marcar uma imagem, consulte a `docker tag` página no site de [documentação do Docker](https://docs.docker.com/engine/reference/commandline/tag) .<br><br> |  

## <a name="next-steps"></a>Próximas etapas

Se você ainda não fez isso, saiba como [Aumentar seus negócios na nuvem com o Azure Marketplace](https://azuremarketplace.microsoft.com/sell).

Para se registrar e começar a trabalhar no Partner Center:

- [Entre no Partner Center](https://partner.microsoft.com/dashboard/account/v3/enrollment/introduction/partnership) para criar ou concluir sua oferta.
- Consulte [criar uma oferta de contêiner do Azure](./partner-center-portal/create-azure-container-offer.md) para obter mais informações.
