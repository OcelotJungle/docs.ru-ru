---
title: Средства Azure для Visual Studio 2015
description: Получите средства для использования библиотек Azure для .NET в Visual Studio 2015.
ms.date: 10/19/2017
ms.custom: azure-sdk-dotnet
ms.openlocfilehash: a29709d56f2debe04d49ee4eafdc27acd4ca480f
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2020
ms.locfileid: "81433154"
---
# <a name="azure-tools-for-visual-studio-2015"></a>Средства Azure для Visual Studio 2015

Самый быстрый и простой способ установить **пакет Azure SDK для Visual Studio 2015** и **пакет SDK для Service Fabric и средства для Visual Studio 2015** — воспользоваться [установщиком веб-платформы](https://www.microsoft.com/web/downloads/platform.aspx). Установщик веб-платформы Майкрософт — это бесплатное средство, которое упрощает скачивание, установку и обновление некоторых компонентов веб-платформы Майкрософт, в том числе средств Azure для Visual Studio 2015. Эти пакеты SDK можно также скачать на [странице загрузок Azure](https://azure.microsoft.com/downloads/) и установить в качестве отдельных компонентов.

## <a name="using-the-web-platform-installer"></a>Использование установщика веб-платформы

1. Скачайте и запустите этот [начальный загрузчик для установщика веб-платформы](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).

2. Начальный загрузчик установит установщик веб-платформы (при необходимости) и автоматически поместит последние версии **пакета Azure SDK для Visual Studio 2015** и **пакета SDK для Service Fabric и средств для Visual Studio 2015** в список *Устанавливаемые элементы*. Нажмите кнопку **Установить**.

    ![Установщик веб-платформы](../media/sdk/vs2015-install/webpi.png)

3. На следующем экране нажмите кнопку **Я принимаю**. Установщик веб-платформы начнет скачивание и установку выбранных компонентов.

4. Когда установка завершится, отобразится экран подтверждения. Нажмите кнопку **Готово**. Теперь можете закрыть установщик веб-платформы.

## <a name="verifying-the-installation"></a>Проверка установки

1. В Visual Studio 2015 щелкните меню **Сервис** и выберите пункт **Расширения и обновления...** .

2. Отображаемый список будет содержать несколько средств Azure, например **средства службы приложений Microsoft Azure**, **подключенную службу хранилища Microsoft Azure** и **средства Service Fabric**.

    ![Расширения и обновления](../media/sdk/vs2015-install/ext-tools.png)
