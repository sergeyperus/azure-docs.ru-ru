---
author: ggailey777
ms.author: glenga
ms.date: 7/24/2019
ms.topic: include
ms.service: azure-functions
ms.openlocfilehash: 0159ceb6e5d6d64a7a9bda383396607e4ce05b84
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96020377"
---
#### <a name="built-in-log-streaming"></a>Встроенная потоковая передача журналов

Параметр `logstream` позволяет получать журналы потоковой передачи конкретного приложения-функции, работающего в Azure, как показано в следующем примере:

```bash
func azure functionapp logstream <FunctionAppName>
```

>[!NOTE]
>Встроенная потоковая передача журналов пока что не поддерживается в Core Tools для приложений-функций, выполняемых в Linux в рамках плана "Потребление". Чтобы просматривать журналы почти в реальном времени, для таких планов размещения необходимо использовать Live Metrics Stream.

#### <a name="live-metrics-stream"></a>Динамический поток метрик

Вы можете просмотреть журналы [Live Metrics Stream](../articles/azure-monitor/app/live-stream.md) для своего приложения-функции в новом окне браузера. Для этого включите параметр `--browser`, как показано в следующем примере:

```bash
func azure functionapp logstream <FunctionAppName> --browser
```
