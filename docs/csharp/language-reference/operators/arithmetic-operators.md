---
title: Арифметические операторы — справочник по C#
description: Сведения об операторах C#, выполняющих операции умножения, деления, вычисления остатка, сложения и вычитания с числовыми типами.
ms.date: 03/27/2019
author: pkulikov
f1_keywords:
- ++_CSharpKeyword
- --_CSharpKeyword
- '*_CSharpKeyword'
- /_CSharpKeyword
- '%_CSharpKeyword'
- +_CSharpKeyword
- -_CSharpKeyword
helpviewer_keywords:
- arithmetic operators [C#]
- increment operator [C#]
- ++ operator [C#]
- decrement operator [C#]
- -- operator [C#]
- multiplication operator [C#]
- '* operator [C#]'
- division operator [C#]
- / operator [C#]
- remainder operator [C#]
- '% operator [C#]'
- addition operator [C#]
- + operator [C#]
- subtraction operator [C#]
- '- operator [C#]'
ms.openlocfilehash: 192acf6fea0c6014aaf092077f8deaa844dfd2ec
ms.sourcegitcommit: d938c39afb9216db377d0f0ecdaa53936a851059
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58633807"
---
# <a name="arithmetic-operators-c-reference"></a><span data-ttu-id="059ba-103">Арифметические операторы (справочник по C#)</span><span class="sxs-lookup"><span data-stu-id="059ba-103">Arithmetic operators (C# Reference)</span></span>

<span data-ttu-id="059ba-104">Следующие операторы выполняют арифметические операции с числовыми типами:</span><span class="sxs-lookup"><span data-stu-id="059ba-104">The following operators perform arithmetic operations with numeric types:</span></span>

- <span data-ttu-id="059ba-105">Унарные операторы [`++` (инкремент)](#increment-operator-), [`--` (декремент)](#decrement-operator---), [`+` (плюс)](#unary-plus-and-minus-operators) и [`-` (минус)](#unary-plus-and-minus-operators).</span><span class="sxs-lookup"><span data-stu-id="059ba-105">Unary [`++` (increment)](#increment-operator-), [`--` (decrement)](#decrement-operator---), [`+` (plus)](#unary-plus-and-minus-operators), and [`-` (minus)](#unary-plus-and-minus-operators) operators.</span></span>
- <span data-ttu-id="059ba-106">Бинарные операторы [`*` (умножение)](#multiplication-operator-), [`/` (деление)](#division-operator-), [`%` (остаток)](#remainder-operator-), [`+` (сложение)](#addition-operator-) и [`-` (вычитание)](#subtraction-operator--).</span><span class="sxs-lookup"><span data-stu-id="059ba-106">Binary [`*` (multiplication)](#multiplication-operator-), [`/` (division)](#division-operator-), [`%` (remainder)](#remainder-operator-), [`+` (addition)](#addition-operator-), and [`-` (subtraction)](#subtraction-operator--) operators.</span></span>

<span data-ttu-id="059ba-107">Эти операторы поддерживают все [целочисленные](../keywords/integral-types-table.md) типы и типы с [плавающей запятой](../keywords/floating-point-types-table.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-107">Those operators support all [integral](../keywords/integral-types-table.md) and [floating-point](../keywords/floating-point-types-table.md) numeric types.</span></span>

## <a name="increment-operator-"></a><span data-ttu-id="059ba-108">Оператор инкремента ++</span><span class="sxs-lookup"><span data-stu-id="059ba-108">Increment operator ++</span></span>

<span data-ttu-id="059ba-109">Оператор инкремента `++` увеличивает операнд на 1.</span><span class="sxs-lookup"><span data-stu-id="059ba-109">The unary increment operator `++` increments its operand by 1.</span></span> <span data-ttu-id="059ba-110">Операндом должна быть переменная, [свойство](../../programming-guide/classes-and-structs/properties.md) или [индексатор](../../../csharp/programming-guide/indexers/index.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-110">The operand must be a variable, a [property](../../programming-guide/classes-and-structs/properties.md) access, or an [indexer](../../../csharp/programming-guide/indexers/index.md) access.</span></span>

<span data-ttu-id="059ba-111">Оператор инкремента поддерживается в двух формах: постфиксный оператор инкремента (`x++`) и префиксный оператор инкремента (`++x`).</span><span class="sxs-lookup"><span data-stu-id="059ba-111">The increment operator is supported in two forms: the postfix increment operator, `x++`, and the prefix increment operator, `++x`.</span></span>

### <a name="postfix-increment-operator"></a><span data-ttu-id="059ba-112">Постфиксный оператор приращения</span><span class="sxs-lookup"><span data-stu-id="059ba-112">Postfix increment operator</span></span>

<span data-ttu-id="059ba-113">Результатом `x++` является значение `x` *перед* выполнением операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="059ba-113">The result of `x++` is the value of `x` *before* the operation, as the following example shows:</span></span>

[!code-csharp-interactive[postfix increment](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#PostfixIncrement)]

### <a name="prefix-increment-operator"></a><span data-ttu-id="059ba-114">Префиксный оператор инкремента</span><span class="sxs-lookup"><span data-stu-id="059ba-114">Prefix increment operator</span></span>

<span data-ttu-id="059ba-115">Результатом `++x` является значение `x` *после* выполнения операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="059ba-115">The result of `++x` is the value of `x` *after* the operation, as the following example shows:</span></span>

[!code-csharp-interactive[prefix increment](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#PrefixIncrement)]

## <a name="decrement-operator---"></a><span data-ttu-id="059ba-116">Оператор декремента --</span><span class="sxs-lookup"><span data-stu-id="059ba-116">Decrement operator --</span></span>

<span data-ttu-id="059ba-117">Унарный оператор декремента `--` уменьшает операнд на 1.</span><span class="sxs-lookup"><span data-stu-id="059ba-117">The unary decrement operator `--` decrements its operand by 1.</span></span> <span data-ttu-id="059ba-118">Операндом должна быть переменная, [свойство](../../programming-guide/classes-and-structs/properties.md) или [индексатор](../../../csharp/programming-guide/indexers/index.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-118">The operand must be a variable, a [property](../../programming-guide/classes-and-structs/properties.md) access, or an [indexer](../../../csharp/programming-guide/indexers/index.md) access.</span></span>

<span data-ttu-id="059ba-119">Оператор декремента поддерживается в двух формах: постфиксный оператор декремента (`x--`) и префиксный оператор декремента (`--x`).</span><span class="sxs-lookup"><span data-stu-id="059ba-119">The decrement operator is supported in two forms: the postfix decrement operator, `x--`, and the prefix decrement operator, `--x`.</span></span>

### <a name="postfix-decrement-operator"></a><span data-ttu-id="059ba-120">Постфиксный оператор уменьшения</span><span class="sxs-lookup"><span data-stu-id="059ba-120">Postfix decrement operator</span></span>

<span data-ttu-id="059ba-121">Результатом `x--` является значение `x` *перед* выполнением операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="059ba-121">The result of `x--` is the value of `x` *before* the operation, as the following example shows:</span></span>

[!code-csharp-interactive[postfix decrement](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#PostfixDecrement)]

### <a name="prefix-decrement-operator"></a><span data-ttu-id="059ba-122">Префиксный оператор декремента</span><span class="sxs-lookup"><span data-stu-id="059ba-122">Prefix decrement operator</span></span>

<span data-ttu-id="059ba-123">Результатом `--x` является значение `x` *после* выполнения операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="059ba-123">The result of `--x` is the value of `x` *after* the operation, as the following example shows:</span></span>

[!code-csharp-interactive[prefix decrement](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#PrefixDecrement)]

## <a name="unary-plus-and-minus-operators"></a><span data-ttu-id="059ba-124">Операторы унарного плюса и минуса</span><span class="sxs-lookup"><span data-stu-id="059ba-124">Unary plus and minus operators</span></span>

<span data-ttu-id="059ba-125">Унарный оператор `+` возвращает значение полученного операнда.</span><span class="sxs-lookup"><span data-stu-id="059ba-125">The unary `+` operator returns the value of its operand.</span></span> <span data-ttu-id="059ba-126">Унарный оператор `-` изменяет знак операнда на противоположный.</span><span class="sxs-lookup"><span data-stu-id="059ba-126">The unary `-` operator computes the numeric negation of its operand.</span></span>

[!code-csharp-interactive[unary plus and minus](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#UnaryPlusAndMinus)]

<span data-ttu-id="059ba-127">Унарный оператор `-` не поддерживает тип [ulong](../keywords/ulong.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-127">The unary `-` operator doesn't support the [ulong](../keywords/ulong.md) type.</span></span>

## <a name="multiplication-operator-"></a><span data-ttu-id="059ba-128">Оператор умножения \*</span><span class="sxs-lookup"><span data-stu-id="059ba-128">Multiplication operator \*</span></span>

<span data-ttu-id="059ba-129">Оператор умножения `*` вычисляет произведение операндов:</span><span class="sxs-lookup"><span data-stu-id="059ba-129">The multiplication operator `*` computes the product of its operands:</span></span>

[!code-csharp-interactive[multiplication operator](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#Multiplication)]

<span data-ttu-id="059ba-130">Унарный оператор `*` представляет собой [оператор косвенного обращения к указателю](multiplication-operator.md#pointer-indirection-operator).</span><span class="sxs-lookup"><span data-stu-id="059ba-130">The unary `*` operator is a [pointer indirection operator](multiplication-operator.md#pointer-indirection-operator).</span></span>

## <a name="division-operator-"></a><span data-ttu-id="059ba-131">Оператор деления /</span><span class="sxs-lookup"><span data-stu-id="059ba-131">Division operator /</span></span>

<span data-ttu-id="059ba-132">Оператор деления `/` делит первый операнд на второй.</span><span class="sxs-lookup"><span data-stu-id="059ba-132">The division operator `/` divides its first operand by its second operand.</span></span>

### <a name="integer-division"></a><span data-ttu-id="059ba-133">Деление целых чисел</span><span class="sxs-lookup"><span data-stu-id="059ba-133">Integer division</span></span>

<span data-ttu-id="059ba-134">Для операндов цельночисленных типов результат оператора `/` является целочисленным типом, который равен частному двух операндов, округленному в сторону нуля:</span><span class="sxs-lookup"><span data-stu-id="059ba-134">For the operands of integer types, the result of the `/` operator is of an integer type and equals the quotient of the two operands rounded towards zero:</span></span>

[!code-csharp-interactive[integer division](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerDivision)]

<span data-ttu-id="059ba-135">Чтобы получить частное двух операндов в виде числа с плавающей запятой, используйте тип `float`, `double` или `decimal`:</span><span class="sxs-lookup"><span data-stu-id="059ba-135">To obtain the quotient of the two operands as a floating-point number, use the `float`, `double`, or `decimal` type:</span></span>

[!code-csharp-interactive[integer as floating-point division](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerAsFloatingPointDivision)]

### <a name="floating-point-division"></a><span data-ttu-id="059ba-136">Деление чисел с плавающей запятой</span><span class="sxs-lookup"><span data-stu-id="059ba-136">Floating-point division</span></span>

<span data-ttu-id="059ba-137">Для типов `float`, `double` и `decimal` результатом оператора `/` является частное двух операндов:</span><span class="sxs-lookup"><span data-stu-id="059ba-137">For the `float`, `double`, and `decimal` types, the result of the `/` operator is the quotient of the two operands:</span></span>

[!code-csharp-interactive[floating-point division](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointDivision)]

<span data-ttu-id="059ba-138">Если один из операндов — это `decimal`, второй операнд не может быть ни `float`, ни `double`, так как ни `float`, ни `double` не преобразуется неявно в тип `decimal`.</span><span class="sxs-lookup"><span data-stu-id="059ba-138">If one of the operands is `decimal`, another operand can be neither `float` nor `double`, because neither `float` nor `double` is implicitly convertible to `decimal`.</span></span> <span data-ttu-id="059ba-139">Необходимо явным образом преобразовать операнд `float` или `double` в тип `decimal`.</span><span class="sxs-lookup"><span data-stu-id="059ba-139">You must explicitly convert the `float` or `double` operand to the `decimal` type.</span></span> <span data-ttu-id="059ba-140">Дополнительные сведения о неявных числовых преобразованиях см. в [таблице неявных числовых преобразований](../keywords/implicit-numeric-conversions-table.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-140">For more information about implicit conversions between numeric types, see [Implicit numeric conversions table](../keywords/implicit-numeric-conversions-table.md).</span></span>

## <a name="remainder-operator-"></a><span data-ttu-id="059ba-141">Оператор остатка %</span><span class="sxs-lookup"><span data-stu-id="059ba-141">Remainder operator %</span></span>

<span data-ttu-id="059ba-142">Оператор остатка `%` вычисляет остаток от деления первого операнда на второй.</span><span class="sxs-lookup"><span data-stu-id="059ba-142">The remainder operator `%` computes the remainder after dividing its first operand by its second operand.</span></span>

### <a name="integer-remainder"></a><span data-ttu-id="059ba-143">Целочисленный остаток</span><span class="sxs-lookup"><span data-stu-id="059ba-143">Integer remainder</span></span>
  
<span data-ttu-id="059ba-144">Для целочисленных операндов результатом `a % b` является значение, произведенное `a - (a / b) * b`.</span><span class="sxs-lookup"><span data-stu-id="059ba-144">For the operands of integer types, the result of `a % b` is the value produced by `a - (a / b) * b`.</span></span> <span data-ttu-id="059ba-145">Знак ненулевого остатка такой же, как и у первого операнда, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059ba-145">The sign of the non-zero remainder is the same as that of the first operand, as the following example shows:</span></span>

[!code-csharp-interactive[integer remainder](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerRemainder)]

<span data-ttu-id="059ba-146">Используйте метод <xref:System.Math.DivRem%2A?displayProperty=nameWithType> для вычисления результатов как целочисленного деления, так и определения остатка.</span><span class="sxs-lookup"><span data-stu-id="059ba-146">Use the <xref:System.Math.DivRem%2A?displayProperty=nameWithType> method to compute both integer division and remainder results.</span></span>

### <a name="floating-point-remainder"></a><span data-ttu-id="059ba-147">Остаток с плавающей запятой</span><span class="sxs-lookup"><span data-stu-id="059ba-147">Floating-point remainder</span></span>

<span data-ttu-id="059ba-148">Для операндов типа `float` и `double` результатом `x % y` для конечных `x` и `y` будет значение `z`, так что:</span><span class="sxs-lookup"><span data-stu-id="059ba-148">For the `float` and `double` operands, the result of `x % y` for the finite `x` and `y` is the value `z` such that</span></span>

- <span data-ttu-id="059ba-149">знак `z`, если отлично от нуля, совпадает со знаком `x`;</span><span class="sxs-lookup"><span data-stu-id="059ba-149">The sign of `z`, if non-zero, is the same as the sign of `x`.</span></span>
- <span data-ttu-id="059ba-150">абсолютное значение `z` является значением, произведенным `|x| - n * |y|`, где `n` — это наибольшее возможное целое число, которое меньше или равно `|x| / |y|`, а `|x|` и `|y|` являются абсолютными значениями `x` и `y`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="059ba-150">The absolute value of `z` is the value produced by `|x| - n * |y|` where `n` is the largest possible integer that is less than or equal to `|x| / |y|` and `|x|` and `|y|` are the absolute values of `x` and `y`, respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="059ba-151">Этот метод вычисления остатка аналогичен тому, который использовался для целочисленных операндов, но отличается от IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="059ba-151">This method of computing the remainder is analogous to that used for integer operands, but differs from the IEEE 754.</span></span> <span data-ttu-id="059ba-152">Если вам нужна операция остатка, которая соответствует IEEE 754, используйте метод <xref:System.Math.IEEERemainder%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="059ba-152">If you need the remainder operation that complies with the IEEE 754, use the <xref:System.Math.IEEERemainder%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="059ba-153">Сведения о поведение оператора `%` в случае неконечных операндов см. в разделе [Оператор остатка](~/_csharplang/spec/expressions.md#remainder-operator) [спецификации языка C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-153">For information about the behavior of the `%` operator with non-finite operands, see the [Remainder operator](~/_csharplang/spec/expressions.md#remainder-operator) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="059ba-154">Для операндов `decimal` оператор остатка `%` эквивалентен [оператору остатка](<xref:System.Decimal.op_Modulus(System.Decimal,System.Decimal)>) типа <xref:System.Decimal?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="059ba-154">For the `decimal` operands, the remainder operator `%` is equivalent to the [remainder operator](<xref:System.Decimal.op_Modulus(System.Decimal,System.Decimal)>) of the <xref:System.Decimal?displayProperty=nameWithType> type.</span></span>

<span data-ttu-id="059ba-155">В следующем примере показано поведение оператора остатка для операндов с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="059ba-155">The following example demonstrates the behavior of the remainder operator with floating-point operands:</span></span>

[!code-csharp-interactive[floating-point remainder](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointRemainder)]

## <a name="addition-operator-"></a><span data-ttu-id="059ba-156">Оператор сложения +</span><span class="sxs-lookup"><span data-stu-id="059ba-156">Addition operator +</span></span>

<span data-ttu-id="059ba-157">Оператор сложения `+` вычисляет сумму своих операндов:</span><span class="sxs-lookup"><span data-stu-id="059ba-157">The addition operator `+` computes the sum of its operands:</span></span>

[!code-csharp-interactive[addition operator](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#Addition)]

<span data-ttu-id="059ba-158">Кроме того, оператор `+` можно использовать для объединения строк и делегатов.</span><span class="sxs-lookup"><span data-stu-id="059ba-158">You also can use the `+` operator for string concatenation and delegate combination.</span></span> <span data-ttu-id="059ba-159">Дополнительные сведения см. в статье [Оператор `+`](addition-operator.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-159">For more information, see the [`+` operator](addition-operator.md) article.</span></span>

## <a name="subtraction-operator--"></a><span data-ttu-id="059ba-160">Оператор вычитания -</span><span class="sxs-lookup"><span data-stu-id="059ba-160">Subtraction operator -</span></span>

<span data-ttu-id="059ba-161">Оператор вычитания `-` вычитает второй операнд из первого:</span><span class="sxs-lookup"><span data-stu-id="059ba-161">The subtraction operator `-` subtracts its second operand from its first operand:</span></span>

[!code-csharp-interactive[subtraction operator](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#Subtraction)]

<span data-ttu-id="059ba-162">Кроме того, оператор `-` можно использовать для удаления делегатов.</span><span class="sxs-lookup"><span data-stu-id="059ba-162">You also can use the `-` operator for delegate removal.</span></span> <span data-ttu-id="059ba-163">Дополнительные сведения см. в статье [Оператор `-`](subtraction-operator.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-163">For more information, see the [`-` operator](subtraction-operator.md) article.</span></span>

## <a name="operator-precedence-and-associativity"></a><span data-ttu-id="059ba-164">Приоритет и ассоциативность операторов</span><span class="sxs-lookup"><span data-stu-id="059ba-164">Operator precedence and associativity</span></span>

<span data-ttu-id="059ba-165">В следующем списке перечислены арифметические операторы в порядке убывания приоритета:</span><span class="sxs-lookup"><span data-stu-id="059ba-165">The following list orders arithmetic operators starting from the highest precedence to the lowest:</span></span>

- <span data-ttu-id="059ba-166">Постфиксные операторы инкремента `x++` и декремента `x--`.</span><span class="sxs-lookup"><span data-stu-id="059ba-166">Postfix increment `x++` and decrement `x--` operators.</span></span>
- <span data-ttu-id="059ba-167">Префиксные операторы инкремента `++x` и декремента `--x` и унарные операторы `+` и `-`.</span><span class="sxs-lookup"><span data-stu-id="059ba-167">Prefix increment `++x` and decrement `--x` and unary `+` and `-` operators.</span></span>
- <span data-ttu-id="059ba-168">Мультипликативные операторы `*`, `/` и `%`.</span><span class="sxs-lookup"><span data-stu-id="059ba-168">Multiplicative `*`, `/`, and `%` operators.</span></span>
- <span data-ttu-id="059ba-169">Аддитивные операторы `+` и `-`.</span><span class="sxs-lookup"><span data-stu-id="059ba-169">Additive `+` and `-` operators.</span></span>

<span data-ttu-id="059ba-170">Бинарные арифметические операторы имеют левую ассоциативность.</span><span class="sxs-lookup"><span data-stu-id="059ba-170">Binary arithmetic operators are left-associative.</span></span> <span data-ttu-id="059ba-171">То есть операторы с одинаковым приоритетом вычисляются в направлении слева направо.</span><span class="sxs-lookup"><span data-stu-id="059ba-171">That is, operators with the same precedence level are evaluated from left to right.</span></span>

<span data-ttu-id="059ba-172">Порядок вычисления, определяемый приоритетом и ассоциативностью операторов, можно изменить с помощью скобок (`()`).</span><span class="sxs-lookup"><span data-stu-id="059ba-172">Use parentheses, `()`, to change the order of evaluation imposed by operator precedence and associativity.</span></span>

[!code-csharp-interactive[precedence and associativity](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#PrecedenceAndAssociativity)]

<span data-ttu-id="059ba-173">Полный список операторов C#, упорядоченных по уровню приоритета, см. в статье [Операторы C#](index.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-173">For the complete list of C# operators ordered by precedence level, see [C# operators](index.md).</span></span>

## <a name="compound-assignment"></a><span data-ttu-id="059ba-174">Составное присваивание</span><span class="sxs-lookup"><span data-stu-id="059ba-174">Compound assignment</span></span>

<span data-ttu-id="059ba-175">Для бинарного оператора `op` выражение составного присваивания в форме</span><span class="sxs-lookup"><span data-stu-id="059ba-175">For a binary operator `op`, a compound assignment expression of the form</span></span>

```csharp
x op= y
```

<span data-ttu-id="059ba-176">эквивалентно</span><span class="sxs-lookup"><span data-stu-id="059ba-176">is equivalent to</span></span>

```csharp
x = x op y
```

<span data-ttu-id="059ba-177">за исключением того, что `x` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="059ba-177">except that `x` is only evaluated once.</span></span>

<span data-ttu-id="059ba-178">Следующий пример иллюстрирует использование составного присваивания с арифметическими операторами:</span><span class="sxs-lookup"><span data-stu-id="059ba-178">The following example demonstrates the usage of compound assignment with arithmetic operators:</span></span>

[!code-csharp-interactive[compound assignment](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#CompoundAssignment)]

<span data-ttu-id="059ba-179">Вы также можете использовать операторы `+=` и `-=` для подписки и отмены подписки на [события](../keywords/event.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-179">You also use the `+=` and `-=` operators to subscribe to and unsubscribe from [events](../keywords/event.md).</span></span> <span data-ttu-id="059ba-180">Дополнительные сведения см. в разделе [Практическое руководство. Подписка и отмена подписки на события](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).</span><span class="sxs-lookup"><span data-stu-id="059ba-180">For more information, see [How to: subscribe to and unsubscribe from events](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).</span></span>

## <a name="arithmetic-overflow-and-division-by-zero"></a><span data-ttu-id="059ba-181">Арифметическое переполнение и деление на нуль</span><span class="sxs-lookup"><span data-stu-id="059ba-181">Arithmetic overflow and division by zero</span></span>

<span data-ttu-id="059ba-182">Если результат арифметической операции выходит за пределы диапазона возможных конечных значений соответствующего числового типа, поведение арифметического оператора зависит от типа его операндов.</span><span class="sxs-lookup"><span data-stu-id="059ba-182">When the result of an arithmetic operation is outside the range of possible finite values of the involved numeric type, the behavior of an arithmetic operator depends on the type of its operands.</span></span>

### <a name="integer-arithmetic-overflow"></a><span data-ttu-id="059ba-183">Целочисленное арифметическое переполнение</span><span class="sxs-lookup"><span data-stu-id="059ba-183">Integer arithmetic overflow</span></span>

<span data-ttu-id="059ba-184">Деление целого числа на ноль всегда вызывает исключение <xref:System.DivideByZeroException>.</span><span class="sxs-lookup"><span data-stu-id="059ba-184">Integer division by zero always throws a <xref:System.DivideByZeroException>.</span></span>

<span data-ttu-id="059ba-185">В случае целочисленного арифметического переполнения итоговое поведение определяется контекстом проверки переполнения, который может быть [проверяемым или непроверяемым](../keywords/checked-and-unchecked.md):</span><span class="sxs-lookup"><span data-stu-id="059ba-185">In case of integer arithmetic overflow, an overflow checking context, which can be [checked or unchecked](../keywords/checked-and-unchecked.md), controls the resulting behavior:</span></span>

- <span data-ttu-id="059ba-186">Если в проверяемом контексте переполнение возникает в константном выражении, происходит ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="059ba-186">In a checked context, if overflow happens in a constant expression, a compile-time error occurs.</span></span> <span data-ttu-id="059ba-187">В противном случае, если операция производится во время выполнения, возникает исключение <xref:System.OverflowException>.</span><span class="sxs-lookup"><span data-stu-id="059ba-187">Otherwise, when the operation is performed at run time, an <xref:System.OverflowException> is thrown.</span></span>
- <span data-ttu-id="059ba-188">В непроверяемом контексте результат усекается путем удаления старших разрядов, которые не помещаются в целевой тип данных.</span><span class="sxs-lookup"><span data-stu-id="059ba-188">In an unchecked context, the result is truncated by discarding any high-order bits that don't fit in the destination type.</span></span>

<span data-ttu-id="059ba-189">Вместе с [проверяемыми и непроверяемыми](../keywords/checked-and-unchecked.md) операторами вы можете использовать операторы `checked` и `unchecked`, чтобы управлять контекстом проверки переполнения, в котором вычисляется выражение:</span><span class="sxs-lookup"><span data-stu-id="059ba-189">Along with the [checked and unchecked](../keywords/checked-and-unchecked.md) statements, you can use the `checked` and `unchecked` operators to control the overflow checking context, in which an expression is evaluated:</span></span>

[!code-csharp-interactive[checked and unchecked](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#CheckedUnchecked)]

<span data-ttu-id="059ba-190">По умолчанию арифметические операции выполняются в *непроверяемом* контексте.</span><span class="sxs-lookup"><span data-stu-id="059ba-190">By default, arithmetic operations occur in an *unchecked* context.</span></span>

### <a name="floating-point-arithmetic-overflow"></a><span data-ttu-id="059ba-191">Арифметическое переполнение с плавающей запятой</span><span class="sxs-lookup"><span data-stu-id="059ba-191">Floating-point arithmetic overflow</span></span>

<span data-ttu-id="059ba-192">Арифметические операции с типами `float` и `double` никогда не вызывают исключение.</span><span class="sxs-lookup"><span data-stu-id="059ba-192">Arithmetic operations with the `float` and `double` types never throw an exception.</span></span> <span data-ttu-id="059ba-193">Результатом арифметических операций с этими типами может быть одно из специальных значений, представляющих бесконечность и объект, не являющийся числовым:</span><span class="sxs-lookup"><span data-stu-id="059ba-193">The result of arithmetic operations with those types can be one of special values that represent infinity and not-a-number:</span></span>

[!code-csharp-interactive[double non-finite values](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointOverflow)]

<span data-ttu-id="059ba-194">Для операндов типа `decimal` арифметическое переполнение всегда вызывает исключение <xref:System.OverflowException>, а деление на нуль всегда вызывает исключение <xref:System.DivideByZeroException>.</span><span class="sxs-lookup"><span data-stu-id="059ba-194">For the operands of the `decimal` type, arithmetic overflow always throws an <xref:System.OverflowException> and division by zero always throws a <xref:System.DivideByZeroException>.</span></span>

## <a name="round-off-errors"></a><span data-ttu-id="059ba-195">Ошибки округления</span><span class="sxs-lookup"><span data-stu-id="059ba-195">Round-off errors</span></span>

<span data-ttu-id="059ba-196">Из-за общих ограничений, касающихся представления вещественных чисел в форме с плавающей запятой и арифметических операций с плавающей запятой, при вычислениях с использованием типов с плавающей запятой могут возникать ошибки округления.</span><span class="sxs-lookup"><span data-stu-id="059ba-196">Because of general limitations of the floating-point representation of real numbers and floating-point arithmetic, the round-off errors might occur in calculations with floating-point types.</span></span> <span data-ttu-id="059ba-197">То есть полученный результат выражения может отличаться от ожидаемого математического результата.</span><span class="sxs-lookup"><span data-stu-id="059ba-197">That is, the produced result of an expression might differ from the expected mathematical result.</span></span> <span data-ttu-id="059ba-198">В следующем примере показано несколько таких случаев:</span><span class="sxs-lookup"><span data-stu-id="059ba-198">The following example demonstrates several such cases:</span></span>

[!code-csharp-interactive[round-off errors](~/samples/snippets/csharp/language-reference/operators/ArithmeticOperators.cs#RoundOffErrors)]

<span data-ttu-id="059ba-199">Дополнительные сведения см. в заметках на страницах справочника [System.Double](/dotnet/api/system.double#remarks), [System.Single](/dotnet/api/system.single#remarks) или [System.Decimal](/dotnet/api/system.decimal#remarks).</span><span class="sxs-lookup"><span data-stu-id="059ba-199">For more information, see remarks at [System.Double](/dotnet/api/system.double#remarks), [System.Single](/dotnet/api/system.single#remarks), or [System.Decimal](/dotnet/api/system.decimal#remarks) reference pages.</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="059ba-200">Возможность перегрузки оператора</span><span class="sxs-lookup"><span data-stu-id="059ba-200">Operator overloadability</span></span>

<span data-ttu-id="059ba-201">Определяемые пользователем типы могут [перегружать](../keywords/operator.md) унарные (`++`, `--`, `+` и `-`) и бинарные (`*`, `/`, `%`, `+` и `-`) арифметические операции.</span><span class="sxs-lookup"><span data-stu-id="059ba-201">User-defined types can [overload](../keywords/operator.md) the unary (`++`, `--`, `+`, and `-`) and binary (`*`, `/`, `%`, `+`, and `-`) arithmetic operators.</span></span> <span data-ttu-id="059ba-202">При перегрузке бинарного оператора соответствующий оператор составного присваивания также неявно перегружается.</span><span class="sxs-lookup"><span data-stu-id="059ba-202">When a binary operator is overloaded, the corresponding compound assignment operator is also implicitly overloaded.</span></span> <span data-ttu-id="059ba-203">Определяемый пользователем тип не может перегружать оператор составного присваивания явным образом.</span><span class="sxs-lookup"><span data-stu-id="059ba-203">A user-defined type cannot explicitly overload a compound assignment operator.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="059ba-204">Спецификация языка C#</span><span class="sxs-lookup"><span data-stu-id="059ba-204">C# language specification</span></span>

<span data-ttu-id="059ba-205">Дополнительные сведения см. в следующих разделах статьи [Спецификация языка C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="059ba-205">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="059ba-206">Постфиксные операторы инкремента и декремента</span><span class="sxs-lookup"><span data-stu-id="059ba-206">Postfix increment and decrement operators</span></span>](~/_csharplang/spec/expressions.md#postfix-increment-and-decrement-operators)
- [<span data-ttu-id="059ba-207">Префиксные операторы инкремента и декремента</span><span class="sxs-lookup"><span data-stu-id="059ba-207">Prefix increment and decrement operators</span></span>](~/_csharplang/spec/expressions.md#prefix-increment-and-decrement-operators)
- [<span data-ttu-id="059ba-208">Оператор унарного плюса</span><span class="sxs-lookup"><span data-stu-id="059ba-208">Unary plus operator</span></span>](~/_csharplang/spec/expressions.md#unary-plus-operator)
- [<span data-ttu-id="059ba-209">Оператор унарного минуса</span><span class="sxs-lookup"><span data-stu-id="059ba-209">Unary minus operator</span></span>](~/_csharplang/spec/expressions.md#unary-minus-operator)
- [<span data-ttu-id="059ba-210">Оператор умножения</span><span class="sxs-lookup"><span data-stu-id="059ba-210">Multiplication operator</span></span>](~/_csharplang/spec/expressions.md#multiplication-operator)
- [<span data-ttu-id="059ba-211">Оператор деления</span><span class="sxs-lookup"><span data-stu-id="059ba-211">Division operator</span></span>](~/_csharplang/spec/expressions.md#division-operator)
- [<span data-ttu-id="059ba-212">Оператор остатка</span><span class="sxs-lookup"><span data-stu-id="059ba-212">Remainder operator</span></span>](~/_csharplang/spec/expressions.md#remainder-operator)
- [<span data-ttu-id="059ba-213">Оператор сложения</span><span class="sxs-lookup"><span data-stu-id="059ba-213">Addition operator</span></span>](~/_csharplang/spec/expressions.md#addition-operator)
- [<span data-ttu-id="059ba-214">Оператор вычитания</span><span class="sxs-lookup"><span data-stu-id="059ba-214">Subtraction operator</span></span>](~/_csharplang/spec/expressions.md#subtraction-operator)
- [<span data-ttu-id="059ba-215">Составное присваивание</span><span class="sxs-lookup"><span data-stu-id="059ba-215">Compound assignment</span></span>](~/_csharplang/spec/expressions.md#compound-assignment)
- [<span data-ttu-id="059ba-216">Операторы checked и unchecked</span><span class="sxs-lookup"><span data-stu-id="059ba-216">The checked and unchecked operators</span></span>](~/_csharplang/spec/expressions.md#the-checked-and-unchecked-operators)

## <a name="see-also"></a><span data-ttu-id="059ba-217">См. также</span><span class="sxs-lookup"><span data-stu-id="059ba-217">See also</span></span>

- [<span data-ttu-id="059ba-218">Справочник по C#</span><span class="sxs-lookup"><span data-stu-id="059ba-218">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="059ba-219">Руководство по программированию на C#</span><span class="sxs-lookup"><span data-stu-id="059ba-219">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="059ba-220">Операторы в C#</span><span class="sxs-lookup"><span data-stu-id="059ba-220">C# Operators</span></span>](index.md)
- <xref:System.Math?displayProperty=nameWithType>
- <xref:System.MathF?displayProperty=nameWithType>
- [<span data-ttu-id="059ba-221">Числовые значения в .NET</span><span class="sxs-lookup"><span data-stu-id="059ba-221">Numerics in .NET</span></span>](../../../standard/numerics.md)