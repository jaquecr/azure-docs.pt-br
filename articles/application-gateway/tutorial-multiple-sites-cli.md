---
title: Hospedar vários sites da Web usando a CLI
titleSuffix: Azure Application Gateway
description: Saiba como criar um gateway de aplicativo que hospeda vários sites web usando a CLI do Azure.
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: how-to
ms.date: 11/13/2019
ms.author: victorh
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: 5e72a98ddd5219662c8850326b4f43b25e545177
ms.sourcegitcommit: 99955130348f9d2db7d4fb5032fad89dad3185e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93348144"
---
# <a name="create-an-application-gateway-that-hosts-multiple-web-sites-using-the-azure-cli"></a>Criar um gateway de aplicativo que hospeda vários sites usando a CLI do Azure

Você pode usar a CLI do Azure para configurar [a hospedagem de vários sites da Web](multiple-site-overview.md) ao criar um [gateway de aplicativo](overview.md). Neste artigo, você define pools de endereço back-end usando conjuntos de dimensionamento de máquinas virtuais. Em seguida, você configurará ouvintes e regras com base em domínios que possui para garantir que o tráfego da Web chegue aos servidores apropriados nos pools. Este artigo pressupõe que você possui vários domínios e usa exemplos de *www \. contoso.com* e *www \. fabrikam.com*.

Neste artigo, você aprenderá como:

* Configurar a rede
* Criar um Gateway de Aplicativo
* Criar ouvintes de back-end
* Criar regras de roteamento
* Criar conjuntos de dimensionamento de máquinas virtuais com pools de back-end
* Criar um registro CNAME no seu domínio

:::image type="content" source="./media/tutorial-multiple-sites-cli/scenario.png" alt-text="Gateway de Aplicativo multissite":::

