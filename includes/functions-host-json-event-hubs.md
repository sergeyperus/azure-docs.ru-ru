---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/04/2018
ms.author: glenga
ms.openlocfilehash: 8f3a58d3a7470867ab23249bbd645289e010ad89
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "95997322"
---
### <a name="functions-2x-and-higher"></a>Функции 2.x и более поздних версий

```json
{
    "version": "2.0",
    "extensions": {
        "eventHubs": {
            "batchCheckpointFrequency": 5,
            "eventProcessorOptions": {
                "maxBatchSize": 256,
                "prefetchCount": 512
            }
        }
    }
}  
```

|Свойство  |По умолчанию | Описание |
|---------|---------|---------|
|maxBatchSize|10|Максимальное число событий, получаемых в цикле получения.|
|prefetchCount|300|Счетчик предварительной выборки по умолчанию, используемый базовым `EventProcessorHost`. Минимальное допустимое значение — 10.|
|batchCheckpointFrequency|1|Количество пакетов событий, которые необходимо обработать перед созданием контрольной точки курсора EventHub.|

> [!NOTE]
> См. сведения о [файле host.json в Функциях Azure версии 2.x и выше](../articles/azure-functions/functions-host-json.md).

### <a name="functions-1x"></a>Функции 1.x

```json
{
    "eventHub": {
      "maxBatchSize": 64,
      "prefetchCount": 256,
      "batchCheckpointFrequency": 1
    }
}
```

|Свойство  |По умолчанию | Описание |
|---------|---------|---------| 
|maxBatchSize|64|Максимальное число событий, получаемых в цикле получения.|
|prefetchCount|Недоступно|Предварительная выборка по умолчанию, используемая базовым `EventProcessorHost`.| 
|batchCheckpointFrequency|1|Количество пакетов событий, которые необходимо обработать перед созданием контрольной точки курсора EventHub.| 

> [!NOTE]
> См. сведения о [файле host.json в Функциях Azure версии 1.x](../articles/azure-functions/functions-host-json-v1.md).
