---
title: Conectar o código do dispositivo C de exemplo do IoT Plug and Play ao Hub IoT | Microsoft Docs
description: Crie e execute um código do dispositivo de exemplo do IoT Plug and Play no Linux ou no Windows que se conecta a um hub IoT. Use a ferramenta Azure IoT Explorer para exibir as informações enviadas pelo dispositivo ao hub.
author: ericmitt
ms.author: ericmitt
ms.date: 07/14/2020
ms.topic: quickstart
ms.service: iot-pnp
services: iot-pnp
ms.openlocfilehash: e490171fd533783aab9fd44798a9c81c55faf89f
ms.sourcegitcommit: 2e72661f4853cd42bb4f0b2ded4271b22dc10a52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92047923"
---
# <a name="quickstart-connect-a-sample-iot-plug-and-play-device-application-running-on-linux-or-windows-to-iot-hub-c"></a>Início Rápido: Conectar um aplicativo de exemplo do dispositivo do IoT Plug and Play no Linux ou no Windows ao Hub IoT (C)

[!INCLUDE [iot-pnp-quickstarts-device-selector.md](../../includes/iot-pnp-quickstarts-device-selector.md)]

Este guia de início rápido mostra como criar um aplicativo de exemplo de dispositivo IoT Plug and Play, conectá-lo ao hub IoT e usar a ferramenta Azure IoT Explorer para exibir a telemetria que ele envia. O aplicativo de exemplo é gravado em C e está incluído no SDK do dispositivo IoT do Azure para C. Um construtor de soluções pode usar a ferramenta do Azure IoT Explorer para compreender as funcionalidades de um dispositivo IoT Plug and Play sem a necessidade de ver nenhum código de dispositivo.

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [iot-pnp-prerequisites](../../includes/iot-pnp-prerequisites.md)]

Você pode executar este guia de início rápido no Linux ou no Windows. Os comandos do shell neste guia de início rápido seguem a convenção do Linux para os separadores de caminho '`/`', se você estiver acompanhando no Windows, não deixe de trocar esses separadores por '`\`'.

Os pré-requisitos diferem por sistema operacional:

### <a name="linux"></a>Linux

Este guia de início rápido pressupõe que você esteja usando o Ubuntu Linux. As etapas deste início rápido foram testadas com o Ubuntu 18.04.

Para concluir este início rápido no Linux, instale o seguinte software em um ambiente Linux local:

Instale o **GCC**, o **Git**, o **CMake** e todas as dependências exigidas usando o comando `apt-get`:

```sh
sudo apt-get update
sudo apt-get install -y git cmake build-essential curl libcurl4-openssl-dev libssl-dev uuid-dev
```

Verifique se a versão do `cmake` é superior a **2.8.12** e se a versão do **GCC** é superior a **4.4.7**.

```sh
cmake --version
gcc --version
```

### <a name="windows"></a>Windows

Para concluir este início rápido no Windows, instale o seguinte software em um ambiente do Windows local:

