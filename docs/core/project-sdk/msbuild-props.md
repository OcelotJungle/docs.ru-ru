---
title: Свойства MSBuild для Microsoft.NET.Sdk
description: Справочник по свойствам MSBuild, распознаваемым пакетом SDK для .NET Core.
ms.date: 02/14/2020
ms.topic: reference
ms.openlocfilehash: 800ff59310d8437d7f770bf20a5bdf37714f8515
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795577"
---
# <a name="msbuild-properties-for-net-core-sdk-projects"></a>Свойства MSBuild для проектов пакета SDK для .NET Core

На этой странице описываются свойства MSBuild для настройки проектов .NET Core. Можно указать *метаданные* для каждого свойства в качестве дочерних элементов свойства.

> [!NOTE]
> Работа над этой страницей еще не завершена, поэтому здесь приведены лишь некоторые полезные свойства MSBuild для пакета SDK для .NET Core. Список стандартных свойств см. в статье [Общие свойства MSBuild](/visualstudio/msbuild/common-msbuild-project-properties).

## <a name="framework-properties"></a>Свойства платформы

- [TargetFramework](#targetframework)
- [TargetFrameworks](#targetframeworks)
- [NetStandardImplicitPackageVersion](#netstandardimplicitpackageversion)

### <a name="targetframework"></a>TargetFramework

Свойство `TargetFramework` указывает версию целевой платформы для приложения, которая неявно ссылается на [метапакет](../packages.md#metapackages). Список допустимых моникеров целевой платформы см. в статье [Целевые платформы в проектах в стиле SDK](../../standard/frameworks.md#supported-target-framework-versions).

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

Дополнительные сведения см.в статье [Целевые платформы в проектах в стиле SDK](../../standard/frameworks.md).

### <a name="targetframeworks"></a>TargetFrameworks

Используйте свойство `TargetFrameworks`, если приложение должно быть предназначено для нескольких платформ. Список допустимых моникеров целевой платформы см. в статье [Целевые платформы в проектах в стиле SDK](../../standard/frameworks.md#supported-target-framework-versions).

> [!NOTE]
> Это свойство игнорируется, если указано свойство `TargetFramework` (в единственном числе).

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

Дополнительные сведения см.в статье [Целевые платформы в проектах в стиле SDK](../../standard/frameworks.md).

### <a name="netstandardimplicitpackageversion"></a>NetStandardImplicitPackageVersion

> [!NOTE]
> Это свойство применяется только к проектам, использующим `netstandard1.x`. Он не применяется к проектам, использующим `netstandard2.x`.

Используйте свойство `NetStandardImplicitPackageVersion`, если требуется указать версию платформы ниже версии [метапакета](../packages.md#metapackages). Файл проекта, приведенный в следующем примере, предназначен для `netstandard1.3`, но использует `NETStandard.Library` версии 1.6.0.

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a>Свойства пакета

Для описания пакета, созданного из проекта, можно указать такие свойства, как `PackageId`, `PackageVersion`, `PackageIcon`, `Title` и `Description`. Дополнительные сведения об этих и других свойствах см. в разделе [целевой объект пакета](/nuget/reference/msbuild-targets#pack-target).

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties"></a>Параметры публикации

- [RuntimeIdentifier](#runtimeidentifier)
- [RuntimeIdentifiers](#runtimeidentifiers)
- [TrimmerRootAssembly](#trimmerrootassembly)
- [UseAppHost](#useapphost)

### <a name="runtimeidentifier"></a>RuntimeIdentifier

Свойство `RuntimeIdentifier` позволяет указать для проекта один [идентификатор среды выполнения (RID)](../rid-catalog.md). Идентификатор среды выполнения позволяет опубликовать автономное развертывание.

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

Свойство `RuntimeIdentifiers` позволяет указать для проекта список [идентификаторов среды выполнения (RID)](../rid-catalog.md) (в качестве разделителя используется точка с запятой). Используйте это свойство, если вам нужна публикация для нескольких сред. `RuntimeIdentifiers` используется во время восстановления для обеспечения наличия в графе нужных ресурсов.

> [!TIP]
> `RuntimeIdentifier` (в единственном числе) может ускорить создание сборок, когда требуется только одна среда выполнения.

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a>TrimmerRootAssembly

Элемент `TrimmerRootAssembly` позволяет исключить сборку из [*обрезки*](../deploying/trim-self-contained.md). Обрезка — это процесс удаления неиспользуемых частей среды выполнения из упакованного приложения. В некоторых случаях при обрезке могут неправильно удаляться необходимые ссылки.

Следующий код XML исключает сборку `System.Security` из обрезки.

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a>UseAppHost

Свойство `UseAppHost` было представлено в пакете SDK для .NET Core.версии 2.1.400. Оно контролирует создание собственного исполняемого файла для развертывания. Этот файл требуется для автономных развертываний.

В .NET Core 3.0 и более поздних версиях зависимый от платформы исполняемый файл создается по умолчанию. Задайте свойству `UseAppHost` значение `false`, чтобы отключить создание исполняемого файла.

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

Дополнительные сведения о развертывании см. в статье [Развертывание приложений .NET Core](../deploying/index.md).

## <a name="compile-properties"></a>Свойства компиляции

- [LangVersion](#langversion)

### <a name="langversion"></a>LangVersion

Свойство `LangVersion` позволяет указать конкретную версию языка программирования. Например, если требуется доступ к предварительным версиям функций C#, задайте параметру `LangVersion` значение `preview`.

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

Дополнительные сведения см. в статье [Управление версиями языка C#](../../csharp/language-reference/configure-language-version.md#override-a-default).

## <a name="run-time-configuration-properties"></a>Свойства конфигурации среды выполнения

Вы можете настроить некоторые варианты поведения среды выполнения, указав свойства MSBuild в файле проекта приложения. Сведения о других способах настройки поведения среды выполнения см. в разделе [Параметры конфигурации среды выполнения .NET Core](../run-time-config/index.md).

- [ConcurrentGarbageCollection](#concurrentgarbagecollection)
- [InvariantGlobalization](#invariantglobalization)
- [RetainVMGarbageCollection](#retainvmgarbagecollection)
- [ServerGarbageCollection](#servergarbagecollection)
- [ThreadPoolMaxThreads](#threadpoolmaxthreads)
- [ThreadPoolMinThreads](#threadpoolminthreads)
- [TieredCompilation](#tieredcompilation)
- [TieredCompilationQuickJit](#tieredcompilationquickjit)
- [TieredCompilationQuickJitForLoops](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a>ConcurrentGarbageCollection

Свойство `ConcurrentGarbageCollection` указывает, включена ли [фоновая (параллельная) сборка мусора](../../standard/garbage-collection/background-gc.md). Задайте значение `false`, чтобы отключить фоновую сборку мусора. Дополнительные сведения см. в разделе [System.GC.Concurrent/COMPlus_gcConcurrent](../run-time-config/garbage-collector.md#systemgcconcurrentcomplus_gcconcurrent).

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a>InvariantGlobalization

Свойство `InvariantGlobalization` определяет, выполняется ли приложение в *инвариантном режиме глобализации*, что означает, что у него нет доступа к данным, относящимся к языку и региональным параметрам. Установите значение `true` для запуска в инвариантном режиме глобализации. Дополнительные сведения см. в разделе [Инвариантный режим](../run-time-config/globalization.md#invariant-mode).

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a>RetainVMGarbageCollection

Свойство `RetainVMGarbageCollection` настраивает сборщик мусора для помещения удаленных сегментов памяти в список ожидания для будущего использования или освобождения. Значение `true` указывает сборщику мусора разместить сегменты в списке ожидания. Дополнительные сведения см. в разделе [System.GC.RetainVM/COMPlus_GCRetainVM](../run-time-config/garbage-collector.md#systemgcretainvmcomplus_gcretainvm).

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a>ServerGarbageCollection

Свойство `ServerGarbageCollection` указывает, использует ли приложение [сборку мусора рабочей станции или сборку мусора сервера](../../standard/garbage-collection/workstation-server-gc.md). Задайте значение `true`, чтобы использовать сборку мусора сервера. Дополнительные сведения см. в разделе [System.GC.Server/COMPlus_gcServer](../run-time-config/garbage-collector.md#systemgcservercomplus_gcserver).

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a>ThreadPoolMaxThreads

Свойство `ThreadPoolMaxThreads` указывает максимальное число потоков для пула рабочих потоков. Дополнительные сведения см. в разделе [Максимальное число потоков](../run-time-config/threading.md#maximum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a>ThreadPoolMinThreads

Свойство `ThreadPoolMinThreads` указывает минимальное число потоков для пула рабочих потоков. Дополнительные сведения см. в разделе [Минимальное число потоков](../run-time-config/threading.md#minimum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a>TieredCompilation

Свойство `TieredCompilation` указывает, использует ли JIT-компилятор [многоуровневую компиляцию](../whats-new/dotnet-core-3-0.md#tiered-compilation). Задайте значение `false`, чтобы отключить многоуровневую компиляцию. Дополнительные сведения см. в разделе [Многоуровневая компиляция](../run-time-config/compilation.md#tiered-compilation).

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a>TieredCompilationQuickJit

Свойство `TieredCompilationQuickJit` указывает, использует ли JIT-компилятор быструю JIT-компиляцию. Задайте значение `false`, чтобы отключить быструю JIT-компиляцию. Дополнительные сведения см. в разделе [Быстрая JIT-компиляция](../run-time-config/compilation.md#quick-jit).

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a>TieredCompilationQuickJitForLoops

Свойство `TieredCompilationQuickJitForLoops` указывает, использует ли JIT-компилятор быструю JIT-компиляцию для методов, содержащих циклы. Задайте значение `true`, чтобы включить быструю JIT-компиляцию для методов, содержащих циклы. Дополнительные сведения см. в разделе [Быстрая JIT-компиляция для циклов](../run-time-config/compilation.md#quick-jit-for-loops).

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties"></a>Свойства ссылки

- [AssetTargetFallback](#assettargetfallback)
- [PackageReference](#packagereference)
- [ProjectReference](#projectreference)
- [Ссылки](#reference)
- [Свойства восстановления](#restore-properties)

### <a name="assettargetfallback"></a>AssetTargetFallback

Свойство `AssetTargetFallback` позволяет указать дополнительные совместимые версии платформы для ссылок на проекты и пакетов NuGet. Например, если вы указали зависимость пакета с помощью `PackageReference`, но в этом пакете нет ресурсов, совместимых с `TargetFramework` вашего проекта, тогда пригодится свойство `AssetTargetFallback`. Совместимость пакета, на который указывает ссылка, повторно проверяется с помощью каждой целевой платформы, указанной в свойстве `AssetTargetFallback`.

В качестве значения свойства `AssetTargetFallback` можно задать одну [версию целевой платформы](../../standard/frameworks.md#supported-target-framework-versions) или несколько.

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="packagereference"></a>PackageReference

`PackageReference` определяет ссылку на пакет NuGet. Например, может потребоваться сослаться на один пакет, а не на [метапакет](../packages.md#metapackages).

Атрибут `Include` указывает идентификатор пакета. Атрибут `Version` указывает версию или диапазон версий. Сведения о том, как указать минимальную версию, максимальную версию, диапазон или точное соответствие, см. в разделе [Диапазоны версий](/nuget/concepts/package-versioning#version-ranges). Вы также можете добавить в ссылку на проект следующие метаданные: `IncludeAssets`, `ExcludeAssets` и `PrivateAssets`.

Фрагмент файла проекта в следующем примере ссылается на пакет [System.Runtime](https://www.nuget.org/packages/System.Runtime/).

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

Дополнительные сведения см. в статье [Ссылки на пакеты в файлах проекта](/nuget/consume-packages/package-references-in-project-files).

### <a name="projectreference"></a>СсылкаНаПроект

Элемент `ProjectReference` определяет ссылку на другой проект. Проект, на который указывает ссылка, добавляется как зависимость пакета NuGet, то есть обрабатывается так же, как `PackageReference`.

Атрибут `Include` задает путь к проекту. Вы также можете добавить в ссылку на проект следующие метаданные: `IncludeAssets`, `ExcludeAssets` и `PrivateAssets`.

Фрагмент файла проекта в следующем примере ссылается на проект `Project2`.

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a>Справочник

Элемент `Reference` определяет ссылку на файл сборки.

Атрибут `Include` задает имя файла, а дочерний элемент `HintPath` указывает путь к сборке.

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-properties"></a>Свойства восстановления

При восстановлении пакета, на который указывает ссылка, устанавливаются все его прямые зависимости и все зависимости этих зависимостей. Можно настроить восстановление пакетов, указав такие свойства, как `RestorePackagesPath` и `RestoreIgnoreFailedSources`. Дополнительные сведения об этих и других свойствах см. в разделе [целевой объект восстановления](/nuget/reference/msbuild-targets#restore-target).

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="see-also"></a>См. также

- [Справочник по схеме MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [Общие свойства MSBuild](/visualstudio/msbuild/common-msbuild-project-properties)
- [Свойства MSBuild для целевого объекта pack NuGet](/nuget/reference/msbuild-targets#pack-target)
- [Свойства MSBuild для целевого объекта restore NuGet](/nuget/reference/msbuild-targets#restore-properties)
- [Настройка сборки](/visualstudio/msbuild/customize-your-build)
