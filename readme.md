# Реализация ПК Специалист для отладочной платы AX4010 ALINX


Основана на версии **specIvaGor250215** для Altera DE1, автор **ivagor (Иван Городецкий)**,
---
**Spetsialist_MX_FPGA beta version (31.01.2012)**, Авторы: **Fifan (Виталий Онуфрович), Ewgeny7 (Евгений Иванов), HardWareMan (Игорь Внуков)**
 [www.zx.pk.ru](http://www.zx.pk.ru), [www.spetsialist-mx.ru](http://www.spetsialist-mx.ru)

Использована реализация ("хард" и софт) работы с SD **Дмитрия Целикова (b2m)** [bashkiria-2m.narod.ru](http://bashkiria-2m.narod.ru/)

Использованный PAL-кодер базируется на проекте vector06cc [vector06cc](https://code.google.com/p/vector06cc/)
**Вячеслава Славинского ([svofski](http://sensi.org/~svo)) **
---


### Для загрузки программы с SD

1. Стартует, жмем **F1**, потом **ENTER**
2. GD000
3. Две команды: DIR и СD. Запускает rksы (в формате без имени, можно скачать например здесь - [http://emu80.org/dl.html](http://emu80.org/dl.html))


### Основные служебные кнопки

- S4 - рестарт,
- остальные будут реализованы чуть позднее

Из-за отсутствия на этой плате переключателей, не поддерживаются переключение устройства отображения, выбираемые комбинациями переключателей, как на DE1.
Поэтому значения этих кнопок нужно задавать программно в коде spec_top путем записи в соответствующие регистры.

**SW1:SW0**

- 00-VGA
- 10 (только при компиляции варианта по умолчанию, с VGA 50 Гц)-Компонентный YPbPr576p50 (G-Y,B-Pb,R-Pr)
- 01 или 11 - композит и S-Video (R-композит, G-Y S-Video, B-С S-Video)

Можно взять только Y от S-Video и подключить к обычному ТВ - будет ч/б

### Тестирование
Для проверки правильности цветопередачи можно использовать приложенный файл *test8c.rks*. Он рисует стандартные цветные полосы: белый, желтый, голубой, зеленый, пурпурный, красный, синий, черный.

Не все VGA мониторы поддерживают 50 Гц развертку, поэтому можно откомпилировать (если раскомментировать **`define FR56HZ** в spec.v) с режимом VGA 56 Гц (при этом, как было написано выше, не будет доступен компонентный выход). Т.к. режим нестандартный, потребуется подстройка (один раз, затем монитор запомнит). При подстройке монитора (автоматической или ручной) удобно использовать приложенный файл *border.rks* (рисует рамку, ограничивающую активную область изображения)

Также можно выбрать используемый процессор, смотрите дефайны в начале spec.v
Для процессора Vslava, не поддерживается турбо-режим, при желании можно доработать тактирование.

