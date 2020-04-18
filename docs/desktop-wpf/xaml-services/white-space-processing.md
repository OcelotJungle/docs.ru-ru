---
title: Обработка пробелов в XAML
ms.date: 03/30/2017
helpviewer_keywords:
- East Asian characters [XAML Services]
- XAML [XAML Services], white-space processing
- white-space processing in XAML [XAML Services]
- characters [XAML Services], East Asian
ms.assetid: cc9cc377-7544-4fd0-b65b-117b90bb0b23
ms.openlocfilehash: 05f28c9115326424164b92e1b704c52bba31cf35
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432848"
---
# <a name="white-space-processing-in-xaml"></a>Обработка пробелов в XAML

Языковые правила XAML заявляют, что значительное белое пространство должно обрабатываться реализацией процессора. [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] В этой статье документы эти правила языка XAML. Он также документирует дополнительную обработку [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] белого пространства, которая определяется реализацией процессора XAML и автором XAML для сериализации.

## <a name="white-space-definition"></a>Определение белого пространства

В соответствии с XML, [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] бело-пространственных символов в пространстве, linefeed, и вкладке. Они соответствуют значениям Unicode 0020, 000A и 0009 соответственно.

## <a name="white-space-normalization"></a>Нормализация белого пространства

По умолчанию следующая нормализация белого [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] пространства [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] происходит, когда процессор обрабатывает файл:

1. Символы перевода строки между восточно-азиатскими символами удаляются. Определение этого термина см. в разделе "Символы восточно-азиатских языков" далее.

2. Все символы белого пространства (пространство, linefeed, вкладка) преобразуются в пробелы.

3. Все последовательные пробелы удаляются и заменяется одним пробелом.

4. Пробел после открывающего тега удаляется.

5. Пробел перед закрывающим тегом удаляется.

"Default" соответствует состоянию, обозначаемому значением атрибута [XML: space](xml-space-handling.md) по умолчанию.

## <a name="white-space-in-inner-text-and-string-primitives"></a>Белое пространство во внутреннем тексте, и строки примитивы

Приведенные выше правила нормализации применяются к тексту внутри элементов XAML. После нормализации обработчик XAML преобразует любой внутренний текст в соответствующий тип следующим образом.

- Если тип свойства не является коллекцией и типом <xref:System.Object> , обработчик XAML попытается преобразовать его в этот тип, используя преобразователь типов. Неудачное преобразование приводит к ошибке во время компиляции.

- Если тип свойства — это коллекция, а внутренний текст не прерывается (не содержит промежуточных тегов элементов), внутренний текст анализируется как один <xref:System.String>. Если тип коллекции не может принять <xref:System.String>, это также приводит к ошибке во время компиляции.

- Если тип свойства — <xref:System.Object>, внутренний текст анализируется как один <xref:System.String>. Если существуют промежуточные теги элементов, это приводит к ошибке во время компиляции, поскольку <xref:System.Object> подразумевает один объект (<xref:System.String> или другой).

- Если тип свойства — коллекция, а внутренний текст прерывается, первая подстрока преобразуется в <xref:System.String> и добавляется как элемент коллекции, затем промежуточный элемент добавляется как элемент коллекции, и, наконец, конечная подстрока (если таковая имеется) добавляется в коллекцию как третий элемент <xref:System.String> .

## <a name="preserving-white-space"></a>Сохранение белого пространства

Есть несколько методов для сохранения [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] белого пространства в источнике для возможной презентации, которые не зависят от нормализации белого пространства [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] процессора.

**xml:space'"сохранить"**: Укажите этот атрибут на уровне элемента, где желательно сохранение белого пространства. При этом сохраняются все пробелы, включая те, что могут быть добавлены приложениями редактирования кода для выравнивания элементов и улучшения визуального восприятия. Однако то, отображаются ли эти пробелы, определяется моделью контента элемента. Избегайте `xml:space="preserve"` указания на корневом уровне, поскольку большинство моделей объектов не считают белое пространство значительным независимо от того, как вы устанавливаете атрибут. Глобальная установка `xml:space` может отрицательно повлиять на производительность обработки XAML (в частности, на сериализацию) в некоторых реализациях. Лучше всего установить атрибут только на уровне элементов, которые отрисовывают белое пространство в строках или представляют собой значительные коллекции белого пространства.

