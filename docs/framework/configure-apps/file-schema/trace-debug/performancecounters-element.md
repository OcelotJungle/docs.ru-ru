---
title: Элемент <performanceCounters>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounters element
- <performanceCounters> element
ms.assetid: a71f605b-c7d9-4501-a5c3-abcbb964a43f
ms.openlocfilehash: f52fdb2d5b0b7911de63f96663e70735d2f2496c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697157"
---
# <a name="performancecounters-element"></a>\<performanceCounter > элемент

Задает размер глобальной памяти, совместно используемой счетчиками производительности.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp;[ **\<System. Diagnostics >** ](system-diagnostics-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp; **\<performancecounters >**  

## <a name="syntax"></a>Синтаксис

```xml
<performanceCounters filemappingsize="524288" />
```

## <a name="attributes-and-elements"></a>Атрибуты и элементы

Следующие разделы описывают атрибуты, дочерние элементы и родительские элементы.

### <a name="attributes"></a>Атрибуты

|Атрибут|Описание|
|---------------|-----------------|
|филемаппингсизе|Обязательный атрибут.<br /><br /> Указывает размер глобальной памяти, совместно используемой счетчиками производительности, в байтах. Значение по умолчанию — 524288.|

### <a name="child-elements"></a>Дочерние элементы

Нет

### <a name="parent-elements"></a>Родительские элементы

|Элемент|Описание|
|-------------|-----------------|
|`Configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|
|`system.diagnostics`|Задает корневой элемент для раздела конфигурации ASP.NET.|

## <a name="remarks"></a>Примечания

Для публикации данных производительности счетчики производительности используют размещенный в памяти файл или общую память.  Размер общей памяти определяет, сколько экземпляров можно использовать одновременно.  Существует два типа общей памяти: глобальная общая память и отдельная общая память.  Глобальная общая память используется всеми категориями счетчиков производительности, установленными с .NET Framework версиями 1,0 или 1,1.  Категории счетчиков производительности, установленные с .NET Framework версии 2,0, используют отдельную общую память, при этом каждая категория счетчиков производительности имеет собственную память.

Размер глобальной общей памяти можно задать только с помощью файла конфигурации.  Размер по умолчанию — 524 288 bДа, максимальный размер — 33 554 432 байт, а минимальный размер — 32 768 байт.  Так как глобальная общая память совместно используется всеми процессами и категориями, первый создатель определяет размер.  Если вы определяете размер в файле конфигурации приложения, этот размер используется только в том случае, если приложение является первым приложением, которое приводит к выполнению счетчиков производительности.  Поэтому правильное расположение для указания `filemappingsize` значения — файл Machine. config.  Отдельные счетчики производительности не могут освободить память в глобальной общей памяти, поэтому в конечном итоге исчерпана глобальная общая память, если создано большое количество экземпляров счетчиков производительности с разными именами.

Для размера отдельной общей памяти значение DWORD Филемаппингсизе в разделе реестра HKEY_LOCAL_MACHINE \Систем\куррентконтролсет\сервицес\\ *\<Category name >* \перформанце упоминается первым, а затем значение, указанное для глобальной общей памяти в файле конфигурации. Если значение Филемаппингсизе не существует, то отдельный размер общей памяти устанавливается равным четвертому (1/4) глобальному параметру в файле конфигурации.

## <a name="see-also"></a>См. также:

- <xref:System.Diagnostics.PerformanceCounter>
- <xref:System.Diagnostics.PerformanceCounterCategory>
- <xref:System.Diagnostics.PerformanceCounter.InstanceLifetime%2A>
- <xref:System.Diagnostics.PerformanceCounterInstanceLifetime>
