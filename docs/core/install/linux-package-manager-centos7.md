---
title: Установка .NET Core на CentOS 7 — диспетчер пакетов — .NET Core
description: Используйте диспетчер пакетов для установки пакета SDK для .NET Core и среды выполнения на CentOS 7.
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: f8c4115b9d85edc36809f0daed5f6825149c8411
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645400"
---
# <a name="centos-7-package-manager---install-net-core"></a>Диспетчер пакетов CentOS 7 — установка .NET Core

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

Эта статья описывает, как использовать диспетчер пакетов для установки .NET Core на CentOS 7.

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="add-microsoft-repository-key-and-feed"></a>Добавление ключа и веб-канала репозитория Майкрософт

Перед установкой .NET нужно сделать следующее:

- добавить ключ подписывания пакета Майкрософт в список доверенных ключей;
- добавить репозиторий в диспетчер пакетов;
- установить необходимые зависимости.

Данную операцию достаточно выполнить один раз для каждого компьютера.

Откройте терминал и выполните приведенную ниже команду.

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

## <a name="install-the-net-core-sdk"></a>Установка пакета SDK для .NET Core

Обновите продукты, доступные для установки, а затем установите пакет SDK для .NET Core. В терминале выполните приведенную ниже команду.

```bash
sudo yum install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a>Установка среды выполнения ASP.NET Core

Обновите продукты, доступные для установки, а затем установите среду выполнения ASP.NET. В терминале выполните приведенную ниже команду.

```bash
sudo yum install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a>Установка среды выполнения .NET Core

Обновите продукты, доступные для установки, а затем установите среду выполнения .NET Core. В терминале выполните приведенную ниже команду.

```bash
sudo yum install dotnet-runtime-3.1
```

## <a name="how-to-install-other-versions"></a>Установка других версий

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Устранение неполадок диспетчера пакетов

В этом разделе описаны распространенные ошибки, которые могут возникнуть при использовании диспетчера пакетов для установки .NET Core.

### <a name="failed-to-fetch"></a>Ошибка получения

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]
