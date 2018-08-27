---
title: Отключение поддержки определения DPI в Visual Studio
description: Обсуждает ограничения конструктор Windows Forms на HDPI-мониторах, а также как запустить Visual Studio как процесс не поддерживают DPI.
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 65c997e12aa033b3b08d32c8ab76372e3c52a803
ms.sourcegitcommit: e614e0f3b031293e4107f37f752be43652f3f253
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2018
ms.locfileid: "42936553"
---
# <a name="disable-dpi-awareness-in-visual-studio"></a>Отключение поддержки определения DPI в Visual Studio

Visual Studio является точек на дюйм (DPI) приложения, что означает отображение шкалы автоматически. Если приложение указано, что он не поддерживает определение DPI, операционная система масштабируется приложение в качестве растрового изображения. Это поведение также называется виртуализации точек на ДЮЙМ. Приложение по-прежнему считает, что он выполняется на 100% масштабирования или 96 точек на дюйм.

## <a name="windows-forms-designer-on-hdpi-monitors"></a>Конструктор Windows Forms на HDPI-мониторах

**Конструктор Windows Forms** в Visual Studio не имеет масштабирования. При открытии некоторых форм, в результате проблем с отображением **конструктор Windows Forms** на большое число точек на дюйм (HDPI) мониторов. Например элементы управления могут иметь пересекаются, как показано на следующем рисунке:

![Конструктор Windows Forms на мониторе HDPI](media/disable-dpi-awareness-visual-studio/win-forms-designer-hdpi.png)

В Visual Studio 2017 версии 15,8 и более поздние версии, при открытии формы в **конструктор Windows Forms** на мониторе HDPI, Visual Studio отображает желтый, информационные панели в верхней части конструктора:

![Информационные панели в Visual Studio, чтобы перезагрузить компьютер в режиме не поддерживают DPI](media/disable-dpi-awareness-visual-studio/scaling-gold-bar.png)

Считывает сообщение **масштабирование на главном экране равен 200% (192 dpi). Это может вызвать проблемы отрисовки в окне конструктора.**

Если вы не работают в конструкторе, не требуется для настройки макета формы можно игнорировать информационные панели и продолжить работу в редакторе кода или в других типах конструкторов. Только **конструктор Windows Forms** снижается. Если вам нужно работать в **конструктор Windows Forms**, следующий раздел поможет вам [решить проблему](#to-resolve-the-problem).

## <a name="to-resolve-the-problem"></a>Чтобы устранить эту проблему

Существует три варианта для устранения проблемы отображения.

### <a name="restart-visual-studio-as-a-dpi-unaware-process"></a>Перезапустите Visual Studio как процесс не поддерживают DPI

Как процесс не поддерживают DPI можно перезапустить Visual Studio, выбрав параметр на желтый информационные панели. Это предпочтительный способ устранения проблемы.

При запуске Visual Studio как процесс не поддерживают DPI, устранения проблем макет конструктора, но шрифты могут быть нечеткими. Visual Studio отображает различные желтый информационное сообщение, когда он выполняется как процесс не поддерживают DPI, — говорит **Visual Studio выполняется как процесс не поддерживают DPI. Конструкторы WPF и XAML могут отображаться неправильно.** Информационные панели также предоставляет возможность **перезапустите Visual Studio, как поддерживающее DPI процесс**.

> [!NOTE]
> - Если извлечения окна инструментов в Visual Studio при выборе перезагрузите компьютер как процесс не поддерживают DPI, может измениться положения этих окон инструментов.
> - Если вы используете профиль Visual Basic по умолчанию, или у вас есть **сохранять новые проекты при создании** параметр выбран в **средства** > **параметры**  >  **Проекты и решения**, Visual Studio не удается восстановить проект после его перезапуска, как процесс не поддерживают DPI. Тем не менее, можно открыть проект, выбрав его в разделе **файл** > **последние проекты и решения**.

Очень важно перезапустить Visual Studio как поддерживающее DPI процесс при завершении работы **конструктор Windows Forms**. Когда он выполняется как процесс не поддерживают DPI, можно, выглядели нечеткими шрифты и могут возникнуть проблемы в других конструкторах например **конструктор XAML**. Если вы закроете и снова откройте Visual Studio при работе в режиме не поддерживают DPI, он становится дюйм еще раз. Можно также щелкнуть **перезапустите Visual Studio, как поддерживающее DPI процесс** параметр на информационные панели.

### <a name="add-a-registry-entry"></a>Добавьте параметр реестра

Visual Studio можно пометить как не поддерживающие точек на ДЮЙМ, путем изменения реестра. Откройте **редактора реестра** и добавить запись **NT\CurrentVersion\AppCompatFlags\Layers этот** подраздел:

**Запись**: % ProgramFiles (x86) %\Microsoft Visual Studio\2017\your-edition\Common7\IDE\devenv.exe

**Тип**: REG_SZ

**Значение**: DPIUNAWARE

> [!NOTE]
> Visual Studio остается в режиме не поддерживают DPI, пока вы не удалите запись в реестр.

### <a name="set-your-display-scaling-setting-to-100"></a>Настройте дисплей масштабирование параметр до 100%

Для применения вашего экрана, масштабирование параметр до 100% в Windows 10 введите **параметры отображения** в панели поиска, а затем выберите задач **изменению параметров отображения**. В **параметры** окне **изменить размер текста, приложений и других элементов** для **100%**.

Настройка вашего экрана, масштабирование до 100% может быть нежелательно, так как он может сделать пользовательский интерфейс слишком мал, чтобы можно было использовать.

## <a name="see-also"></a>См. также

- [Автоматическое масштабирование в Windows Forms](automatic-scaling-in-windows-forms.md)