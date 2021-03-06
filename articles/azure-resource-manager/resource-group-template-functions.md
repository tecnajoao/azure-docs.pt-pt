---
title: Funções de modelo do Resource Manager | Documentos da Microsoft
description: Descreve as funções para utilizar num modelo do Azure Resource Manager para recuperar valores, trabalhar com cadeias de caracteres e numéricos e obter informações de implementação.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/08/2019
ms.author: tomfitz
ms.openlocfilehash: b5a1f12a877008a3ce2ff7bd9635b9ed47b379f7
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59280320"
---
# <a name="azure-resource-manager-template-functions"></a>Funções de modelo do Azure Resource Manager
Este artigo descreve todas as funções que pode usar num modelo Azure Resource Manager. Para obter informações sobre como utilizar as funções no seu modelo, consulte [sintaxe do modelo](resource-group-authoring-templates.md#syntax).

Para criar suas próprias funções, consulte [funções definidas pelo utilizador](resource-group-authoring-templates.md#functions).

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="json" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a>Funções de matriz e objeto
Resource Manager fornece várias funções para trabalhar com matrizes e objetos.

* [array](resource-group-template-functions-array.md#array)
* [Coalesce](resource-group-template-functions-array.md#coalesce)
* [concat](resource-group-template-functions-array.md#concat)
* [contém](resource-group-template-functions-array.md#contains)
* [createArray](resource-group-template-functions-array.md#createarray)
* [Vazio](resource-group-template-functions-array.md#empty)
* [primeiro](resource-group-template-functions-array.md#first)
* [intersecção](resource-group-template-functions-array.md#intersection)
* [json](resource-group-template-functions-array.md#json)
* [última](resource-group-template-functions-array.md#last)
* [Comprimento](resource-group-template-functions-array.md#length)
* [min.](resource-group-template-functions-array.md#min)
* [máx.](resource-group-template-functions-array.md#max)
* [Intervalo](resource-group-template-functions-array.md#range)
* [ignorar](resource-group-template-functions-array.md#skip)
* [tirar](resource-group-template-functions-array.md#take)
* [União](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a>Funções de comparação
Resource Manager fornece várias funções para fazer comparações nos seus modelos.

* [é igual a](resource-group-template-functions-comparison.md#equals)
* [menos](resource-group-template-functions-comparison.md#less)
* [lessOrEquals](resource-group-template-functions-comparison.md#lessorequals)
* [maior](resource-group-template-functions-comparison.md#greater)
* [greaterOrEquals](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a>Funções de valor de implementação
O Resource Manager proporciona as seguintes funções para obter valores de secções do modelo e os valores relacionados com a implementação:

* [implementação](resource-group-template-functions-deployment.md#deployment)
* [parâmetros](resource-group-template-functions-deployment.md#parameters)
* [Variáveis](resource-group-template-functions-deployment.md#variables)

<a id="and" />
<a id="bool" />
<a id="if" />
<a id="not" />
<a id="or" />

## <a name="logical-functions"></a>Funções lógicas
O Resource Manager fornece as seguintes funções para trabalhar com condições lógicas:

* [e](resource-group-template-functions-logical.md#and)
* [booleano](resource-group-template-functions-logical.md#bool)
* [IF](resource-group-template-functions-logical.md#if)
* [não](resource-group-template-functions-logical.md#not)
* [ou](resource-group-template-functions-logical.md#or)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="numeric-functions"></a>Funções numéricas
O Resource Manager fornece as seguintes funções para trabalhar com números inteiros:

* [adicionar](resource-group-template-functions-numeric.md#add)
* [copyIndex](resource-group-template-functions-numeric.md#copyindex)
* [div](resource-group-template-functions-numeric.md#div)
* [float](resource-group-template-functions-numeric.md#float)
* [int](resource-group-template-functions-numeric.md#int)
* [min.](resource-group-template-functions-numeric.md#min)
* [máx.](resource-group-template-functions-numeric.md#max)
* [mod](resource-group-template-functions-numeric.md#mod)
* [mul](resource-group-template-functions-numeric.md#mul)
* [sub](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a>Funções de recursos
O Resource Manager proporciona as seguintes funções para obter valores do recurso:

* [listAccountSas](resource-group-template-functions-resource.md#list)
* [listKeys](resource-group-template-functions-resource.md#listkeys)
* [listSecrets](resource-group-template-functions-resource.md#list)
* [list*](resource-group-template-functions-resource.md#list)
* [Fornecedores](resource-group-template-functions-resource.md#providers)
* [Referência](resource-group-template-functions-resource.md#reference)
* [resourceGroup](resource-group-template-functions-resource.md#resourcegroup)
* [resourceId](resource-group-template-functions-resource.md#resourceid)
* [subscrição](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="guid" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a>Funções de cadeia
O Resource Manager fornece as seguintes funções para trabalhar com cadeias de caracteres:

* [base64](resource-group-template-functions-string.md#base64)
* [base64ToJson](resource-group-template-functions-string.md#base64tojson)
* [base64ToString](resource-group-template-functions-string.md#base64tostring)
* [concat](resource-group-template-functions-string.md#concat)
* [contém](resource-group-template-functions-string.md#contains)
* [dataUri](resource-group-template-functions-string.md#datauri)
* [dataUriToString](resource-group-template-functions-string.md#datauritostring)
* [Vazio](resource-group-template-functions-string.md#empty)
* [endsWith](resource-group-template-functions-string.md#endswith)
* [primeiro](resource-group-template-functions-string.md#first)
* [Formato](resource-group-template-functions-string.md#format)
* [GUID](resource-group-template-functions-string.md#guid)
* [indexOf](resource-group-template-functions-string.md#indexof)
* [última](resource-group-template-functions-string.md#last)
* [lastIndexOf](resource-group-template-functions-string.md#lastindexof)
* [Comprimento](resource-group-template-functions-string.md#length)
* [newGuid](resource-group-template-functions-string.md#newguid)
* [padLeft](resource-group-template-functions-string.md#padleft)
* [substituir](resource-group-template-functions-string.md#replace)
* [ignorar](resource-group-template-functions-string.md#skip)
* [dividir](resource-group-template-functions-string.md#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](resource-group-template-functions-string.md#string)
* [subcadeia](resource-group-template-functions-string.md#substring)
* [tirar](resource-group-template-functions-string.md#take)
* [toLower](resource-group-template-functions-string.md#tolower)
* [toUpper](resource-group-template-functions-string.md#toupper)
* [Cortar](resource-group-template-functions-string.md#trim)
* [uniqueString](resource-group-template-functions-string.md#uniquestring)
* [uri](resource-group-template-functions-string.md#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)
* [utcNow](resource-group-template-functions-string.md#utcnow)

## <a name="next-steps"></a>Passos Seguintes
* Para obter uma descrição das secções num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md)
* Intercalar vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md)
* Para fazer a iteração de um número especificado de vezes ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md)
* Para ver como implementar o modelo que criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md)
