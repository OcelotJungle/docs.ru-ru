---
title: Практическое руководство. Использование инструмента определения схемы XML для создания классов и документов схемы XML
ms.date: 03/30/2017
helpviewer_keywords:
- generating XML classes using XML Schema Definition tool
- generating XML Schema Document using XML Schema Definition tool
- XML Schema Definition tool, using to generate classes that conform to specific schema
- XML Schema Definition tool, using to generate XML Schema Document
ms.assetid: 51f0edc3-993d-4051-b7f2-77753694d3d1
ms.openlocfilehash: 2bbdced0f984b653a58afba9685683e8c0891271
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389801"
---
# <a name="how-to-use-the-xml-schema-definition-tool-to-generate-classes-and-xml-schema-documents"></a>Практическое руководство. Использование инструмента определения схемы XML для создания классов и документов схемы XML
С помощью инструмента определения схемы XML (Xsd.exe) можно создать схему XML, которая описывает класс, или создать класс, определенный схемой XML. В процедурах ниже показана методика выполнения таких операций.

Инструмент определения схемы XML (Xsd.exe) обычно можно найти по следующему пути:\
_C:\\Program Files (x86)\\Microsoft SDKs\\Windows\\{версия}\\bin\\NETFX {версия} Tools\\_

### <a name="to-generate-classes-that-conform-to-a-specific-schema"></a>Создание классов, соответствующих определенной схеме  
  
1. Откройте окно командной строки.  
  
2. Передайте схему XML как аргумент в инструмент определения схемы XML, который создаст набор классов, точно соответствующих схеме XML, например:  
  
    ```console  
    xsd mySchema.xsd  
    ```  
  
     Средство может обрабатывать только схемы, которые ссылаются на спецификацию XML консорциума W3C от 16 марта 2001 г. Иными словами, пространство имен схемы XML должно иметь вид "http://www.w3.org/2001/XMLSchema", как показано в следующем примере.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema attributeFormDefault="qualified" elementFormDefault="qualified" targetNamespace="" xmlns:xs="http://www.w3.org/2001/XMLSchema" />  
    ```  
  
3. При необходимости измените классы с методами, свойствами или полями. Дополнительные сведения об изменении класса с помощью атрибутов см. в разделах [Управление сериализацией XML с использованием атрибутов](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md) и [Атрибуты управления сериализацией с кодировкой SOAP](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
 Часто бывает полезным изучить схему потока XML, которая генерируется при сериализации экземпляров класса (или классов). Например, можно опубликовать схему для совместного использования или сравнить ее со схемой, в которой предпринимается попытка обеспечения соответствия.  
  
#### <a name="to-generate-an-xml-schema-document-from-a-set-of-classes"></a>Создание документа схемы XML из набора классов  
  
1. Скомпилируйте класс или классы в библиотеку DLL.  
  
2. Откройте окно командной строки.  
  
3. Передайте библиотеку DLL как аргумент в Xsd.exe, например:  
  
    ```console  
    xsd MyFile.dll  
    ```  
  
     В результате записывается схема (или схемы), которая начинается с имени "schema0.xsd".  
  
## <a name="see-also"></a>См. также

- <xref:System.Data.DataSet>
- [Инструмент определения схемы XML и сериализация XML](../../../docs/standard/serialization/the-xml-schema-definition-tool-and-xml-serialization.md)
- [Введение в сериализацию XML](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [Инструмент определения схемы XML (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Практическое руководство. Сериализация объекта](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [Практическое руководство. Десериализация объекта](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