**Сущности и ненарушающие пространства:** [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] поддерживает размещение любой сущности Unicode в модели текстовых объектов. Можно использовать специальные объекты, такие \#как неразрушающее пространство (&160; в кодировании UTF-8). Можно также использовать элементы управления форматированным текстом, поддерживающие неразрывные пробелы. Следует соблюдать осторожность при использовании сущностей для имитации характеристики разметки, таких как отступы, поскольку выходные данные сущностей во время выполнения зависят от множества факторов, при этом возможности формирования получения отступов в типичной системе разметки, например правильное использование панелей и полей, ограничены. Например, сущности сопоставляются со шрифтами и могут изменять размер после выбора шрифта пользователем.

## <a name="east-asian-characters"></a>Восточноазиатские персонажи

«Восточноазиатские персонажи» определяются как набор символов Unicode в диапазоне U-20000 до U-2FFFD и U-30000 до U-3FFFD. Это подмножество также иногда называют "CJK-иероглифами". Для получения дополнительной информации см. <https://www.unicode.org>.

## <a name="white-space-and-text-content-models"></a>Модели белого пространства и текстового контента

На практике сохранение белого пространства вызывает озабоченность лишь для подмножества всех возможных моделей контента. Это подмножество состоит из моделей содержимого, которые могут принимать одноэлементный тип <xref:System.String> в определенной форме, выделенную коллекцию <xref:System.String> или сочетание <xref:System.String> и других типов в коллекции <xref:System.Collections.IList> или <xref:System.Collections.Generic.ICollection%601> .

### <a name="white-space-and-text-content-models-in-wpf"></a>Модели белого пространства и текстового контента в WPF

Для наглядности оставшаяся часть этого подраздела ссылается на конкретные типы, определенные в WPF. Функции обработки белого пространства, описанные в этой статье, относятся как к .NET XAML Services, так и к WPF. Чтобы увидеть это в действии, можно поэкспериментировать с некоторой разметкой WPF XAML, просмотреть результаты в графе объектов и снова сериализовать их в разметку.

Даже для моделей содержимого, которые могут принимать строки, поведение по умолчанию в этих моделях содержимого заключается в том, что любое белое пространство, которое остается, не рассматривается как значительное. Например, <xref:System.Windows.Controls.ListBox> берется, <xref:System.Collections.IList>но белое пространство (например, линейные ленты между каждым) <xref:System.Windows.Controls.ListBoxItem>не сохраняется и не отображается. Попытка использовать символ перевода строки в качестве разделителей между строками для элементов <xref:System.Windows.Controls.ListBoxItem> вообще не даст результатов. Строки, разделенные символами перевода строки, считаются одной строкой и одним элементом.

Те коллекции, которые рассматривают белое пространство как значительное, как правило, являются частью модели документа потока. Основная коллекция, которая поддерживает поведение <xref:System.Windows.Documents.InlineCollection>сохранения белого пространства. Этот класс коллекции <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>объявляется с помощью ; при обнаружении этого [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] атрибута процессор будет рассматривать белое пространство в коллекции как значительное. Сочетание `xml:space="preserve"` белого пространства в <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> обозначенной коллекции состоит в том, что все белое пространство сохраняется и визуалируется. Сочетание `xml:space="default"` и белого пространства <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> в пределах вызывает первоначальную нормализацию белого пространства, описанную ранее, которая оставляет одно пространство в определенных положениях, и эти пространства сохраняются и отображаются. Предпочтительное для вас поведение выбираете вы. Следует выборочно использовать `xml:space` , чтобы включить желаемое поведение.

Кроме того, некоторые встроенные элементы, обозначающие разрыв строки в модели документа потока, должны намеренно не вводить дополнительное пространство даже в значительной коллекции белого пространства. Например, <xref:System.Windows.Documents.LineBreak> элемент имеет ту же \<цель, что и тег BR/> в HTML, а для читаемости в разметке, как правило, a <xref:System.Windows.Documents.LineBreak> отделен от любого последующего текста авторским лентой. Этот символ не следует нормализовать, чтобы он не стал начальным пробелом в следующей строке. Для такого поведения определение класса <xref:System.Windows.Documents.LineBreak> для элемента применяется <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>, которое затем интерпретируется [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] процессором, чтобы означать, что окружение <xref:System.Windows.Documents.LineBreak> белого пространства всегда обрезается.

## <a name="see-also"></a>См. также

- [Обзор XAML (WPF)](../fundamentals/xaml.md)
- [Сущности символов XML и XAML](xml-character-entities.md)
- [xml:обработка пространства в XAML](xml-space-handling.md)