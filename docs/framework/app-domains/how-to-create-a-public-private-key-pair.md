---
title: "Практическое руководство. Создание пары открытого и закрытого ключей | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- key pairs for strong-named assemblies
- signing assemblies
- assemblies [.NET Framework], signing
- cryptographic key pairs
- snk files (key pair files)
- public-private key pairs
- .snk files
- strong-named assemblies, key pairs
ms.assetid: 05026813-f3bd-4d7c-9e0b-fc588eb3d114
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 808b01ae8965de70ac7b141b049b3f6a9f7d94d9
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="how-to-create-a-public-private-key-pair"></a>Практическое руководство. Создание пары открытого и закрытого ключей
Для подписи сборки строгим именем необходимо иметь пару, состоящую из открытого и закрытого ключа. Эта пара криптографических ключей используется во время компиляции для создания сборки со строгим именем. Пару ключей можно создать с помощью [средства для работы со строгими именами (Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md). Файлы пары ключей обычно имеют расширение SNK.  
  
> [!NOTE]
>  В [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] страницы свойств проекта C# и Visual Basic включают вкладку **Подписание**, которая позволяет выбрать существующие файлы ключей или создать новые файлы ключей без использования Sn.exe. В Visual C++ можно указать расположение уже существующего файла ключа на странице свойств **Дополнительно** в разделе **Компоновщик** раздела **Свойства конфигурации** окна **Страницы свойств**. Использование атрибута [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] для идентификации пар файлов ключей признано устаревшим, начиная с <xref:System.Reflection.AssemblyKeyFileAttribute>.  
  
### <a name="to-create-a-key-pair"></a>Создание пары ключей  
  
1.  В командной строке введите следующую команду:  
  
     **sn –k** \<*имя файла*>  
  
     В этой команде *имя файла* — это имя выходного файла, содержащего пару ключей.  
  
 В следующем примере создается пара ключей с именем `sgKey.snk`.  
  
```  
sn -k sgKey.snk  
```  
  
 Если требуется отложить подписание сборки, а также управлять парой ключей целиком (что может потребоваться разве что для тестирования), можно использовать следующие команды для создания пары ключей и извлечения открытого ключа из нее в отдельный файл. Во-первых, создайте пару ключей:  
  
```  
sn -k keypair.snk  
```  
  
 Затем извлеките открытый ключ из пары ключей и скопируйте его в отдельный файл:  
  
```  
sn -p keypair.snk public.snk  
```  
  
 После создания пары ключей необходимо поместить файл в расположение, в котором его смогут найти инструменты создания подписи строгого имени.  
  
 При подписании сборки строгим именем [компоновщик сборок (Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) выполняет поиск файла ключа относительно текущей и выходной папки. При использовании компиляторов, работающих в режиме командной строки, достаточно просто скопировать ключ в текущий каталог, содержащий модули кода.  
  
 При использовании более ранней версии [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], в которой нет вкладки **Подписание** в свойствах проекта, рекомендуемым расположением файла ключа является каталог проекта с атрибутом файла, заданным следующим образом:  
  
 [!code-cpp[AssemblyName_KeyPair#21](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyName_KeyPair/CPP/keyfileattrib.cpp#21)] [!code-csharp[AssemblyName_KeyPair#21](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyName_KeyPair/CS/keyfileattrib.cs#21)] [!code-vb[AssemblyName_KeyPair#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyName_KeyPair/VB/keyfileattrib.vb#21)]  
  
## <a name="see-also"></a>См. также  
 [Создание и использование сборок со строгими именами](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
