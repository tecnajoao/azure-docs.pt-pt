---
title: Ligar um Raspberry Pi a sua aplicação do Azure IoT Central (C#) | Documentos da Microsoft
description: Como desenvolvedor de dispositivo, como ligar um Raspberry Pi a sua aplicação do Azure IoT Central utilizando C#.
author: viv-liu
ms.author: viviali
ms.date: 04/05/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 341b4d23664900cdf1f9a209df663ad4e6e96fe4
ms.sourcegitcommit: ef20235daa0eb98a468576899b590c0bc1a38394
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59426363"
---
# <a name="connect-a-raspberry-pi-to-your-azure-iot-central-application-c"></a>Ligar um Raspberry Pi a sua aplicação do Azure IoT Central (c#)

[!INCLUDE [howto-raspberrypi-selector](../../includes/iot-central-howto-raspberrypi-selector.md)]

Este artigo descreve como, como um desenvolvedor de dispositivo, para ligar um Raspberry Pi a sua aplicação do Microsoft Azure IoT Central, utilizando a linguagem de programação c#.

## <a name="before-you-begin"></a>Antes de começar

Para concluir os passos neste artigo, tem os seguintes componentes:

* Uma aplicação do Azure IoT Central, criada a partir da **Devkits exemplo** o modelo de aplicativo. Para obter mais informações, veja [criar um início rápido da aplicação](quick-deploy-iot-central.md).
* Um dispositivo de Raspberry Pi com o sistema de operativo Raspbian. O Raspberry Pi tem de ser capaz de ligar à internet. Para obter mais informações, consulte [configurar o seu Raspberry Pi](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/3).

## <a name="sample-devkits-application"></a>**Exemplo Devkits** aplicação

Um aplicativo criado a partir da **Devkits de exemplo** inclui o modelo de aplicativo um **Raspberry Pi** modelo de dispositivo com as seguintes características:

- Telemetria, que inclui as seguintes medidas que recolherá o dispositivo:
  - Humidade
  - Temperatura
  - Pressão
  - Magnetômetro (X, Y, Z)
  - Acelerômetro (X, Y, Z)
  - Por giroscópio (X, Y, Z)
- Definições
  - Tensão
  - Atual
  - Ventoinha velocidade
  - Botão de alternar do Runtime de integração.
- Propriedades
  - Morrem número propriedade do dispositivo
  - Propriedade de cloud de localização

Para todos os detalhes da configuração do modelo de dispositivo, consulte a [detalhes do modelo de dispositivo do Raspberry Pi](#raspberry-pi-device-template-details).

## <a name="add-a-real-device"></a>Adicionar um dispositivo real

Na aplicação do Azure IoT Central, adicionar um dispositivo real a partir da **Raspberry Pi** modelo do dispositivo. Tome nota do dispositivo detalhes de ligação (**ID de âmbito**, **ID do dispositivo**, e **chave primária**). Para obter mais informações, consulte [adicionar um dispositivo real à sua aplicação do Azure IoT Central](tutorial-add-device.md).

### <a name="create-your-net-application"></a>Criar a sua aplicação .NET

Criar e testar a aplicação de dispositivo no seu computador desktop.

Para concluir os passos seguintes, pode utilizar o Visual Studio Code. Para obter mais informações, consulte [trabalhando com c#](https://code.visualstudio.com/docs/languages/csharp).

> [!NOTE]
> Se preferir, pode concluir os passos seguintes com um editor de código diferente.

1. Para inicializar o seu projeto do .NET e adicione os pacotes de NuGet necessários, execute os seguintes comandos:

   ```cmd/sh
   mkdir pisample
   cd pisample
   dotnet new console
   dotnet add package Microsoft.Azure.Devices.Client
   dotnet restore
   ```

1. Abra o `pisample` pasta no Visual Studio Code. Em seguida, abra a **pisample.csproj** arquivo de projeto. Adicionar o `<RuntimeIdentifiers>` marca mostrada no seguinte fragmento:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <RuntimeIdentifiers>win-arm;linux-arm</RuntimeIdentifiers>
      </PropertyGroup>
      <ItemGroup>
        <PackageReference Include="Microsoft.Azure.Devices.Client" Version="1.19.0" />
      </ItemGroup>
    </Project>
    ```

    > [!NOTE]
    > Sua **Microsoft.Azure.Devices.Client** número de versão de pacote pode ser maior do que aquele mostrado.

1. Save **pisample.csproj**. Se o Visual Studio Code pede-lhe para executar o comando restore, escolha **restaurar**.

1. Open **Program.cs** e substitua os conteúdos com o código a seguir:

    ```csharp
    using System;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    using Newtonsoft.Json;

    namespace pisample
    {
      class Program
      {
        static string DeviceConnectionString = "{your device connection string}";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();
        static CancellationTokenSource cts;
        static double baseTemperature = 60;
        static double basePressure = 500;
        static double baseHumidity = 50;
        static void Main(string[] args)
        {
          Console.WriteLine("Raspberry Pi Azure IoT Central example");

          try
          {
            InitClient();
            SendDeviceProperties();

            cts = new CancellationTokenSource();
            SendTelemetryAsync(cts.Token);

            Console.WriteLine("Wait for settings update...");
            Client.SetDesiredPropertyUpdateCallbackAsync(HandleSettingChanged, null).Wait();
            Console.ReadKey();
            cts.Cancel();
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        public static void InitClient()
        {
          try
          {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        public static async void SendDeviceProperties()
        {
          try
          {
            Console.WriteLine("Sending device properties:");
            Random random = new Random();
            TwinCollection telemetryConfig = new TwinCollection();
            reportedProperties["dieNumber"] = random.Next(1, 6);
            Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

            await Client.UpdateReportedPropertiesAsync(reportedProperties);
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        private static async void SendTelemetryAsync(CancellationToken token)
        {
          try
          {
            Random rand = new Random();

            while (true)
            {
              double currentTemperature = baseTemperature + rand.NextDouble() * 20;
              double currentPressure = basePressure + rand.NextDouble() * 100;
              double currentHumidity = baseHumidity + rand.NextDouble() * 20;

              var telemetryDataPoint = new
              {
                humidity = currentHumidity,
                pressure = currentPressure,
                temp = currentTemperature
              };
              var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
              var message = new Message(Encoding.ASCII.GetBytes(messageString));

              token.ThrowIfCancellationRequested();
              await Client.SendEventAsync(message);

              Console.WriteLine("{0} > Sending telemetry: {1}", DateTime.Now, messageString);

              await Task.Delay(1000);
            }
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Intentional shutdown: {0}", ex.Message);
          }
        }

        private static async Task HandleSettingChanged(TwinCollection desiredProperties, object userContext)
        {
          try
          {
            Console.WriteLine("Received settings change...");
            Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

            string setting = "fanSpeed";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "setVoltage";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "setCurrent";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "activateIR";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            await Client.UpdateReportedPropertiesAsync(reportedProperties);
          }

          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        private static void AcknowledgeSettingChange(TwinCollection desiredProperties, string setting)
        {
          reportedProperties[setting] = new
          {
            value = desiredProperties[setting]["value"],
            status = "completed",
            desiredVersion = desiredProperties["$version"],
            message = "Processed"
          };
        }
      }
    }
    ```

    > [!NOTE]
    > Atualizar o marcador de posição `{your device connection string}` no próximo passo.

## <a name="run-your-net-application"></a>Execute a sua aplicação .NET

Adicione a cadeia de ligação específicos do dispositivo para o código para o dispositivo autenticar com o Azure IoT Central. Siga estas instruções para [gerar a cadeia de ligação do dispositivo](howto-generate-connection-string.md) utilizando o **ID de âmbito**, **ID de dispositivo**, e **chave primária** é feita uma Observe de anteriormente.

1. Substitua `{your device connection string}` no **Program.cs** ficheiro com a cadeia de ligação que gerou.

1. Execute o seguinte comando no seu ambiente de linha de comandos:

   ```cmd/sh
   dotnet restore
   dotnet publish -r linux-arm
   ```

1. Copiar o `pisample\bin\Debug\netcoreapp2.1\linux-arm\publish` pasta para o seu dispositivo Raspberry Pi. Pode utilizar o **scp** comandos para copiar os ficheiros, por exemplo:

    ```cmd/sh
    scp -r publish pi@192.168.0.40:publish
    ```

    Para obter mais informações, consulte [acesso remoto de Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/).

1. Inicie sessão no seu dispositivo Raspberry Pi e execute os seguintes comandos numa shell:

    ```cmd/sh
    sudo apt-get update
    sudo apt-get install libc6 libcurl3 libgcc1 libgssapi-krb5-2 liblttng-ust0 libstdc++6 libunwind8 libuuid1 zlib1g
    ```

1. No seu Raspberry Pi, execute os seguintes comandos:

    ```cmd/sh
    cd publish
    chmod 777 pisample
    ./pisample
    ```

    ![Programa começa](./media/howto-connect-raspberry-pi-csharp/device_begin.png)

1. Na aplicação do Azure IoT Central, pode ver como o código que executa o Raspberry Pi interage com o aplicativo:

   * Sobre o **medidas** página para o seu dispositivo real, pode ver a telemetria.
   * Sobre o **propriedades** página, pode ver o valor do comunicado **morrem número** propriedade.
   * Sobre o **definições** página, pode alterar várias definições no Raspberry Pi, por exemplo, a velocidade de tensão e fan.

     Captura de ecrã seguinte mostra o Raspberry Pi a receber a alteração da definição:

     ![Raspberry Pi recebe a alteração da definição](./media/howto-connect-raspberry-pi-csharp/device_switch.png)

## <a name="raspberry-pi-device-template-details"></a>Detalhes do modelo do raspberry Pi dispositivo

Um aplicativo criado a partir da **Devkits de exemplo** inclui o modelo de aplicativo um **Raspberry Pi** modelo de dispositivo com as seguintes características:

### <a name="telemetry-measurements"></a>Medições de telemetria

| Nome do campo     | Unidades  | Mínimo | Máximo | Casas decimais |
| -------------- | ------ | ------- | ------- | -------------- |
| humidade       | %      | 0       | 100     | 0              |
| temp           | °C     | -40     | 120     | 0              |
| pressure       | hPa    | 260     | 1260    | 0              |
| magnetometerX  | mgauss | -1000   | 1000    | 0              |
| magnetometerY  | mgauss | -1000   | 1000    | 0              |
| magnetometerZ  | mgauss | -1000   | 1000    | 0              |
| accelerometerX | mg     | -2000   | 2000    | 0              |
| accelerometerY | mg     | -2000   | 2000    | 0              |
| accelerometerZ | mg     | -2000   | 2000    | 0              |
| gyroscopeX     | mdps   | -2000   | 2000    | 0              |
| gyroscopeY     | mdps   | -2000   | 2000    | 0              |
| gyroscopeZ     | mdps   | -2000   | 2000    | 0              |

### <a name="settings"></a>Definições

Definições de numérico

| Nome a apresentar | Nome do campo | Unidades | Casas decimais | Mínimo | Máximo | Inicial |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| Tensão      | setVoltage | Volts | 0              | 0       | 240     | 0       |
| Atual      | setCurrent | AMPS  | 0              | 0       | 100     | 0       |
| Ventoinha velocidade    | fanSpeed   | RPM   | 0              | 0       | 1000    | 0       |

Ativar/desativar definições

| Nome a apresentar | Nome do campo | No texto | Desativar o texto | Inicial |
| ------------ | ---------- | ------- | -------- | ------- |
| IR           | activateIR | ON      | OFF      | Desativado     |

### <a name="properties"></a>Propriedades

| Type            | Nome a apresentar | Nome do campo | Tipo de dados |
| --------------- | ------------ | ---------- | --------- |
| Propriedade do dispositivo | Morrem número   | dieNumber  | número    |
| Texto            | Localização     | localização   | N/A       |

## <a name="next-steps"></a>Passos Seguintes

Agora que aprendeu como ligar um Raspberry Pi a sua aplicação do Azure IoT Central, aqui estão os passos sugeridos seguintes:

* [Ligar uma aplicação de cliente genérica do node. js para o Azure IoT Central](howto-connect-nodejs.md)
