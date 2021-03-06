---
title: "Целевые платформы | Документация Майкрософт"
description: "Сведения о целевых платформах для приложений и библиотек .NET Core."
keywords: .NET, .NET Core, framework, TFM
author: richlander
ms.author: mairaw
ms.date: 04/27/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6ef56a2e-593d-497b-925a-1e25bb6df2e6
ms.translationtype: Machine Translation
ms.sourcegitcommit: 45835eb80642253f80ea630ae9db1ac766b72b9c
ms.openlocfilehash: 11c1f11e4f8354b7573d03e680cf4a8a16fa26d9
ms.contentlocale: ru-ru
ms.lasthandoff: 05/11/2017

---

# <a name="target-frameworks"></a>Требуемые версии .NET Framework

*Платформы* определяют объекты, методы и средства, которые можно использовать для создания приложений и библиотек. Платформа .NET Framework используется для создания приложений и библиотек, в первую очередь для выполнения на компьютерах с операционной системой Windows. .NET Core включает платформу, которая позволяет создавать приложения и библиотеки, которые выполняются на разных операционных системах.

Термин *платформа* может имеет разные значения в зависимости от контекста. Например, .NET Core может упоминаться как "платформа .NET Core" в контексте создания приложений и библиотек или в контексте среды, в которой выполняется код приложения и библиотеки. Термин *вычислительная платформа* описывает *где и как* выполняется приложение. Поскольку .NET Core выполняет код в среде [.NET Core Common Language Runtime (CoreCLR)](https://github.com/dotnet/coreclr), то также может именоваться платформой. Это же справедливо и для .NET Framework, которая имеет среду CLR ([Common Language Runtime](clr.md)) для выполнения кода приложений и библиотек, разработанных с использованием объектов, методов и средств платформы .NET Framework. В документации вы будете часто встречать термин "кросс-платформенный", который следует трактовать как "предназначенный для разных операционных систем и архитектур (x86, x64, arm)". Обычно автор использует его именно в этом значении.

Объекты и методы платформ именуются прикладными программными интерфейсами (API). Интерфейсы API используются в [Visual Studio](https://www.visualstudio.com/), [Visual Studio для Mac](https://www.visualstudio.com/vs/visual-studio-mac/), [Visual Studio Code](https://code.visualstudio.com/) и других интегрированных средах разработки (IDE) и редакторах, предоставляя вам правильные наборы объектов и методы для разработки. Также платформы используются [NuGet](https://www.nuget.org/) для создания и применения пакетов NuGet. Это позволяет создавать и использовать подходящие пакеты для целевой платформы вашего приложения или библиотеки.

*Нацеливание на платформу* или на несколько платформ обозначает выбор интерфейсов API и конкретных версий, которые вы будете использовать. Существует несколько способов указывать платформы: по имени продукта, по короткому или длинному имени платформы или по имени семейства.

## <a name="referring-to-frameworks"></a>Ссылки на платформы

Есть несколько способов указывать ссылки на платформы, и большинство из них используются в документации по .NET Core. Например, платформу .NET Framework 4.6.2 можно указывать в следующих форматах:

**Ссылка на продукт**

Можно ссылаться на среду выполнения или платформу .NET. Оба являются одинаково допустимыми.

* .NET Framework 4.6.2
* .NET 4.6.2

**Ссылка на платформу**

Можно ссылаться на платформу или ориентацию на нее с помощью длинных или коротких форм моникера целевой платформы. Оба являются одинаково допустимыми.

* `.NETFramework,Version=4.6.2`
* `net462`

**Ссылка на семейство платформ**

Можно ссылаться на семейство платформ с помощью длинных или коротких форм идентификатора платформы. Оба являются одинаково допустимыми.

* `.NETFramework`
* `net`

## <a name="latest-framework-versions"></a>Последние версии платформ

Приведенная ниже таблица описывает набор платформ, которые можно использовать, способы их указания и реализованные в них версии [библиотеки .NET Standard](library.md). Эти версии платформ являются последними стабильными версиями. Предварительные версии здесь не упоминаются.

| Платформа             | Последняя версия | Моникер целевой платформы (TFM) | Компактный моникер целевой платформы (TFM) | Версия .NET Standard | Метапакет |
| :-------------------: | :------------: | :----------------------------: | :------------------------------------: | :-------------------: | :---------: |
| .NET Standard         | 1.6.1          | .NETStandard,Version=1.6       | netstandard1.6                         | Н/Д                   | [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) |
| Приложение .NET Core | 1.1.1          | .NETCoreApp,Version=1.1        | netcoreapp1.1                          | 1.6                   | [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App) |
| .NET Framework        | 4.6.2          | .NETFramework,Version=4.6.2    | net462                                 | 1.5                   | Н/Д |

## <a name="supported-frameworks"></a>Поддерживаемые платформы

Платформа обычно указывается коротким моникером целевой платформы (*TFM*). В .NET Standard этот метод можно обобщить как *TxM*, чтобы одной ссылкой описать сразу несколько платформ. Клиенты NuGet поддерживают следующие платформы. Эквивалентные обозначения отображаются в скобках (`[]`).

| Имя                       | Сокращение | TFM/TxM                                    |
| -------------------------- | ------------ | -------------------------------------------- |
| .NET Standard              | netstandard  | netstandard1.0                               |
|                            |              | netstandard1.1                               |
|                            |              | netstandard1.2                               |
|                            |              | netstandard1.3                               |
|                            |              | netstandard1.4                               |
|                            |              | netstandard1.5                               |
|                            |              | netstandard1.6                               |
| .NET Core                  | netcoreapp   | netcoreapp1.0                                |
|                            |              | netcoreapp1.1                                |
| .NET Framework             | net          | net11                                        |
|                            |              | net20                                        |
|                            |              | net35                                        |
|                            |              | net40                                        |
|                            |              | net403                                       |
|                            |              | net45                                        |
|                            |              | net451                                       |
|                            |              | net452                                       |
|                            |              | net46                                        |
|                            |              | net461                                       |
|                            |              | net462                                       |
| Магазин Windows              | netcore      | netcore [netcore45]                          |
|                            |              | netcore45 [win, win8]                        |
|                            |              | netcore451 [win81]                           |
| .NET Micro Framework       | netmf        | netmf                                        |
| Silverlight                | sl           | sl4                                          |
|                            |              | sl5                                          |
| Windows Phone              | wp           | wp [wp7]                                     |
|                            |              | wp7                                          |
|                            |              | wp75                                         |
|                            |              | wp8                                          |
|                            |              | wp81                                         |
|                            |              | wpa81                                        |
| Универсальная платформа Windows  | uap          | uap [uap10.0]                                |
|                            |              | uap10.0 [win10] [netcore50]                  |

## <a name="deprecated-frameworks"></a>Устаревшие платформы

Следующие среды являются устаревшими. Пакеты, предназначенные для этих платформ, следует перевести на предлагаемые для замены.

| Устаревшая платформа | Замена |
| -------------------- | ----------- |
| aspnet50             | netcoreapp  |
| aspnetcore50         |             |
| dnxcore50            |             |
| dnx                  |             |
| dnx45                |             |
| dnx451               |             |
| dnx452               |             |
| dotnet               | netstandard |
| dotnet50             |             |
| dotnet51             |             |
| dotnet52             |             |
| dotnet53             |             |
| dotnet54             |             |
| dotnet55             |             |
| dotnet56             |             |
| netcore50            | uap10.0     |
| win                  | netcore45   |
| win8                 | netcore45   |
| win81                | netcore451  |
| win10                | uap10.0     |
| winrt                | netcore45   |

## <a name="precedence"></a>Приоритет

Некоторые платформы являются родственными и совместимыми друг с другом, хотя и не полностью идентичными.

| Платформа                        | Можно использовать   |
| -------------------------------- | --------- |
| Универсальная платформа Windows (uap) | win81     |
|                                  | wpa81     |
|                                  | netcore50 |
| Магазин Windows (win)              | winrt     |
|                                  | winrt45   |

## <a name="net-standard"></a>.NET Standard

[.NET Standard](https://github.com/dotnet/standard) упрощает перекрестные ссылки между платформами, совместимыми на уровне двоичных файлов, позволяя в одной целевой платформе ссылаться на несколько других. Дополнительные сведения см. в статье [о библиотеках .NET Standard](library.md).

[Средство получения ближайшей платформы из набора средств NuGet](http://nugettoolsdev.azurewebsites.net/) имитирует логику NuGet, которая используется для выбора конкретной платформы из нескольких доступных в пакете вариантов в зависимости от платформы проекта. Чтобы использовать это средство, укажите одну платформу для проекта, а также одну или несколько платформ для пакета. Выберите кнопку **Отправить**. Средство сообщит, совместимы ли указанные в списке платформы для пакета с платформой, указанной для проекта.

## <a name="portable-class-libraries"></a>Переносимые библиотеки классов

Сведения о переносимых библиотеках классов см. в разделе [Переносимые библиотеки классов](https://docs.microsoft.com/nuget/schema/target-frameworks#portable-class-libraries) статьи *о требуемой версии .NET Framework* в документации по NuGet. Стивен Клиэри создал средство, которое перечисляет все поддерживаемые PCL. Дополнительные сведения см. в статье [о профилях платформ в среде .NET Framework](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).