* [Visual Studio (Community, Professional ou Enterprise)](https://visualstudio.microsoft.com/downloads/) – inclua a carga de trabalho **Desenvolvimento para Desktop com C++** ao [instalar](/cpp/build/vscpp-step-0-installation?preserve-view=true&view=vs-2019) o Visual Studio.
* [Git](https://git-scm.com/download/).
* [CMake](https://cmake.org/download/).

## <a name="download-the-code"></a>Baixar o código

Neste início rápido, você preparará um ambiente de desenvolvimento que pode ser usado para clonar e compilar o SDK do dispositivo Hub IoT do Azure para C.

Abra um prompt de comando no diretório de sua escolha. Execute o seguinte comando para clonar o repositório GitHub dos [SDKs de C e Bibliotecas do IoT do Azure](https://github.com/Azure/azure-iot-sdk-c) nesta localização:

```cmd\bash
git clone https://github.com/Azure/azure-iot-sdk-c.git
cd azure-iot-sdk-c
git submodule update --init
```

Essa operação deve demorar alguns minutos.

## <a name="build-the-code"></a>Compilar o código

Use o SDK do dispositivo para criar o código de exemplo incluído:

1. Crie um subdiretório _cmake_ na pasta raiz do SDK do dispositivo e navegue até essa pasta:

    ```cmd\bash
    cd azure-iot-sdk-c
    mkdir cmake
    cd cmake
    ```

1. Execute os seguintes comandos para criar o SDK e os exemplos:

    ```cmd\bash
    cmake -Duse_prov_client=ON -Dhsm_type_symm_key=ON -Drun_e2e_tests=OFF ..
    cmake --build .
    ```

> [!TIP]
> No Windows, você pode abrir a solução gerada pelo comando `cmake` no Visual Studio 2019. Abra o arquivo de projeto *azure_iot_sdks.sln* no diretório _cmake_ e defina o projeto **pnp_simple_thermostat** como o projeto de inicialização na solução. Agora você pode compilar o exemplo no Visual Studio e executá-lo no modo de depuração.

## <a name="run-the-device-sample"></a>Executar o exemplo de dispositivo

[!INCLUDE [iot-pnp-environment](../../includes/iot-pnp-environment.md)]

Para saber mais sobre a configuração do exemplo, confira o [leiame de exemplo](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/samples/pnp/readme.md).

Para executar um aplicativo de exemplo no SDK que simula um dispositivo IoT Plug and Play que envia telemetria ao Hub IoT:

Na pasta _cmake_, navegue até a pasta que contém o arquivo executável e execute-o:

```bash
# Bash
cd iothub_client/samples/pnp/pnp_simple_thermostat/
./pnp_simple_thermostat
```

```cmd
REM Windows
cd iothub_client\samples\pnp\pnp_simple_thermostat\Debug
.\pnp_simple_thermostat.exe
```

> [!TIP]
> Para rastrear a execução de código no Visual Studio no Windows, adicione um ponto de interrupção à função `main` no arquivo _pnp_simple_thermostat.c_.

Agora, o dispositivo está pronto para receber comandos e atualizações de propriedade e começou a enviar dados telemétricos para o hub. Mantenha o exemplo em execução enquanto você conclui as próximas etapas.

## <a name="use-azure-iot-explorer-to-validate-the-code"></a>Usar o Azure IoT Explorer para validar o código

Após iniciar o exemplo de cliente do dispositivo, use a ferramenta Azure IoT Explorer para verificar se ele está funcionando.

[!INCLUDE [iot-pnp-iot-explorer.md](../../includes/iot-pnp-iot-explorer.md)]

## <a name="review-the-code"></a>Examine o código

Este exemplo implementa um dispositivo termostato simples do IoT Plug and Play. O modelo que esse exemplo implementa não usa os [componentes](concepts-components.md) do IoT Plug and Play. O [arquivo de modelo de DTDL para o dispositivo de termostato](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/samples/Thermostat.json) define a telemetria, as propriedades e os comandos que o dispositivo implementa.

O código do dispositivo usa a função padrão para se conectar ao seu hub IoT:

```c
deviceHandle = IoTHubDeviceClient_CreateFromConnectionString(connectionString, MQTT_Protocol)
```

O dispositivo envia a ID de modelo do modelo de DTDL que ele implementa na solicitação de conexão. Um dispositivo que envia uma ID de modelo é um dispositivo IoT Plug and Play:

```c
static const char g_ModelId[] = "dtmi:com:example:Thermostat;1";

...

IoTHubDeviceClient_SetOption(deviceHandle, OPTION_MODEL_ID, modelId)
```

O código que atualiza propriedades, manipula comandos e envia telemetria é idêntico ao código de um dispositivo que não usa as convenções do IoT Plug and Play.

O código usa a biblioteca Parson para analisar objetos JSON nos conteúdos enviados do seu hub IoT:

```c
// JSON parser
#include "parson.h"
```

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você aprendeu a conectar um dispositivo IoT Plug and Play a um Hub IoT. Para saber mais sobre como criar uma solução que interage com os dispositivos IoT Plug and Play, confira:

> [!div class="nextstepaction"]
> [Instruções: Conectar-se a um dispositivo e interagir com ele](./quickstart-service-node.md)