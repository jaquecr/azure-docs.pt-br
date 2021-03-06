---
title: Não é possível excluir uma rede virtual no Azure | Microsoft Docs
description: Saiba como solucionar um problema em que você não consegue excluir uma rede virtual no Azure.
services: virtual-network
documentationcenter: na
author: chadmath
manager: dcscontentpm
editor: ''
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/31/2018
ms.author: genli
ms.openlocfilehash: 27372207df66b4198bd9c785ecc099fa88cbe548
ms.sourcegitcommit: 2a8a53e5438596f99537f7279619258e9ecb357a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2020
ms.locfileid: "94335665"
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a>Solucionar problemas: falha ao excluir uma rede virtual no Azure

Você poderá receber erros ao tentar excluir uma rede virtual no Microsoft Azure. Este artigo apresenta etapas para a solução de problemas para ajudá-lo a resolver esse problema.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Diretriz de solução de problemas 

1. [Verifique se um gateway de rede virtual está em execução na rede virtual](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Verifique se um gateway de aplicativo está em execução na rede virtual](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Verifique se as instâncias de contêiner do Azure ainda existem na rede virtual](#check-whether-azure-container-instances-still-exist-in-the-virtual-network).
4. [Verifique se o Serviço de Domínio do Azure Active Directory está habilitado na rede virtual](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
5. [Verifique se a rede virtual está conectada a outro recurso](#check-whether-the-virtual-network-is-connected-to-other-resource).
6. [Verifique se uma máquina virtual ainda está em execução na rede virtual](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
7. [Verifique se a rede virtual está presa na migração](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a>Verifique se um gateway de rede virtual está em execução na rede virtual

Para remover a rede virtual, você deve remover primeiro o gateway de rede virtual.

Para redes virtuais clássicas, vá para a página **Visão geral** da rede virtual clássica no portal do Azure. Na seção **conexões VPN** , se o gateway estiver em execução na rede virtual, você verá o endereço IP do gateway. 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Para redes virtuais, vá para a página **Visão geral** da rede virtual. Confira **Dispositivos conectados** para o gateway de rede virtual.

![Captura de tela da lista de dispositivos conectados para uma rede virtual no portal do Azure. O gateway de rede virtual é realçado na lista.](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Antes de remover o gateway, primeiro remova qualquer objeto de **Conexão** no gateway. 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a>Verifique se um gateway de aplicativo está em execução na rede virtual

Vá para a página **Visão geral** da rede virtual. Verifique os **Dispositivos conectados** para o gateway de aplicativo.

![Captura de tela da lista de dispositivos conectados para uma rede virtual no portal do Azure. O gateway de aplicativo é realçado na lista.](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Se houver um gateway de aplicativo, você deverá removê-lo antes de você pode excluir a rede virtual.

### <a name="check-whether-azure-container-instances-still-exist-in-the-virtual-network"></a>Verificar se as instâncias de contêiner do Azure ainda existem na rede virtual

1. Na portal do Azure, vá para a página **visão geral** do grupo de recursos.
1. No cabeçalho da lista de recursos do grupo de recursos, selecione **Mostrar tipos ocultos**. O tipo de perfil de rede fica oculto no portal do Azure por padrão.
1. Selecione o perfil de rede relacionado aos grupos de contêineres.
1. Selecione **Excluir**.

   ![Captura de tela da lista de perfis de rede ocultos.](media/virtual-network-troubleshoot-cannot-delete-vnet/container-instances.png)

1. Exclua a sub-rede ou a rede virtual novamente.

Se essas etapas não resolverem o problema, use esses [CLI do Azure comandos](https://docs.microsoft.com/azure/container-instances/container-instances-vnet#clean-up-resources) para limpar os recursos. 

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a>Verifique se o Serviço de Domínio do Azure Active Directory está habilitado na rede virtual

Se o Serviço de Domínio do Active Directory estiver habilitado e conectado à rede virtual, não será possível excluir essa rede virtual. 

![Captura da tela de Azure AD Domain Services na portal do Azure. O campo disponível na rede virtual/sub-rede é realçado.](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

Para desabilitar o serviço, consulte [Azure Active Directory Domain Services usando o portal do Azure](../active-directory-domain-services/delete-aadds.md).

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a>Verifique se a rede virtual está conectada a outro recurso

Verifique se há Links de Circuito, conexões e emparelhamentos de rede virtual. Qualquer uma dessas opções pode fazer a exclusão de uma rede virtual falhar. 

A ordem de exclusão recomendada é a seguinte:

1. Conexões de gateway
2. Gateways
3. IPs
4. Emparelhamentos de rede virtual
5. ASE (Ambiente do Serviço de Aplicativo)

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a>Verifique se uma máquina virtual ainda está em execução na rede virtual

Verifique se nenhuma máquina virtual está na rede virtual.

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a>Verifique se a rede virtual está presa na migração

Se a rede virtual estiver presa em um estado de migração, ela não poderá ser excluída. Execute o comando a seguir para anular a migração e, em seguida, excluir a rede virtual.

```azurepowershell
Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort
```

## <a name="next-steps"></a>Próximas etapas

- [Rede Virtual do Azure](virtual-networks-overview.md)
- [Perguntas frequentes sobre a rede virtual do Azure (Perguntas frequentes)](virtual-networks-faq.md)
