---
title: Fuso de horário de instância de gerida de base de dados SQL do Azure | Documentos da Microsoft"
description: Saiba mais sobre as especificações de fuso horário de instância gerida da base de dados SQL do Azure
services: sql-database
ms.service: sql-database
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.reviewer: ''
manager: craigg
ms.date: 04/10/2019
ms.openlocfilehash: 23314e97051da95ab164baeab6e9d089f486351a
ms.sourcegitcommit: 1a19a5845ae5d9f5752b4c905a43bf959a60eb9d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/11/2019
ms.locfileid: "59489695"
---
# <a name="time-zone-in-azure-sql-database-managed-instance-preview"></a>Fuso horário na instância gerida da base de dados do SQL do Azure (pré-visualização)

Embora utilizar Hora Universal Coordenada (UTC) é uma prática recomendada para a camada de dados de soluções na cloud, instância gerida da base de dados SQL do Azure oferece uma opção de fuso horário para satisfazer as necessidades das aplicações existentes que armazenam valores de data e hora e data da chamada e funções de tempo com um contexto implícito de um fuso horário específico.

Como o funções T-SQL [GETDATE()](https://docs.microsoft.com/sql/t-sql/functions/getdate-transact-sql) ou código CLR observar o fuso horário que definir na instância do nível. Trabalhos do SQL Agent também seguem agenda, de acordo com o fuso horário da instância.

  >[!NOTE]
  > A instância gerida é a opção de implementação apenas de base de dados do SQL do Azure que suporta a definição de fuso horário. Outras opções de implementação seguem sempre UTC.
Uso [AT TIME ZONE](https://docs.microsoft.com/sql/t-sql/queries/at-time-zone-transact-sql) no únicos e em pool bases de dados SQL se precisar de interpretam as informações de data e hora no fuso horário não UTC.

## <a name="supported-time-zones"></a>Suportado fusos horários

Um conjunto de fusos horários suportados é herdado do sistema operativo subjacente da instância gerida e está a ser atualizado regularmente para obter novas definições de fuso horário e refletir as alterações para os já existentes.

Uma lista com os nomes das zonas de tempo suportados é exposta por meio da [sys.time_zone_info](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-time-zone-info-transact-sql) vista de sistema.

## <a name="setting-time-zone"></a>Fuso horário de definição

Um fuso horário de instância gerida pode ser definido durante a criação de instância apenas. O fuso horário padrão é a hora Universal Coordenada (UTC).

  >[!NOTE]
  > Não é possível alterar o fuso horário de uma instância gerida existente.

### <a name="setting-the-time-zone-through-azure-portal"></a>Definir o fuso horário através do portal do Azure

Ao introduzir parâmetros para a nova instância, selecione um fuso horário na lista de fusos horários suportados:
  
![Definir o fuso horário durante a criação de instância](media/sql-database-managed-instance-timezone/01-setting_timezone-during-instance-creation.png)

### <a name="azure-resource-manager-template"></a>Modelo Azure Resource Manager

Especifique a propriedade timezoneId no seu [modelo do Resource Manager](https://aka.ms/sql-mi-create-arm-posh) para definir o fuso horário durante a criação de instância.

```json
"properties": {
                "administratorLogin": "[parameters('user')]",
                "administratorLoginPassword": "[parameters('pwd')]",
                "subnetId": "[parameters('subnetId')]",
                "storageSizeInGB": 256,
                "vCores": 8,
                "licenseType": "LicenseIncluded",
                "hardwareFamily": "Gen5",
                "collation": "Serbian_Cyrillic_100_CS_AS",
                "timezoneId": "Central European Standard Time"
            },

```

Lista de valores suportados para a propriedade timezoneId pode ser encontrada no final deste artigo.

Se não for especificado, será definido fuso horário UTC.

## <a name="checking-the-time-zone-of-instance"></a>A verificar o fuso horário da instância

[CURRENT_TIMEZONE](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-transact-sql) função retorna um nome a apresentar do fuso horário da instância.

## <a name="cross-feature-considerations"></a>Considerações sobre várias funcionalidades

### <a name="restore-and-import"></a>Restauro e da importação

Pode restaurar o ficheiro de cópia de segurança ou importar dados para a instância gerida de uma instância ou um servidor com as definições de fuso horário diferente. No entanto, certifique-se fazer isso com cuidado e para analisar o comportamento da aplicação e os resultados das consultas e relatórios, tal como ao transferir dados entre duas instâncias do SQL Server com as definições de fuso horário diferente.

### <a name="point-in-time-restore"></a>Restauro para um ponto anterior no tempo

Quando efetuar o restauro de ponto no tempo, o tempo de restauro para é interpretado como hora UTC para evitar qualquer ambiguidade devido ao horário de Verão e as alterações do mesmo potenciais.

### <a name="auto-failover-groups"></a>Grupos de ativação pós-falha automática

Usando o mesmo fuso horário na instância principal e secundária numa ativação pós-falha grupo não é imposto, mas é altamente recomendável.
  >[!IMPORTANT]
  > Embora haja cenários válidos para ter o fuso horário diferente na instância de geo-secundária utilizada para a leitura de escala apenas, tenha em atenção que no caso de ativação pós-falha manual ou automática para a instância secundária ele manterá seu fuso horário original.

## <a name="limitations"></a>Limitações

- Não é possível alterar o fuso horário da instância gerida existente.
- Processos externos iniciados a partir de trabalhos do SQL Agent não observam fuso horário da instância.
- Instância gerida do nativa [New-AzSqlInstance](https://docs.microsoft.com/powershell/module/az.sql/new-azsqlinstance) cmdlet do PowerShell não tempo de passagem do suporte de zona parâmetro ainda. Wrapper de PowerShell de utilização com [modelo do Resource Manager](https://aka.ms/sql-mi-create-arm-posh) em vez disso.
- Comando da CLI [az sql mi criar](https://docs.microsoft.com/cli/azure/sql/mi?view=azure-cli-latest#az-sql-mi-create) não suporta o parâmetro de fuso horário ainda.

## <a name="list-of-supported-time-zones"></a>Lista de fusos horários suportados

| **ID do fuso horário** | **Nome a apresentar do fuso horário** |
| --- | --- |
| Hora Padrão da Linha de Data | (UTC-12:00) Oeste da Linha de Data Internacional |
| UTC-11 | (UTC-11:00) Hora Universal Coordenada-11 |
| Fuso Horário das Ilhas Aleutas | (UTC-10:00) Ilhas Aleutas |
| Hora Padrão do Havai | (UTC-10:00) Havai |
| Fuso Horário das Ilhas Marquesas | (UTC-09:30) Ilhas Marquesas |
| Hora Padrão do Alasca | (UTC-09:00) Alasca |
| UTC-09 | (UTC-09:00) Hora Universal Coordenada-09 |
| Hora Padrão do Pacífico (México) | (UTC-08:00) Baja California |
| UTC-08 | (UTC-08:00) Hora Universal Coordenada-08 |
| Hora Padrão do Pacífico | (UTC-08:00) Hora do Pacífico (E.U.A. e Canadá) |
| Hora Padrão das Regiões Montanhosas dos E.U.A. | (UTC-07:00) Arizona |
| Hora Padrão das Regiões Montanhosas (México) | (UTC-07:00) Chihuahua, La Paz, Mazatlan |
| Hora Padrão das Montanhosas | (UTC-07:00) Hora das Regiões Montanhosas (E.U.A. e Canadá) |
| Hora Padrão da América Central | (UTC-06:00) América Central |
| Hora Padrão Central | (UTC-06:00) Hora Central (E.U.A. e Canadá) |
| Fuso Horário da Ilha de Páscoa | (UTC-06:00) Ilha da Páscoa |
| Hora Padrão Central (México) | (UTC-06:00) Guadalajara, Cidade do México, Monterrey |
| Hora Padrão do Canadá Central | (UTC-06:00) Saskatchewan |
| Hora Padrão da AS - Pacífico | (UTC-05:00) Bogotá, Lima, Quito, Rio Branco |
| Hora Padrão do Leste (México) | (UTC-05:00) Chetumal |
| Hora Padrão do Leste | (UTC-05:00) Hora do Leste (U.S.A. e Canadá) |
| Fuso Horário de Haiti | (UTC-05:00) Haiti |
| Fuso Horário de Cuba | (UTC-05:00) Havana |
| Hora Padrão do Leste dos E.U.A | (UTC-05:00) Indiana (Leste) |
| Ilhas Turcas e Caicos fuso horário | (UTC-05:00) Ilhas Turcas e Caicos |
| Hora Padrão do Paraguai | (UTC-04:00) Assunção |
| Hora Padrão do Atlântico | (UTC-04:00) Hora do Atlântico (Canadá) |
| Hora Padrão da Venezuela | (UTC-04:00) Caracas |
| Hora Padrão do Brasil Central | (UTC-04:00) Cuiabá |
| Hora Padrão do Oeste da AS | (UTC-04:00) Georgetown, La Paz, Manaus, São João |
| Hora Padrão do Pacífico da AS | (UTC-04:00) Santiago |
| Hora padrão da Terra Nova | (UTC-03:30) Terra Nova |
| Fuso Horário de Tocantins | (UTC-03:00) Araguaína |
| E. Hora padrão da América do Sul | (UTC-03:00) Brasília |
| Hora Padrão do Leste da AS | (UTC-03:00) Caiena, Fortaleza |
| Hora Padrão da Argentina | (UTC-03:00) Cidade de Buenos Aires |
| Hora Padrão da Gronelândia | (UTC-03:00) Gronelândia |
| Hora Padrão de Montevideu | (UTC-03:00) Montevidéu |
| Hora Padrão de Magallanes | (UTC-03:00) Punta Arenas |
| Fuso Horário de Saint Pierre | (UTC-03:00) São Pedro e Miquelão |
| Hora Padrão da Baía | (UTC-03:00) Salvador |
| UTC-02 | (UTC-02:00) Hora Universal Coordenada-02 |
| Hora Padrão do Atlântico Central | (UTC-02:00) Atlântico Central - Antigo |
| Hora Padrão dos Açores | (UTC-01:00) Açores |
| Cape Verde Standard Time | (UTC-01:00) Ilhas de Cabo Verde |
| UTC | (UTC) Hora Universal Coordenada |
| Hora Padrão de GMT | (UTC+00:00) Dublim, Edimburgo, Lisboa, Londres |
| Hora Padrão de Greenwich | (UTC+00:00) Monróvia, Reiquiavique |
| W. Hora padrão da Europa | (UTC+01:00) Amesterdão, Berlim, Berna, Roma, Estocolmo, Viena |
| Hora Padrão da Europa Central | (UTC+01:00) Belgrado, Bratislava, Budapeste, Liubliana, Praga |
| Hora Padrão de Romance | (UTC+01:00) Bruxelas, Copenhaga, Madrid, Paris |
| Hora Padrão de Marrocos | (UTC+01:00) Casablanca |
| Hora Padrão de São Tomé | (UTC+01:00) São Tomé |
| Hora Padrão da Europa Central | (UTC+01:00) Sarajevo, Skopje, Varsóvia, Zagreb |
| W. Hora padrão da África Central | (UTC+01:00) África Central Ocidental |
| Hora Padrão da Jordânia | (UTC+02:00) Amã |
| Hora Padrão GT | (UTC+02:00) Atenas, Bucareste |
| Hora Padrão do Médio Oriente | (UTC+02:00) Beirute |
| Hora Padrão do Egipto | (UTC+02:00) Cairo |
| E. Hora padrão da Europa | (UTC+02:00) Chisinau |
| Hora Padrão da Síria | (UTC+02:00) Damasco |
| Hora padrão do Oeste bancária | (UTC+02:00) Gaza, Hebrom |
| Hora Padrão da África do Sul | (UTC+02:00) Harare, Pretória |
| Hora Padrão da Finlândia | (UTC+02:00) Helsínquia, Kiev, Riga, Sófia, Tallin, Vilnius |
| Israel Standard Time | (UTC+02:00) Jerusalém |
| Hora padrão de Kaliningrado | (UTC+02:00) Kaliningrado |
| Hora Standard do Sudão | (UTC+02:00) Cartum |
| Hora Padrão da Líbia | (UTC+02:00) Trípoli |
| Hora Padrão da Namíbia | (UTC+02:00) Windhoek |
| Hora Padrão Árabe | (UTC+03:00) Bagdade |
| Hora Padrão da Turquia | (UTC+03:00) Istambul |
| Hora Padrão da Arábia Saudita | (UTC+03:00) Kuwait, Riade |
| Hora Padrão da Bielorrússia | (UTC+03:00) Minsk |
| Hora padrão da Rússia | (UTC+03:00) Moscovo, São Petersburgo |
| E. Hora padrão da África | (UTC+03:00) Nairobi |
| Hora Padrão do Irão | (UTC+03:30) Teerão |
| Hora Padrão de Abu Dhabi | (UTC+04:00) Abu Dhabi, Mascate |
| Fuso Horário de Astracã | (UTC+04:00) Astrakhan, Ulianovsk |
| Hora Padrão do Azerbaijão | (UTC+04:00) Baku |
| Fuso horário Rússia 3 | (UTC+04:00) Izhevsk, Samara |
| Hora Padrão da Maurícia | (UTC+04:00) Port Louis |
| Hora Padrão de Saratov | (UTC + 04:00) Saratov |
| Hora Padrão da Geórgia | (UTC+04:00) Tbilisi |
| Hora de Volgogrado | (UTC+04:00) Volgogrado |
| Hora Padrão do Cáucaso | (UTC+04:00) Erevan |
| Hora Padrão do Afeganistão | (UTC+04:30) Cabul |
| Hora Padrão da Ásia Oeste | (UTC+05:00) Achgabat, Tashkent |
| Hora padrão de Ecaterimburgo | (UTC+05:00) Ecaterimburgo |
| Hora Padrão do Paquistão | (UTC+05:00) Islamabade, Carachi |
| Hora Padrão da Índia | (UTC+05:30) Chennai, Calcutá, Mumbai, Nova Deli |
| Hora Padrão do Sri Lanka | (UTC+05:30) Sri Jayawardenepura |
| Hora Padrão do Nepal | (UTC+05:45) Catmandu |
| Hora Padrão da Ásia Central | (UTC+06:00) Astana |
| Hora Padrão do Bangladeche | (UTC+06:00) Daca |
| Fuso Horário de Omsk | (UTC + 06:00) Omsk |
| Hora Padrão de Myanmar | (UTC+06:30) Yangon (Rangum) |
| Hora Padrão do Sudeste Asiático | (UTC+07:00) Banguecoque, Hanói, Jacarta |
| Fuso Horário de Altai | (UTC+07:00) Barnaul, Gorno-Altaysk |
| W. Fuso horário da Mongólia | (UTC+07:00) Hovd |
| Hora padrão do Nordeste da Ásia | (UTC+07:00) Krasnoyarsk |
| N. Hora Padrão da Ásia Central | (UTC+07:00) Novosibirsk |
| Fuso Horário de Tomsk | (UTC+07:00) Tomsk |
| Hora Padrão da China | (UTC+08:00) Pequim, Chongqing, Hong Kong, Urumqi |
| Hora padrão do Nordeste da Ásia | (UTC+08:00) Irkutsk |
| Hora padrão de Singapura | (UTC+08:00) Kuala Lumpur, Singapura |
| W. Hora padrão da Austrália | (UTC+08:00) Perth |
| Hora Padrão de Taipé | (UTC+08:00) Taipé |
| Hora Padrão de Ulan Bator | (UTC+08:00) Ulan Bator |
| Fuso Horário do Centro-Oeste da Austrália | (UTC+08:45) Eucla |
| Fuso Horário de Transbaikal | (UTC+09:00) Chita |
| Hora Padrão de Tóquio | (UTC+09:00) Osaka, Sapporo, Tóquio |
| Hora Padrão da Coreia do Norte | (UTC+09:00) Pyongyang |
| Hora Padrão da Coreia | (UTC+09:00) Seul |
| Hora padrão de Yakutsk | (UTC+09:00) Yakutsk |
| CEN. Hora padrão da Austrália | (UTC+09:30) Adelaide |
| Hora padrão da Austrália Central | (UTC+09:30) Darwin |
| E. Hora padrão da Austrália | (UTC+10:00) Brisbane |
| Hora Padrão da Austrália Oriental | (UTC+10:00) Camberra, Melbourne, Sydney |
| Hora Padrão do Pacífico Oeste | (UTC+10:00) Guame, Port Moresby |
| Hora Padrão da Tasmânia | (UTC+10:00) Hobart |
| Hora padrão de Vladivostoque | (UTC+10:00) Vladivostoque |
| Fuso Horário da Ilha de Lord Howe | (UTC+10:30) Ilha de Lord Howe |
| Fuso Horário de Bougainville | (UTC+11:00) Ilha de Bougainville |
| Fuso horário Rússia 10 | (UTC+11:00) Chokurdakh |
| Hora Padrão de Magadã | (UTC+11:00) Magadã |
| Fuso Horário de Norfolk | (UTC+11:00) Ilha Norfolk |
| Fuso Horário de Sacalina | (UTC+11:00) Sakhalin |
| Hora Padrão do Pacífico Central | (UTC+11:00) Ilhas Salomão, Nova Caledónia |
| Fuso horário Rússia 11 | (UTC+12:00) Anadyr, Petropavlovsk-Kamchatsky |
| Hora Padrão da Nova Zelândia | (UTC+12:00) Auckland, Wellington |
| UTC+12 | (UTC+12:00) Hora Universal Coordenada+12 |
| Hora Padrão das Fiji | (UTC+12:00) Fiji |
| Hora Padrão de Kamchatka | (UTC+12:00) Petropavlovsk-Kamchatsky - Antigo |
| Fuso Horário das Ilhas Chatham | (UTC+12:45) Ilhas Chatham |
| UTC+13 | (UTC + 13:00) Hora Universal Coordenada+13 |
| Hora Padrão de Tonga | (UTC+13:00) Nucualofa |
| Hora Padrão de Samoa | (UTC+13:00) Samoa |
| Hora Padrão Ilhas Espórades Equatoriais | (UTC+14:00) Ilha de Kiritimati |

## <a name="see-also"></a>Consulte também

- [CURRENT_TIMEZONE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-transact-sql)
- [AT TIME ZONE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/at-time-zone-transact-sql)
- [sys.time_zone_info (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-time-zone-info-transact-sql)