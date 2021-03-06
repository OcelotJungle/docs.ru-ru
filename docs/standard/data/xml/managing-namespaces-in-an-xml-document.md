---
title: Управление пространствами имен в XML-документе
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 682643fc-b848-4e42-8c0d-50deeaeb5f2a
ms.openlocfilehash: 1b3e57c0a8a37574a92d23cf1d623301cc54b984
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/05/2020
ms.locfileid: "82796156"
---
# <a name="managing-namespaces-in-an-xml-document"></a>Управление пространствами имен в XML-документе
Пространства имен XML связывают имена элементов и атрибутов в XML-документе с пользовательскими и стандартными URI. Для создания этих связей определяются префиксы для URI пространства имен, с помощью которых затем квалифицируются имена элементов и атрибутов в XML-данных. Пространства имен предотвращают конфликты имен элементов и атрибутов, а также позволяют обрабатывать и проверять элементы и атрибуты с одним и тем же именем.  
  
<a name="declare"></a>
## <a name="declaring-namespaces"></a>Объявление пространств имен  
 Пространство имен для элемента объявляется с помощью атрибута `xmlns:`:  
  
 `xmlns:<name>=<"uri">`  
  
 где `<name>` — это префикс пространства имен, а `<"uri">` — это URI, который определяет это пространство имен. После объявления префикса его можно использовать для уточнения имен элементов и атрибутов в XML-документе и связывания их с URI-кодом пространства имен. Так как этот префикс пространства имен используется во всем документе, он должен быть коротким.  
  
 В данном примере определяются два элемента `BOOK`. Первый элемент квалифицируется префиксом `mybook`, а второй — префиксом `bb`. Каждый префикс связан с разными URI-кодами пространств имен:  
  
```xml  
<mybook:BOOK xmlns:mybook="http://www.contoso.com/books.dtd">  
<bb:BOOK xmlns:bb="urn:blueyonderairlines" />
</mybook>
```  
  
 Чтобы указать, что элемент принадлежит к определенному пространству имен, добавьте к нему префикс пространства имен. Например, если элемент `Author` принадлежит пространству имен `mybook`, то он объявляется как `<mybook:Author>`.  
  
<a name="scope"></a>
## <a name="declaration-scope"></a>Область видимости объявления  
 Пространство имен действует от точки объявления до конца элемента, где оно было объявлено. В этом примере пространство имен, определенное в элементе `BOOK`, не применяется к элементам, которые находятся за пределами элемента `BOOK`, например к элементу `Publisher`:  
  
```xml  
<Author>Joe Smith</Author>  
<BOOK xmlns:book="http://www.contoso.com">  
    <title>My Wonderful Day</title>  
      <price>$3.95</price>  
</BOOK>  
<Publisher>  
    <Name>MSPress</Name>  
</Publisher>  
```  
  
 Пространство имен можно использовать только после его объявления, однако это не значит, что объявление пространства имен должно располагаться в самом начале XML-документа.  
  
 Если в XML-документе используются несколько пространств имен, можно определить одно из них как пространство по умолчанию, чтобы упростить чтение документа. Пространство имен по умолчанию объявляется в корневом элементе и применяется ко всем элементам в документе, которые не квалифицированы. Пространства имен по умолчанию применяются только к элементам и не применяются к атрибутам.  
  
 Для использования пространства имен по умолчанию не указывайте префикс и двоеточие в объявлении элемента:  
  
```xml  
<BOOK xmlns="http://www.contoso.com/books.dtd">  
...
</BOOK>
```  
  
## <a name="managing-namespaces"></a>Управление пространствами имен  
 В классе <xref:System.Xml.XmlNamespaceManager> хранится коллекция URI пространств имен и их префиксов. С его помощью можно искать, добавлять и удалять пространства имен из этой коллекции. В некоторых контекстах этот класс необходим для повышения производительности обработки XML. Например, класс <xref:System.Xml.Xsl.XsltContext> используется классом <xref:System.Xml.XmlNamespaceManager> для обеспечения поддержки XPath.  
  
 Диспетчер пространств имен не выполняет проверку пространств имен, так как предполагается, что префиксы и пространства имен уже проверены и соответствуют спецификации [W3C для пространств имен](https://www.w3.org/TR/REC-xml-names/).  
  
> [!NOTE]
> Интерфейс LINQ to XML [в C#](../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md) и [Visual Basic](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md) использует <xref:System.Xml.XmlNamespaceManager> для управления пространствами имен. Дополнительные сведения об управлении пространствами имен в случае использования LINQ to XML см. в документации по LINQ, в разделах [Работа с пространствами имен XML (C#)](../../../csharp/programming-guide/concepts/linq/namespaces-overview-linq-to-xml.md) и [Работа с пространствами имен XML (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
 Вот некоторые из задач по управлению и подстановке, которые можно выполнить с помощью класса <xref:System.Xml.XmlNamespaceManager>. Дополнительные сведения и примеры см. в разделах справочника, посвященных каждому методу или свойству.  
  
|Кому|Использовать|  
|--------|---------|  
|Добавление пространства имен|Метод <xref:System.Xml.XmlNamespaceManager.AddNamespace%2A>|  
|Удаление пространства имен|Метод <xref:System.Xml.XmlNamespaceManager.RemoveNamespace%2A>|  
|Поиск URI для пространства имен по умолчанию|Свойство<xref:System.Xml.XmlNamespaceManager.DefaultNamespace%2A>|  
|Поиск URI для префикса пространства имен|Метод <xref:System.Xml.XmlNamespaceManager.LookupNamespace%2A>|  
|Поиск префикса для URI-кодов пространства имен|Метод <xref:System.Xml.XmlNamespaceManager.LookupPrefix%2A>|  
|Получение списка пространств имен, которые есть на текущем узле|Метод <xref:System.Xml.XmlNamespaceManager.GetNamespacesInScope%2A>|  
|Задание области видимости пространства имен|Методы <xref:System.Xml.XmlNamespaceManager.PushScope%2A> и <xref:System.Xml.XmlNamespaceManager.PopScope%2A>|  
|Проверка того, определен ли префикс в текущей области|Метод <xref:System.Xml.XmlNamespaceManager.HasNamespace%2A>|  
|Получение таблицы имен используется для поиска префиксов и URI|Свойство<xref:System.Xml.XmlNamespaceManager.NameTable%2A>|  
  
## <a name="see-also"></a>См. также

- <xref:System.Xml.XmlNamespaceManager>
- [XML-документы и данные](../../../../docs/standard/data/xml/index.md)
