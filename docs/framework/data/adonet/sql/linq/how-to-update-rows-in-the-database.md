---
title: Практическое руководство. Как обновлять строки в базе данных
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a2b5c90f-6cc3-4128-bfab-1db488d5af26
ms.openlocfilehash: c2055e1dd988352b50a439531ab5533f34a4965e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793130"
---
# <a name="how-to-update-rows-in-the-database"></a>Практическое руководство. Как обновлять строки в базе данных

Строки в базе данных можно обновлять, изменяя значения членов объектов, связанных с [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601> коллекцией, а затем отправляя изменения в базу данных. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]преобразует изменения в соответствующие команды SQL `UPDATE` .

> [!NOTE]
> Можно переопределить методы [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], используемые по умолчанию для операций `Insert`, `Update` и `Delete` базы данных. Дополнительные сведения см. в разделе [Настройка операций вставки, обновления и удаления](customizing-insert-update-and-delete-operations.md).
>
> Разработчики, использующие Visual Studio, могут использовать реляционный конструктор объектов для разработки хранимых процедур для той же цели.

В следующих шагах предполагается, что подключение к базе данных Northwind выполняется с помощью допустимого объекта <xref:System.Data.Linq.DataContext>. Дополнительные сведения см. в разделе [Практическое руководство. Подключитесь к базе](how-to-connect-to-a-database.md)данных.

### <a name="to-update-a-row-in-the-database"></a>Чтобы обновить строку в базе данных, выполните следующие действия.

1. Отправьте в базу данных запрос на обновляемую строку.

2. Выполните необходимые изменения значений членов полученного объекта [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].

3. Отправьте изменения в базу данных.

## <a name="example"></a>Пример

В следующем примере выполняются запросы к базе данных для заказа № 11000, а затем изменяются значения `ShipName` и `ShipVia` полученного объекта `Order`. И наконец, изменения этих членов отправляются в базу данных в качестве изменений столбцов `ShipName` и `ShipVia`.

[!code-csharp[System.Data.Linq.Table#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#2)]
[!code-vb[System.Data.Linq.Table#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#2)]

## <a name="see-also"></a>См. также

- [Практическое руководство. Управление конфликтами изменений](how-to-manage-change-conflicts.md)
- [Практическое руководство. Назначение хранимых процедур для выполнения обновлений, вставок и удалений (реляционный конструктор объектов)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [Внесение и отправка изменений данных](making-and-submitting-data-changes.md)
