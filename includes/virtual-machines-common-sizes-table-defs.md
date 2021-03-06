---
title: arquivo de inclusão
description: arquivo de inclusão
services: virtual-machines
author: jonbeck7
ms.service: virtual-machines
ms.topic: include
ms.date: 03/09/2018
ms.author: azcspmt;jonbeck;cynthn
ms.custom: include file
ms.openlocfilehash: 63c53a9b95e27486d7d6944c28f8fb085b1bc6ca
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "74279196"
---
<!-- Not used for Ls-series -->

## <a name="size-table-definitions"></a>Definições da tabela de tamanhos

- A capacidade de armazenamento é mostrada em unidades de GiB ou de 1024^3 bytes. Quando você compara os discos medidos em GB (1000 ^ 3 bytes) para os discos medidos em GiB (1024 ^ 3), lembre-se de que os números de capacidade fornecidos em GiB podem parecer menores. Por exemplo, 1023 GiB = 1098,4 GB.
- A taxa de transferência do disco é medida em IOPS (operações de entrada/saída por segundo) e em MBps, em que MBps = 10^6 bytes/s.
- Os discos de dados podem operar nos modos em cache ou não armazenado em cache. Para a operação do disco de dados armazenados em cache, o modo de cache do host é definido como **ReadOnly** ou **ReadWrite**.  Para as operação do disco de dados não armazenados em cache, o modo de cache do host é definido como **Nenhum**.
- Se você quiser obter o melhor desempenho para suas VMs, você deve limitar o número de discos de dados para dois discos por vCPU.
- **Largura de banda de rede esperada** é a largura de banda agregada máxima alocada por tipo de VM em todas as NICs para todos os destinos. Para obter mais informações, consulte [largura de banda de rede da máquina virtual](../articles/virtual-network/virtual-machine-network-throughput.md).

  Os limites superiores não são garantidos. Os limites oferecem orientação para selecionar o tipo de VM correto para o aplicativo pretendido. O desempenho real da rede dependerá de vários fatores, incluindo o congestionamento da rede, cargas de aplicativos e configurações de rede. Para obter informações sobre como otimizar a taxa de transferência de rede, consulte [otimizar a taxa de transferência de rede para máquinas virtuais do Azure](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Para obter o desempenho de rede esperado no Linux ou no Windows, talvez seja necessário selecionar uma versão específica ou otimizar sua VM. Para obter mais informações, consulte [NTTTCP (largura de banda/teste de taxa de transferência)](../articles/virtual-network/virtual-network-bandwidth-testing.md).



