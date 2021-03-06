---
title: "Выполнение приложений интрасети с полным доверием | Документы Майкрософт"
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
- full trust, running intranet applications in
- intranet applications, running in full trust
- running intranet applications in full trust
ms.assetid: ee13c0a8-ab02-49f7-b8fb-9eab16c6c4f0
caps.latest.revision: 20
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6f3dc4235c75d7438f019838cb22192f4dc7c41a
ms.openlocfilehash: f80832a0c0220183a7386bb0273e5a11d9eee6df
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="running-intranet-applications-in-full-trust"></a>Выполнение приложений интранета с полным доверием
Начиная с платформы .NET Framework версии 3.5 с пакетом обновления 1 (SP1) приложения и их сборки библиотек можно запускать как сборки с полным доверием из сетевой папки. В сборки, загружаемые из папки в интрасети, автоматически добавляется свидетельство зоны <xref:System.Security.SecurityZone.MyComputer>. Это свидетельство дает таким сборкам тот же набор разрешений (обычно это полное доверие), которым обладают сборки, расположенные на компьютере. Эта функция не относится к приложениям ClickOnce и к приложениям, предназначенным для запуска на узле.  
  
## <a name="rules-for-library-assemblies"></a>Правила для сборок библиотек  
 Указанные ниже правила применяются к сборкам, которые загружаются исполняемым файлом в сетевой папке.  
  
-   Сборки библиотек должны располагаться в той же папке, что и исполняемая сборка. Сборки, расположенные во вложенной папке или в другой папке, не получают полного доверия.  
  
-   Если исполняемый файл загружает сборку с задержкой, то должен использоваться путь, с помощью которого запускался исполняемый файл. Например, если папка \\\\*сетевой_компьютер*\\*папка* сопоставлена с буквой диска и исполняемый файл был запущен по этому пути, сборки, загружаемые исполняемым файлом с использованием сетевого пути, не получат полного доверия. Для загрузки сборки с задержкой в зоне <xref:System.Security.SecurityZone.MyComputer> исполняемый файл должен использовать путь с буквой диска.  
  
## <a name="restoring-the-former-intranet-policy"></a>Восстановление старой политики интрасети  
 В более ранних версиях .NET Framework общие сборки получали свидетельство зоны <xref:System.Security.SecurityZone.Intranet>. Для предоставления сборке из сетевой папки полного доверия нужно было указывать политику управления доступом для кода.  
  
 Новый режим по умолчанию применяется к сборкам из интрасети. Чтобы восстановить старый режим выдачи свидетельства <xref:System.Security.SecurityZone.Intranet>, необходимо задать параметр реестра, который относится ко всем приложениям на компьютере. Эта процедура различается для 32- и 64-разрядных компьютеров.  
  
-   На 32-разрядных компьютерах создайте подраздел в разделе HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework системного реестра. Используйте имя параметра LegacyMyComputerZone и значение 1 типа DWORD.  
  
-   На 64-разрядных компьютерах создайте подраздел в разделе HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework системного реестра. Используйте имя параметра LegacyMyComputerZone и значение 1 типа DWORD. Создайте аналогичный подраздел в разделе HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework.  
  
## <a name="see-also"></a>См. также  
 [Программирование с использованием сборок](../../../docs/framework/app-domains/programming-with-assemblies.md)
