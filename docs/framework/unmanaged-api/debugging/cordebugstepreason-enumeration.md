---
title: Перечисление CorDebugStepReason
ms.date: 03/30/2017
api_name:
- CorDebugStepReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugStepReason
helpviewer_keywords:
- CorDebugStepReason enumeration [.NET Framework debugging]
ms.assetid: fe248069-b33c-48e1-a777-06ac9b239c54
topic_type:
- apiref
ms.openlocfilehash: 288d7bfdf18be5cef032227c537032966fa68df4
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795707"
---
# <a name="cordebugstepreason-enumeration"></a>Перечисление CorDebugStepReason
Указывает результат отдельного шага.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
typedef enum CorDebugStepReason {  
    STEP_NORMAL,  
    STEP_RETURN,  
    STEP_CALL,  
    STEP_EXCEPTION_FILTER,  
    STEP_EXCEPTION_HANDLER,  
    STEP_INTERCEPT,  
    STEP_EXIT  
} CorDebugStepReason;  
```  
  
## <a name="members"></a>Участники  
  
|Участник|Описание|  
|------------|-----------------|  
|`STEP_NORMAL`|Пошаговое завершение нормального выполнения в одной и той же функции.|  
|`STEP_RETURN`|Пошаговое продолжение обычно после возвращения функции.|  
|`STEP_CALL`|Пошаговое продолжение обычно в начале вновь вызванной функции.|  
|`STEP_EXCEPTION_FILTER`|Было создано исключение, и управление было передано в фильтр исключений.|  
|`STEP_EXCEPTION_HANDLER`|Было создано исключение, а Управление было передано обработчику исключений.|  
|`STEP_INTERCEPT`|Элемент управления передан перехватчику.|  
|`STEP_EXIT`|Поток завершил работу до завершения шага.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Метод StepComplete](icordebugmanagedcallback-stepcomplete-method.md)
- [Перечисления отладки](debugging-enumerations.md)