Se preferir, você poderá concluir este procedimento usando o [Azure PowerShell](tutorial-multiple-sites-powershell.md).

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este artigo exigirá que você esteja executando o CLI do Azure versão 2.0.4 ou posterior. Para saber qual é a versão, execute `az --version`. Se você precisa instalar ou atualizar, consulte [Instalar a CLI do Azure](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Criar um grupo de recursos usando [az group create](/cli/azure/group).

O exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAG* no local *eastus*.

```azurecli-interactive
az group create --name myResourceGroupAG --location eastus
```

## <a name="create-network-resources"></a>Criar recursos da rede

Criar a rede virtual e a sub-rede denominada *myAGSubnet* usando [az network vnet create](/cli/azure/network/vnet). Você pode adicionar a sub-rede que é necessária para os servidores de back-end usando [az network vnet subnet create](/cli/azure/network/vnet/subnet). Crie o endereço IP público denominado *myAGPublicIPAddress* usando [az network public-ip create](/cli/azure/network/public-ip).

```azurecli-interactive
az network vnet create \
  --name myVNet \
  --resource-group myResourceGroupAG \
  --location eastus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name myAGSubnet \
  --subnet-prefix 10.0.1.0/24

az network vnet subnet create \
  --name myBackendSubnet \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --address-prefix 10.0.2.0/24

az network public-ip create \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --allocation-method Static \
  --sku Standard
```

## <a name="create-the-application-gateway"></a>Criar o gateway de aplicativo

Você pode usar [az network application-gateway creat](/cli/azure/network/application-gateway#az-network-application-gateway-create) para criar o gateway do aplicativo. Quando você cria um gateway de aplicativo usando a CLI do Azure, você pode especificar informações de configuração, como configurações de HTTP, sku e capacidade. O gateway de aplicativo é atribuído a *myAGSubnet* e *myAGPublicIPAddress* que você criou anteriormente. 

```azurecli-interactive
az network application-gateway create \
  --name myAppGateway \
  --location eastus \
  --resource-group myResourceGroupAG \
  --vnet-name myVNet \
  --subnet myAGsubnet \
  --capacity 2 \
  --sku Standard_v2 \
  --http-settings-cookie-based-affinity Disabled \
  --frontend-port 80 \
  --http-settings-port 80 \
  --http-settings-protocol Http \
  --public-ip-address myAGPublicIPAddress
```

O gateway de aplicativo pode demorar vários minutos para ser criado. Depois de criar o gateway de aplicativo, você pode ver esses novos recursos:

- *appGatewayBackendPool* - Um gateway de aplicativo deve ter pelo menos um pool de endereços de back-end.
- *appGatewayBackendHttpSettings* - Especifica que a porta 80 e um protocolo HTTP são usados para comunicação.
- *appGatewayHttpListener* - O ouvinte padrão associado ao *appGatewayBackendPool*.
- *appGatewayFrontendIP* - Atribui *myAGPublicIPAddress* ao *appGatewayHttpListener*.
- *rule1* - A regra padrão de roteamento que está associada ao *appGatewayHttpListener*.

### <a name="add-the-backend-pools"></a>Adicionar os pools de back-end

Adicione os pools de back-end que são necessários para conter os servidores de back-end usando [AZ Network Application-Gateway Address-pool Create](/cli/azure/network/application-gateway/address-pool#az-network-application-gateway-address-pool-create)
```azurecli-interactive
az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name contosoPool

az network application-gateway address-pool create \
  --gateway-name myAppGateway \
  --resource-group myResourceGroupAG \
  --name fabrikamPool
```

### <a name="add-listeners"></a>Adicionar ouvintes

Adicione ouvintes que são necessários para rotear o tráfego usando [AZ Network Application-Gateway http-Listener Create](/cli/azure/network/application-gateway/http-listener#az-network-application-gateway-http-listener-create).

>[!NOTE]
> Com a SKU do gateway de aplicativo ou do WAF v2, você também pode configurar até 5 nomes de host por ouvinte e pode usar caracteres curinga no nome do host. Consulte [nomes de host curinga no ouvinte](multiple-site-overview.md#wildcard-host-names-in-listener-preview) para obter mais informações.
>Para usar vários nomes de host e caracteres curinga em um ouvinte usando CLI do Azure, você deve usar `--host-names` em vez de `--host-name` . Com nomes de host, você pode mencionar até cinco nomes de host como valores separados por espaços. Por exemplo, `--host-names "*.contoso.com *.fabrikam.com"`

```azurecli-interactive
az network application-gateway http-listener create \
  --name contosoListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.contoso.com

az network application-gateway http-listener create \
  --name fabrikamListener \
  --frontend-ip appGatewayFrontendIP \
  --frontend-port appGatewayFrontendPort \
  --resource-group myResourceGroupAG \
  --gateway-name myAppGateway \
  --host-name www.fabrikam.com   
  ```

### <a name="add-routing-rules"></a>Adicionar regras de redirecionamento

As regras são processadas na ordem em que estão listadas. O tráfego é direcionado usando a primeira regra que corresponde, independentemente da especificidade. Por exemplo, se você tiver uma regra usando um ouvinte básico e outra usando um ouvinte multissite, ambas na mesma porta, a regra com o ouvinte multissite deverá ser listada antes daquela com o ouvinte básico, para que a função multissite funcione conforme esperado. 

Neste exemplo, você cria duas novas regras e exclui a regra padrão criada quando você implantou o gateway de aplicativo. Você pode adicionar a regra usando [az network application-gateway rule create](/cli/azure/network/application-gateway/rule#az-network-application-gateway-rule-create).

```azurecli-interactive
az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name contosoRule \
  --resource-group myResourceGroupAG \
  --http-listener contosoListener \
  --rule-type Basic \
  --address-pool contosoPool

az network application-gateway rule create \
  --gateway-name myAppGateway \
  --name fabrikamRule \
  --resource-group myResourceGroupAG \
  --http-listener fabrikamListener \
  --rule-type Basic \
  --address-pool fabrikamPool

az network application-gateway rule delete \
  --gateway-name myAppGateway \
  --name rule1 \
  --resource-group myResourceGroupAG
```

## <a name="create-virtual-machine-scale-sets"></a>Criar conjuntos de dimensionamento de máquinas virtuais

Neste exemplo, você cria três conjuntos de dimensionamento de máquinas virtuais que oferecem suporte a três pools de back-end no gateway de aplicativo. Os conjuntos de dimensionamento que você cria são denominados *myvmss1* , *myvmss2* , e *myvmss3*. Cada conjunto de dimensionamento contém duas instâncias de máquina virtual no qual você instala o IIS.

```azurecli-interactive
for i in `seq 1 2`; do

  if [ $i -eq 1 ]
  then
    poolName="contosoPool"
  fi

  if [ $i -eq 2 ]
  then
    poolName="fabrikamPool"
  fi

  az vmss create \
    --name myvmss$i \
    --resource-group myResourceGroupAG \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password Azure123456! \
    --instance-count 2 \
    --vnet-name myVNet \
    --subnet myBackendSubnet \
    --vm-sku Standard_DS2 \
    --upgrade-policy-mode Automatic \
    --app-gateway myAppGateway \
    --backend-pool-name $poolName
done
```

### <a name="install-nginx"></a>Instalar o NGINX

```azurecli-interactive
for i in `seq 1 2`; do

  az vmss extension set \
    --publisher Microsoft.Azure.Extensions \
    --version 2.0 \
    --name CustomScript \
    --resource-group myResourceGroupAG \
    --vmss-name myvmss$i \
    --settings '{ "fileUris": ["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/install_nginx.sh"],
  "commandToExecute": "./install_nginx.sh" }'

done
```

## <a name="create-a-cname-record-in-your-domain"></a>Criar um registro CNAME no seu domínio

Depois de criar o gateway de aplicativo com seu endereço IP público, é possível obter o endereço DNS e usá-lo para criar um registro CNAME em seu domínio. Use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show) para obter o endereço DNS do gateway de aplicativo. Copie o valor de *fqdn* em DNSSettings e use-o como o valor do registro CNAME a ser criado. 

```azurecli-interactive
az network public-ip show \
  --resource-group myResourceGroupAG \
  --name myAGPublicIPAddress \
  --query [dnsSettings.fqdn] \
  --output tsv
```

O uso de registros A não é recomendado porque o VIP pode ser alterado quando o gateway de aplicativo é reiniciado.

## <a name="test-the-application-gateway"></a>Testar o gateway de aplicativo

Digite seu nome de domínio na barra de endereços do navegador. Por exemplo, \/http://www.contoso.com.

![Testar o site contoso no gateway do aplicativo](./media/tutorial-multiple-sites-cli/application-gateway-nginxtest1.png)

Altere o endereço para seu outro domínio e você verá algo parecido com o exemplo a seguir:

![Testar site do fabrikam no gateway de aplicativo](./media/tutorial-multiple-sites-cli/application-gateway-nginxtest2.png)

## <a name="clean-up-resources"></a>Limpar os recursos

Quando não for mais necessário, remova o grupo de recursos, o gateway de aplicativo e todos os recursos relacionados.

```azurecli-interactive
az group delete --name myResourceGroupAG
```

## <a name="next-steps"></a>Próximas etapas

[Criar um gateway de aplicativo com regras de roteamento baseadas em caminhos de URL](./tutorial-url-route-cli.md)
