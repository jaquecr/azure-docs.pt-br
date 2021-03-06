---
title: Atualizar a extensão do observador de rede para a versão mais recente
description: Saiba como atualizar a extensão do observador de rede do Azure para a versão mais recente.
services: virtual-machines-windows
documentationcenter: ''
author: damendo
manager: balar
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.topic: article
ms.workload: infrastructure-services
ms.date: 09/23/2020
ms.author: damendo
ms.openlocfilehash: 23520a0249e22b3f81c7f7c598ef10d8c3acb550
ms.sourcegitcommit: 693df7d78dfd5393a28bf1508e3e7487e2132293
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92900193"
---
# <a name="update-the-network-watcher-extension-to-the-latest-version"></a>Atualizar a extensão do observador de rede para a versão mais recente

## <a name="overview"></a>Visão geral

O [observador de rede do Azure](../../network-watcher/network-watcher-monitoring-overview.md) é um serviço de monitoramento, diagnóstico e análise de desempenho de rede que monitora as redes do Azure. A extensão da máquina virtual (VM) do agente do observador de rede é um requisito para capturar o tráfego de rede sob demanda e usar outras funcionalidades avançadas em VMs do Azure. A extensão do observador de rede é usada por recursos como o monitor de conexão, o monitor de conexão (versão prévia), a solução de problemas de conexão e a captura de pacotes.

## <a name="prerequisites"></a>Pré-requisitos

Este artigo pressupõe que você tenha a extensão do observador de rede instalada em sua VM.

## <a name="latest-version"></a>Última versão

A versão mais recente da extensão do observador de rede é atualmente `1.4.1654.1` .

## <a name="update-your-extension"></a>Atualizar sua extensão

Para atualizar sua extensão, você precisa saber a versão da extensão.

### <a name="check-your-extension-version"></a>Verifique sua versão de extensão

Você pode verificar a versão da extensão usando o portal do Azure, o CLI do Azure ou o PowerShell.

#### <a name="usetheazureportal"></a>Usar o portal do Azure

1. Vá para o painel **extensões** de sua VM no portal do Azure.
1. Selecione a extensão **AzureNetworkWatcher** para ver o painel de detalhes.
1. Localize o número de versão no campo **versão** .  

#### <a name="use-the-azure-cli"></a>Usar a CLI do Azure

Execute o seguinte comando em um prompt de CLI do Azure:

```azurecli
az vm get-instance-view --resource-group  "SampleRG" --name "Sample-VM"
```
Localize **"AzureNetworkWatcherExtension"** na saída e identifique o número de versão do campo *"TypeHandlerVersion"* na saída.  Observação: as informações sobre a extensão aparecem várias vezes na saída JSON. Examine o bloco "extensões" e você verá o número de versão completo da extensão. 

Você verá algo semelhante ao seguinte: ![ CLI do Azure captura de tela](./media/network-watcher/azure-cli-screenshot.png)

#### <a name="usepowershell"></a>Usar o PowerShell

Execute os seguintes comandos em um prompt do PowerShell:

```powershell
Get-AzVM -ResourceGroupName "SampleRG" -Name "Sample-VM" -Status
```
Localize a extensão do observador de rede do Azure na saída e identifique o número de versão do campo *"TypeHandlerVersion"* na saída.   

Você verá algo parecido com o seguinte: ![ captura de tela do PowerShell](./media/network-watcher/powershell-screenshot.png)

### <a name="update-your-extension"></a>Atualizar sua extensão

Se sua versão for anterior à `1.4.1654.1` , que é a versão mais recente atual, atualize sua extensão usando qualquer uma das opções a seguir.

#### <a name="option-1-use-powershell"></a>Opção 1: usar o PowerShell

Execute os seguintes comandos:

```powershell
#Linux command
Set-AzVMExtension -ResourceGroupName "myResourceGroup1" -Location "WestUS" -VMName "myVM1" -Name "AzureNetworkWatcherExtension" -Publisher "Microsoft.Azure.NetworkWatcher" -Type "NetworkWatcherAgentLinux"

#Windows command
Set-AzVMExtension -ResourceGroupName "myResourceGroup1" -Location "WestUS" -VMName "myVM1" -Name "AzureNetworkWatcherExtension" -Publisher "Microsoft.Azure.NetworkWatcher" -Type "NetworkWatcherAgentWindows"
```

Se isso não funcionar. Remova e instale a extensão novamente, usando as etapas abaixo. Isso adicionará automaticamente a versão mais recente.

Removendo a extensão 

```powershell
#Same command for Linux and Windows
Remove-AzVMExtension -ResourceGroupName "SampleRG" -VMName "Sample-VM" -Name "AzureNetworkWatcherExtension"
``` 

Instalando a extensão novamente

```powershell
#Linux command
Set-AzVMExtension -ResourceGroupName "SampleRG" -Location "centralus" -VMName "Sample-VM" -Name "AzureNetworkWatcherExtension" -Publisher "Microsoft.Azure.NetworkWatcher" -Type "NetworkWatcherAgentLinux" -typeHandlerVersion "1.4"

#Windows command
Set-AzVMExtension -ResourceGroupName "SampleRG" -Location "centralus" -VMName "Sample-VM" -Name "AzureNetworkWatcherExtension" -Publisher "Microsoft.Azure.NetworkWatcher" -Type "NetworkWatcherAgentWindows" -typeHandlerVersion "1.4"
```

#### <a name="option-2-use-the-azure-cli"></a>Opção 2: usar o CLI do Azure

Forçar uma atualização.

```azurecli
#Linux command
az vm extension set --resource-group "myResourceGroup1" --vm-name "myVM1" --name "NetworkWatcherAgentLinux" --publisher "Microsoft.Azure.NetworkWatcher" --force-update

#Windows command
az vm extension set --resource-group "myResourceGroup1" --vm-name "myVM1" --name "NetworkWatcherAgentWindows" --publisher "Microsoft.Azure.NetworkWatcher" --force-update
```

Se isso não funcionar, remova e instale a extensão novamente e siga estas etapas para adicionar automaticamente a versão mais recente.

Remova a extensão.

```azurecli
#Same for Linux and Windows
az vm extension delete --resource-group "myResourceGroup1" --vm-name "myVM1" -n "AzureNetworkWatcherExtension"

```

Instale a extensão novamente.

```azurecli
#Linux command
az vm extension set --resource-group "DALANDEMO" --vm-name "Linux-01" --name "NetworkWatcherAgentLinux" --publisher "Microsoft.Azure.NetworkWatcher"

#Windows command
az vm extension set --resource-group "DALANDEMO" --vm-name "Linux-01" --name "NetworkWatcherAgentWindows" --publisher "Microsoft.Azure.NetworkWatcher"

```

#### <a name="option-3-reboot-your-vms"></a>Opção 3: reinicialize suas VMs

Se você tiver a atualização automática definida como true para a extensão do observador de rede, reinicialize a instalação da VM para a extensão mais recente.

## <a name="support"></a>Suporte

Se precisar de mais ajuda a qualquer momento neste artigo, consulte a documentação de extensão do observador de rede para [Linux](./network-watcher-linux.md) ou [Windows](./network-watcher-windows.md). Você também pode contatar os especialistas do Azure nos [fóruns do Azure e do Stack Overflow do MSDN](https://azure.microsoft.com/support/forums/). Como alternativa, arquivo de um incidente de suporte do Azure. Vá para o [site de suporte do Azure](https://azure.microsoft.com/support/options/)e selecione **obter suporte** . Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](https://azure.microsoft.com/support/faq/).
