---
title: Команда dotnet new
description: Команда dotnet new создает проекты .NET Core на основе указанного шаблона.
ms.date: 04/10/2020
ms.openlocfilehash: 9a68baafa7ac3e6ad2fdc8f1c6e8621d6e15f1ff
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506861"
---
# <a name="dotnet-new"></a>dotnet new

**Эта статья относится к следующему.** ✔️ SDK для .NET Core 2.0 и более поздних версий

## <a name="name"></a>name

`dotnet new` - создает проект, файл конфигурации или решений на основе указанного шаблона.

## <a name="synopsis"></a>Краткий обзор

```dotnetcli
dotnet new <TEMPLATE> [--dry-run] [--force] [-i|--install {PATH|NUGET_ID}]
    [-lang|--language {C#|F#|VB}] [-n|--name <OUTPUT_NAME>]
    [--nuget-source <SOURCE>] [-o|--output <OUTPUT_DIRECTORY>]
    [-u|--uninstall] [--update-apply] [--update-check] [Template options]

dotnet new <TEMPLATE> [-l|--list] [--type <TYPE>]

dotnet new -h|--help
```

## <a name="description"></a>Описание

Команда `dotnet new` создает проект .NET Core или другие артефакты на основе шаблона.

Она вызывает [подсистему шаблонов](https://github.com/dotnet/templating), чтобы создать артефакты на диске на основе заданных параметров и шаблона.

### <a name="implicit-restore"></a>Неявное восстановление

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

## <a name="arguments"></a>Аргументы

- **`TEMPLATE`**

  Шаблон для создания экземпляров при вызове команды. Каждый шаблон может иметь отдельные параметры, доступные для передачи. Дополнительные сведения см. в разделе [Параметры шаблона](#template-options).

  Вы можете запустить `dotnet new --list` или `dotnet new -l`, чтобы просмотреть список всех установленных шаблонов. Если значение `TEMPLATE` не совпадает в точности с текстом в столбце **Шаблоны** или **Короткое имя** из возвращаемой таблицы, для этих двух столбцов выполняется поиск совпадений в подстроках.

  Начиная с пакета SDK для .NET Core 3.0, интерфейс командной строки выполняет поиск шаблонов в NuGet.org при вызове команды `dotnet new` в следующих случаях:

  - если CLI не может найти совпадение шаблона при вызове `dotnet new`, даже частичное;
  - если доступна более новая версия шаблона. В этом случае проект или артефакт создается, но CLI предупреждает об обновленной версии шаблона.

  В следующей таблице показаны шаблоны, которые устанавливаются с пакетом SDK для .NET Core. Язык по умолчанию для шаблона указан внутри квадратных скобок. Нажмите на ссылку с коротким названием, чтобы увидеть конкретные параметры шаблона.

| Шаблоны                                    | короткое имя;                      | Язык     | Tags                                  | Введенный |
|----------------------------------------------|---------------------------------|--------------|---------------------------------------|------------|
| Консольное приложение                          | [Консоль](#console)             | [C#], F#, VB | Общее/консоль                        | 1.0        |
| Библиотека классов                                | [classlib](#classlib)           | [C#], F#, VB | Общее/библиотека                        | 1.0        |
| Приложение WPF                              | [wpf](#wpf)                     | [C#]         | Общее/WPF                            | 3.0        |
| Библиотека классов WPF                            | [wpflib](#wpf)                  | [C#]         | Общее/WPF                            | 3.0        |
| Библиотека настраиваемых элементов управления WPF                   | [wpfcustomcontrollib](#wpf)     | [C#]         | Общее/WPF                            | 3.0        |
| Библиотека пользовательских элементов управления WPF                     | [wpfusercontrollib](#wpf)       | [C#]         | Общее/WPF                            | 3.0        |
| Приложение Windows Forms (WinForms)         | [winforms](#winforms)           | [C#]         | Общее (WinForms)                       | 3.0        |
| Библиотека классов для Windows Forms (WinForms)       | [winformslib](#winforms)        | [C#]         | Общее (WinForms)                       | 3.0        |
| Служба Worker Service                               | [рабочая роль](#web-others)           | [C#]         | Общее/Рабочая роль/Веб                     | 3.0        |
| Проект модульного теста                            | [mstest](#test)                 | [C#], F#, VB | Тест/MSTest                           | 1.0        |
| Тестовый проект NUnit 3                         | [nunit](#nunit)                  | [C#], F#, VB | Тест/NUnit                            | 2.1.400    |
| Элемент теста NUnit 3                            | `nunit-test`                    | [C#], F#, VB | Тест/NUnit                            | 2.2        |
| Тестовый проект xUnit                           | [xunit](#test)                  | [C#], F#, VB | Тест/xUnit                            | 1.0        |
| Компонент Razor                              | `razorcomponent`                | [C#]         | Веб/ASP.NET                           | 3.0        |
| Страница Razor                                   | [page](#page)                   | [C#]         | Веб/ASP.NET                           | 2.0        |
| MVC ViewImports                              | [viewimports](#namespace)       | [C#]         | Веб/ASP.NET                           | 2.0        |
| MVC ViewStart                                | `viewstart`                     | [C#]         | Веб/ASP.NET                           | 2.0        |
| Серверное приложение Blazor                            | [blazorserver](#blazorserver)   | [C#]         | Веб/Blazor                            | 3.0        |
| Пустой ASP.NET Core                           | [web](#web)                     | [C#], F#     | Веб/пусто                             | 1.0        |
| Веб-приложение ASP.NET Core (Model-View-Controller) | [mvc](#web-options)             | [C#], F#     | Веб/MVC                               | 1.0        |
| Веб-приложение ASP.NET Core                         | [webapp, razor](#web-options)   | [C#]         | Веб/MVC и Razor Pages                   | 2.2, 2.0   |
| ASP.NET Core с Angular                    | [angular](#spa)                 | [C#]         | MVC/Веб/SPA                           | 2.0        |
| ASP.NET Core с React.js                   | [react](#spa)                   | [C#]         | MVC/Веб/SPA                           | 2.0        |
| ASP.NET Core с React.js и Redux         | [reactredux](#reactredux)       | [C#]         | MVC/Веб/SPA                           | 2.0        |
| Библиотека классов Razor                          | [razorclasslib](#razorclasslib) | [C#]         | Веб/Razor/Библиотека/Библиотека классов Razor | 2.1        |
| Веб-API ASP.NET Core                         | [webapi](#webapi)               | [C#], F#     | Веб/веб-API                            | 1.0        |
| Служба ASP.NET Core gRPC                    | [grpc](#web-others)             | [C#]         | Веб/gRPC                              | 3.0        |
| Файл dotnet gitignore                        | `gitignore`                     |              | Config                                | 3.0        |
| Файл global.json                             | [globaljson](#globaljson)       |              | Config                                | 2.0        |
| Конфигурация NuGet                                 | `nugetconfig`                   |              | Config                                | 1.0        |
| Локальное средство файла манифеста dotnet              | `tool-manifest`                 |              | Config                                | 3.0        |
| Файл веб-конфигурации                                   | `webconfig`                     |              | Config                                | 1.0        |
| Файл решения                                | `sln`                           |              | Решение                              | 1.0        |
| Файл буфера протокола                         | [proto](#namespace)             |              | Веб/gRPC                              | 3.0        |

## <a name="options"></a>Параметры

- **`--dry-run`**

  Отображает сводку того, что произойдет, если выполнить команду и это приведет к созданию шаблона. Доступно начиная с пакета SDK для .NET Core 2.2.

- **`--force`**

  Принудительное создание содержимого, даже если при этом изменяются существующие файлы. Это необходимо, когда выбранный шаблон переопределяет существующие файлы в выходном каталоге.

- **`-h|--help`**

  Распечатывает справку для команды. Его можно вызвать для самой команды `dotnet new` или для любого шаблона. Например, `dotnet new mvc --help`.

- **`-i|--install <PATH|NUGET_ID>`**

  Устанавливает пакет шаблона из указанного пути `PATH` или по указанному идентификатору `NUGET_ID`. Если вы хотите установить предварительную версию пакета шаблонов, необходимо указать версию в формате `<package-name>::<package-version>`. По умолчанию `dotnet new` передает \* для версии, что указывает на последнюю стабильную версию пакета. См. пример в разделе [Примеры](#examples).
  
  Если при выполнении этой команды версия шаблона уже была установлена, шаблон будет обновлен до указанной версии или до последней стабильной версии, если версию не указано.

  Сведения о создании пользовательских шаблонов см. в статье [Пользовательские шаблоны для команды dotnet new](custom-templates.md).

- **`-l|--list`**

  Перечисляет шаблоны с указанным именем. Если имя не указано, перечисляются все шаблоны.

- **`-lang|--language {C#|F#|VB}`**

  Язык создаваемого шаблона. Допустимый язык зависит от шаблона (см. значения по умолчанию в разделе об [аргументах](#arguments)). Не является допустимым для некоторых шаблонов.

  > [!NOTE]
  > Некоторые оболочки интерпретируют `#` как специальный символ. В этих случаях заключите значение языкового параметра в кавычки. Например, `dotnet new console -lang "F#"`.

- **`-n|--name <OUTPUT_NAME>`**

  Имя создаваемых выходных данных. Если имя не указано, используется имя текущего каталога.

- **`--nuget-source <SOURCE>`**

  Задает источник пакетов NuGet для использования во время установки. Доступно начиная с пакета SDK для .NET Core 2.1.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  Расположение, в котором размещаются созданные выходные данные. Значением по умолчанию является текущий каталог.

- **`--type <TYPE>`**

  Фильтрует шаблоны по доступным типам. Предопределенные значения: `project`, `item` и `other`.

- **`-u|--uninstall [PATH|NUGET_ID]`**

  Удаляет пакет шаблона из указанного пути `PATH` или по указанному идентификатору `NUGET_ID`. Если значение `<PATH|NUGET_ID>` не указано, отображаются все установленные пакеты шаблонов и связанные с ними шаблоны. Не указывайте номер версии, если задаете `NUGET_ID`.

  Если вы не указываете параметр в этой опции, команда перечисляет установленные шаблоны и подробные сведения о них.

  > [!NOTE]
  > Чтобы удалить шаблон с помощью `PATH`, вам необходимо указать полный путь. Например, *C:/Users/\<ПОЛЬЗОВАТЕЛЬ>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* будет работать, а *./GarciaSoftware.ConsoleTemplate.CSharp* — нет.
  > Путь к шаблону не должен содержать конечную косую черту закрытия каталога.

- **`--update-apply`**

  Проверяет наличие обновлений для установленных в настоящее время пакетов шаблонов и устанавливает их. Доступно, начиная с пакета SDK для .NET Core 3.0.

- **`--update-check`**

  Проверяет наличие обновлений для установленных в настоящее время пакетов шаблонов. Доступно, начиная с пакета SDK для .NET Core 3.0.

## <a name="template-options"></a>Параметры шаблона

Каждый шаблон проекта может содержать дополнительные доступные параметры. Основные шаблоны имеют следующие дополнительные параметры:

### <a name="console"></a>console

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Доступно, начиная с пакета SDK для .NET Core 3.0.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`--langVersion <VERSION_NUMBER>`**

  Задает свойство `LangVersion` в созданном файле проекта. Например, вам требуется `--langVersion 7.3`, чтобы использовать C# 7.3. Не поддерживается для F#. Доступно начиная с пакета SDK для .NET Core 2.2.

  Список версий C# по умолчанию см. в разделе [Значения по умолчанию](../../csharp/language-reference/configure-language-version.md#defaults).

- **`--no-restore`**

  Если указано — во время создания проекта не выполняется неявное восстановление. Доступно начиная с пакета SDK для .NET Core 2.2.

***

### <a name="classlib"></a>classlib

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Значения: `netcoreapp<version>` для создания библиотеки классов .NET Core или `netstandard<version>` для создания стандартной библиотеки классов .NET. Значение по умолчанию — `netstandard2.0`.

- **`--langVersion <VERSION_NUMBER>`**

  Задает свойство `LangVersion` в созданном файле проекта. Например, вам требуется `--langVersion 7.3`, чтобы использовать C# 7.3. Не поддерживается для F#. Доступно начиная с пакета SDK для .NET Core 2.2.

  Список версий C# по умолчанию см. в разделе [Значения по умолчанию](../../csharp/language-reference/configure-language-version.md#defaults).

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="wpf-wpflib-wpfcustomcontrollib-wpfusercontrollib"></a><a name="wpf"></a> wpf, wpflib, wpfcustomcontrollib, wpfusercontrollib

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Значение по умолчанию — `netcoreapp3.1`. Доступно, начиная с пакета SDK для .NET Core 3.1.

- **`--langVersion <VERSION_NUMBER>`**

  Задает свойство `LangVersion` в созданном файле проекта. Например, вам требуется `--langVersion 7.3`, чтобы использовать C# 7.3.

  Список версий C# по умолчанию см. в разделе [Значения по умолчанию](../../csharp/language-reference/configure-language-version.md#defaults).

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="winforms-winformslib"></a><a name="winforms"></a> winforms, winformslib

- **`--langVersion <VERSION_NUMBER>`**

  Задает свойство `LangVersion` в созданном файле проекта. Например, вам требуется `--langVersion 7.3`, чтобы использовать C# 7.3.

  Список версий C# по умолчанию см. в разделе [Значения по умолчанию](../../csharp/language-reference/configure-language-version.md#defaults).

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="worker-grpc"></a><a name="web-others"></a> worker, grpc

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Значение по умолчанию — `netcoreapp3.1`. Доступно, начиная с пакета SDK для .NET Core 3.1.

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="mstest-xunit"></a><a name="test"></a>тmstest, xunit

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Параметр доступен, начиная с пакета SDK для .NET Core 3.0.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`-p|--enable-pack`**

  Включает упаковку проекта с помощью команды [dotnet pack](dotnet-pack.md).

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="nunit"></a>nunit

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md).

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.2         | `netcoreapp2.2` |
  | 2.1         | `netcoreapp2.1` |

- **`-p|--enable-pack`**

  Включает упаковку проекта с помощью команды [dotnet pack](dotnet-pack.md).

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="page"></a>страница

- **`-na|--namespace <NAMESPACE_NAME>`**

  Пространство имен для сформированного кода. Значение по умолчанию — `MyApp.Namespace`.

- **`-np|--no-pagemodel`**

  Создает страницу без PageModel.

***

### <a name="viewimports-proto"></a><a name="namespace"></a> viewimports, proto

- **`-na|--namespace <NAMESPACE_NAME>`**

  Пространство имен для сформированного кода. Значение по умолчанию — `MyApp.Namespace`.

***

### <a name="blazorserver"></a>blazorserver

- **`-au|--auth <AUTHENTICATION_TYPE>`**

  Тип проверки подлинности. Допустимые значения:

  - `None` — без проверки подлинности (по умолчанию).
  - `Individual` — индивидуальная проверка подлинности.
  - `IndividualB2C` — индивидуальная проверка подлинности с помощью Azure AD B2C.
  - `SingleOrg` — проверка подлинности организации для отдельного клиента.
  - `MultiOrg` — проверка подлинности организации для нескольких клиентов.
  - `Windows` — проверка подлинности Windows.

- **`--aad-b2c-instance <INSTANCE>`**

  Экземпляр Azure Active Directory B2C, к которому выполняется подключение. Используется с проверкой подлинности `IndividualB2C`. Значение по умолчанию — `https://login.microsoftonline.com/tfp/`.

- **`-ssp|--susi-policy-id <ID>`**

  Идентификатор политики входа и регистрации для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`-rp|--reset-password-policy-id <ID>`**

  Идентификатор политики сброса паролей для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`-ep|--edit-profile-policy-id <ID>`**

  Идентификатор политики изменения профилей для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`--aad-instance <INSTANCE>`**

  Экземпляр Azure Active Directory, к которому выполняется подключение. Используется с проверкой подлинности `SingleOrg` или `MultiOrg`. Значение по умолчанию — `https://login.microsoftonline.com/`.

- **`--client-id <ID>`**

  Идентификатор клиента для этого проекта. Используется с проверкой подлинности `IndividualB2C`, `SingleOrg` или `MultiOrg`. Значение по умолчанию — `11111111-1111-1111-11111111111111111`.

- **`--domain <DOMAIN>`**

  Домен клиента каталога. Используется с проверкой подлинности `SingleOrg` или `IndividualB2C`. Значение по умолчанию — `qualified.domain.name`.

- **`--tenant-id <ID>`**

  Идентификатор TenantId каталога, к которому устанавливается подключение. Используется с проверкой подлинности `SingleOrg`. Значение по умолчанию — `22222222-2222-2222-2222-222222222222`.

- **`--callback-path <PATH>`**

  Путь запроса по базовому пути кода URI перенаправления для приложения. Используется с проверкой подлинности `SingleOrg` или `IndividualB2C`. Значение по умолчанию — `/signin-oidc`.

- **`-r|--org-read-access`**

  Предоставляет приложению доступ к каталогу для чтения. Применяется только при проверке подлинности `SingleOrg` или `MultiOrg`.

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`--no-https`**

  Отключает протокол HTTPS. Этот параметр применяется, только если `Individual`, `IndividualB2C`, `SingleOrg` или `MultiOrg` не используются для `--auth`.

- **`-uld|--use-local-db`**

  Указывает, что вместо SQLite следует использовать LocalDB. Применяется только при проверке подлинности `Individual` или `IndividualB2C`.

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="web"></a>web

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Опция не доступна в .NET Core 2.2 SDK.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.1` |

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

- **`--no-https`**

  Отключает протокол HTTPS.

***

### <a name="mvc-webapp"></a><a name="web-options"></a> mvc, webapp

- **`-au|--auth <AUTHENTICATION_TYPE>`**

  Тип проверки подлинности. Допустимые значения:

  - `None` — без проверки подлинности (по умолчанию).
  - `Individual` — индивидуальная проверка подлинности.
  - `IndividualB2C` — индивидуальная проверка подлинности с помощью Azure AD B2C.
  - `SingleOrg` — проверка подлинности организации для отдельного клиента.
  - `MultiOrg` — проверка подлинности организации для нескольких клиентов.
  - `Windows` — проверка подлинности Windows.

- **`--aad-b2c-instance <INSTANCE>`**

  Экземпляр Azure Active Directory B2C, к которому выполняется подключение. Используется с проверкой подлинности `IndividualB2C`. Значение по умолчанию — `https://login.microsoftonline.com/tfp/`.

- **`-ssp|--susi-policy-id <ID>`**

  Идентификатор политики входа и регистрации для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`-rp|--reset-password-policy-id <ID>`**

  Идентификатор политики сброса паролей для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`-ep|--edit-profile-policy-id <ID>`**

  Идентификатор политики изменения профилей для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`--aad-instance <INSTANCE>`**

  Экземпляр Azure Active Directory, к которому выполняется подключение. Используется с проверкой подлинности `SingleOrg` или `MultiOrg`. Значение по умолчанию — `https://login.microsoftonline.com/`.

- **`--client-id <ID>`**

  Идентификатор клиента для этого проекта. Используется с проверкой подлинности `IndividualB2C`, `SingleOrg` или `MultiOrg`. Значение по умолчанию — `11111111-1111-1111-11111111111111111`.

- **`--domain <DOMAIN>`**

  Домен клиента каталога. Используется с проверкой подлинности `SingleOrg` или `IndividualB2C`. Значение по умолчанию — `qualified.domain.name`.

- **`--tenant-id <ID>`**

  Идентификатор TenantId каталога, к которому устанавливается подключение. Используется с проверкой подлинности `SingleOrg`. Значение по умолчанию — `22222222-2222-2222-2222-222222222222`.

- **`--callback-path <PATH>`**

  Путь запроса по базовому пути кода URI перенаправления для приложения. Используется с проверкой подлинности `SingleOrg` или `IndividualB2C`. Значение по умолчанию — `/signin-oidc`.

- **`-r|--org-read-access`**

  Предоставляет приложению доступ к каталогу для чтения. Применяется только при проверке подлинности `SingleOrg` или `MultiOrg`.

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`--no-https`**

  Отключает протокол HTTPS. Этот параметр применяется, только если `Individual`, `IndividualB2C`, `SingleOrg` или `MultiOrg` не используются.

- **`-uld|--use-local-db`**

  Указывает, что вместо SQLite следует использовать LocalDB. Применяется только при проверке подлинности `Individual` или `IndividualB2C`.

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Параметр доступен, начиная с пакета SDK для .NET Core 3.0.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

- **`--use-browserlink`**

  Включает BrowserLink в проект. Опция не доступна в .NET Core 2.2 и 3.1 SDK.

- **`-rrc|--razor-runtime-compilation`**

  Определяет, настроен ли проект для использования [компиляции среды выполнения Razor](/aspnet/core/mvc/views/view-compilation#runtime-compilation) в отладочных сборках. Параметр доступен начиная с пакета SDK для .NET Core 3.1.201.

***

### <a name="angular-react"></a><a name="spa"></a> angular, react

- **`-au|--auth <AUTHENTICATION_TYPE>`**

  Тип проверки подлинности. Доступно, начиная с пакета SDK для .NET Core 3.0.
  
  Допустимые значения:

  - `None` — без проверки подлинности (по умолчанию).
  - `Individual` — индивидуальная проверка подлинности.

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

- **`--no-https`**

  Отключает протокол HTTPS. Данная опция применяется только в том случае, если проверкой подлинности является `None`.

- **`-uld|--use-local-db`**

  Указывает, что вместо SQLite следует использовать LocalDB. Применяется только при проверке подлинности `Individual` или `IndividualB2C`. Доступно, начиная с пакета SDK для .NET Core 3.0.

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Опция не доступна в .NET Core 2.2 SDK.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.0` |

***

### <a name="reactredux"></a>reactredux

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Опция не доступна в .NET Core 2.2 SDK.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.0` |

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

- **`--no-https`**

  Отключает протокол HTTPS.

***

### <a name="razorclasslib"></a>razorclasslib

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

- **`-s|--support-pages-and-views`**

  Поддерживает добавление традиционных страниц Razor и представлений в дополнение к компонентам этой библиотеки. Доступно, начиная с пакета SDK для .NET Core 3.0.

***
  
### <a name="webapi"></a>webapi

- **`-au|--auth <AUTHENTICATION_TYPE>`**

  Тип проверки подлинности. Допустимые значения:

  - `None` — без проверки подлинности (по умолчанию).
  - `IndividualB2C` — индивидуальная проверка подлинности с помощью Azure AD B2C.
  - `SingleOrg` — проверка подлинности организации для отдельного клиента.
  - `Windows` — проверка подлинности Windows.

- **`--aad-b2c-instance <INSTANCE>`**

  Экземпляр Azure Active Directory B2C, к которому выполняется подключение. Используется с проверкой подлинности `IndividualB2C`. Значение по умолчанию — `https://login.microsoftonline.com/tfp/`.

- **`-ssp|--susi-policy-id <ID>`**

  Идентификатор политики входа и регистрации для этого проекта. Используется с проверкой подлинности `IndividualB2C`.

- **`--aad-instance <INSTANCE>`**

  Экземпляр Azure Active Directory, к которому выполняется подключение. Используется с проверкой подлинности `SingleOrg`. Значение по умолчанию — `https://login.microsoftonline.com/`.

- **`--client-id <ID>`**

  Идентификатор клиента для этого проекта. Используется с проверкой подлинности `IndividualB2C` или `SingleOrg`. Значение по умолчанию — `11111111-1111-1111-11111111111111111`.

- **`--domain <DOMAIN>`**

  Домен клиента каталога. Используется с проверкой подлинности `IndividualB2C` или `SingleOrg`. Значение по умолчанию — `qualified.domain.name`.

- **`--tenant-id <ID>`**

  Идентификатор TenantId каталога, к которому устанавливается подключение. Используется с проверкой подлинности `SingleOrg`. Значение по умолчанию — `22222222-2222-2222-2222-222222222222`.

- **`-r|--org-read-access`**

  Предоставляет приложению доступ к каталогу для чтения. Применяется только при проверке подлинности `SingleOrg`.

- **`--exclude-launch-settings`**

  Исключает файл *launchSettings.json* из создаваемого шаблона.

- **`--no-https`**

  Отключает протокол HTTPS. `app.UseHsts` и `app.UseHttpsRedirection` не добавляются к `Startup.Configure`. Этот параметр применяется, только если `IndividualB2C` или `SingleOrg` не используются для проверки подлинности.

- **`-uld|--use-local-db`**

  Указывает, что вместо SQLite следует использовать LocalDB. Применяется только при проверке подлинности `IndividualB2C`.

- **`-f|--framework <FRAMEWORK>`**

  Указывает целевую [платформу](../../standard/frameworks.md). Опция не доступна в .NET Core 2.2 SDK.

  В следующей таблице приведены значения по умолчанию в соответствии с версией пакета SDK, которую вы используете:

  | Версия пакета SDK | Значение по умолчанию   |
  |-------------|-----------------|
  | 3.1         | `netcoreapp3.1` |
  | 3.0         | `netcoreapp3.0` |
  | 2.1         | `netcoreapp2.1` |

- **`--no-restore`**

  Во время создания проекта не выполняется неявное восстановление.

***

### <a name="globaljson"></a>globaljson

- **`--sdk-version <VERSION_NUMBER>`**

  Задает версию пакета SDK для .NET Core, используемую в файле *global.json*.

***

## <a name="examples"></a>Примеры

- Создайте проект консольного приложения на C#, указав имя шаблона:

  ```dotnetcli
  dotnet new "Console Application"
  ```

- Создание проекта консольного приложения F# в текущем каталоге:

  ```dotnetcli
  dotnet new console -lang F#
  ```

- Создайте проект библиотеки классов .NET Standard в указанном каталоге:

  ```dotnetcli
  dotnet new classlib -lang VB -o MyLibrary
  ```

- Создайте новый проект MVC ASP.NET Core C# в текущем каталоге без проверки подлинности:

  ```dotnetcli
  dotnet new mvc -au None
  ```

- Создайте новый проект xUnit:

  ```dotnetcli
  dotnet new xunit
  ```

- Перечислите все шаблоны, доступные для одностраничных приложений (SPA):

  ```dotnetcli
  dotnet new spa -l
  ```

- Список всех шаблонов, соответствующих подстроке *we*. Точное совпадение не найдено, поэтому сравнение подстрок выполняется по короткому имени и столбцам имен.

  ```dotnetcli
  dotnet new we -l
  ```

- Попытайтесь вызвать шаблон, соответствующий *ng*. Если точное совпадение не найдено, выведите шаблоны с частичным совпадением.

  ```dotnetcli
  dotnet new ng
  ```

- Установите версию 2.0 шаблонов SPA для ASP.NET Core:

  ```dotnetcli
  dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0
  ```

- Перечислите установленные шаблоны и подробную информацию о них, в том числе и о том, как их удалить:

  ```dotnetcli
  dotnet new -u
  ```

- Создайте *global.json* в текущем каталоге, установив версию SDK на 3.1.101:

  ```dotnetcli
  dotnet new globaljson --sdk-version 3.1.101
  ```

## <a name="see-also"></a>См. также

- [Пользовательские шаблоны для команды dotnet new](custom-templates.md)
- [Создание пользовательского шаблона для dotnet](../tutorials/cli-templates-create-item-template.md)
- [Репозиторий dotnet/dotnet-template-samples в GitHub](https://github.com/dotnet/dotnet-template-samples)
- [Доступные шаблоны для команды dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
