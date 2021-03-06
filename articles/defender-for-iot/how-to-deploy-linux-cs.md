---
title: Установка & развертывание агента C# для Linux
description: Сведения об установке и развертывании защитника безопасности на основе C# для IoT на платформе Linux
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.devlang: na
ms.custom: devx-track-csharp
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/09/2020
ms.author: mlottner
ms.openlocfilehash: 48737831440a1402b6974955b4da61a4216b011f
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "90939479"
---
# <a name="deploy-defender-for-iot-c-based-security-agent-for-linux"></a>Развертывание агента безопасности на основе C# для Azure IoT для Linux

В этом руководство объясняется, как установить и развернуть защитник безопасности на основе C# для IoT на платформе Linux.

Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Установка
> * Проверка развертывания
> * Удаление агента
> * Диагностика

## <a name="prerequisites"></a>Предварительные требования

Сведения о других платформах и разновидностях агентов см. в разделе Выбор подходящего [агента безопасности](how-to-deploy-agent.md).

1. Для развертывания агента безопасности требуются права локального администратора на компьютере, используемом для установки.

1. [Создайте модуль безопасности](quickstart-create-security-twin.md) для устройства.

## <a name="installation"></a>Установка

Чтобы развернуть агент безопасности, выполните следующие действия.

1. Скачайте последнюю версию на компьютер с сайта [GitHub](https://aka.ms/iot-security-github-cs).

1. Извлеките содержимое пакета и перейдите в папку _/Install_ .

1. Добавьте права на выполнение к **скрипту InstallSecurityAgent**, выполнив следующую команду `chmod +x InstallSecurityAgent.sh`.

1. Затем выполните следующую команду с **правами root**:

   ```
   ./InstallSecurityAgent.sh -i -aui <authentication identity>  -aum <authentication method> -f <file path> -hn <host name>  -di <device id> -cl <certificate location kind>
   ```

   Дополнительные сведения о параметрах проверки подлинности см. [в разделе Настройка проверки подлинности](concept-security-agent-authentication-methods.md).

Сценарий выполняет следующие действия:

- Установка необходимых компонентов.

- Добавляет пользователя службы (с отключенным интерактивным входом).

- Устанавливает агент в качестве **управляющей** программы. предполагает, что устройство использует **систему** для классической модели развертывания.

- Настраивает параметры **sudo** , чтобы разрешить агенту выполнять определенные задачи в качестве привилегированных.

- Настройка агента с предоставленными параметрами проверки подлинности.

Для получения дополнительной справки запустите скрипт с параметром –help: `./InstallSecurityAgent.sh --help`.

### <a name="uninstall-the-agent"></a>Удаление агента

Чтобы удалить агент, запустите скрипт с параметром –u: `./InstallSecurityAgent.sh -u`.

> [!NOTE]
> Удаление не приводит к удалению всех ранее отсутствующих необходимых компонентов, которые были установлены во время установки.

## <a name="troubleshooting"></a>Устранение неполадок

1. Проверьте состояние развертывания, выполнив следующую команду:

    `systemctl status ASCIoTAgent.service`

1. Включите ведение журналов.
   Если агент не запускается, включите ведение журнала, чтобы просмотреть дополнительные сведения.

   Чтобы включить ведение журнала:

   1. Откройте файл конфигурации для редактирования в любом редакторе Linux:

        `vi /var/ASCIoTAgent/General.config`

   1. Измените следующие значения:

      ```
      <add key="logLevel" value="Debug"/>
      <add key="fileLogLevel" value="Debug"/>
      <add key="diagnosticVerbosityLevel" value="Some" />
      <add key="logFilePath" value="IotAgentLog.log"/>
      ```

       Значение **logFilePath** настраивается.

       > [!NOTE]
       > Мы рекомендуем **отключить** ведение журнала после устранения неполадок. Если оставить ведение журнала **включенным**, размер файла журнала и использование данных увеличится.

   1. Перезапустите агент, выполнив команду:

       `systemctl restart ASCIoTAgent.service`

   1. Просмотрите дополнительные сведения о сбое в файле журнала.

       Расположение файла журнала: `/var/ASCIoTAgent/IotAgentLog.log`.

       Измените путь к расположению файла в соответствии с именем, выбранным для значения **logFilePath** на шаге 2.

## <a name="next-steps"></a>Дальнейшие шаги

- Ознакомьтесь с [обзором](overview.md) службы "защитник для Интернета вещей"
- Дополнительные сведения о защитнике для [архитектуры](architecture.md) IOT
- Включите [службу](quickstart-onboard-iot-hub.md).
- Ознакомьтесь с [вопросами и](resources-frequently-asked-questions.md) ответами
- Ознакомьтесь со сведениями об [оповещениях](concept-security-alerts.md).
