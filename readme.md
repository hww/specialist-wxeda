# Реализация ПК Специалист 

Реализация для отладочной платы AX4010 ALINX, основана на [specialist-wxeda](https://github.com/andykarpov/specialist-wxeda).

![AX4010.jpg](/docs/AX4010.jpg)

### Назначение клавиш на плате

- KEY1 - рестарт

### Видео режимы

Из-за отсутствия на этой плате переключателей, не поддерживаются переключение устройства отображения, выбираемые комбинациями переключателей, как на DE1.
Поэтому значения этих кнопок нужно задавать программно в коде spec_top путем записи в соответствующие регистр SW[1:0].

| Значение SW[1:0] | Режим | Описание |
|---------------|-------------------|---------------------|
| 00 | VGA | |
| 10 | Компонентный YPbPr576p50 | **R**-Pr, **G**-Y, **B**-Pb _только при компиляции варианта по умолчанию, с VGA 50 Гц_ |
| 01 или 11 | Copmosite-Video и S-Video | **R**-Composite, **G**-Y_SVideo, **B**-С_SVideo) |

Для черно белого телевизора можно использовать сигнал Y_SVideo.

### Для загрузки программы с SD

1. Посте старта, нажате на клавишу **F1**, затем **ENTER**
2. Затем ввести комманду ```GD000```, это должно запустить операционную систему. 

В операционной системе имеются следующие команды:

DIR - Просмотр файлов в текущем директории
СD - Смена текужего директория

Для запускает _rks_ файлов требуется ввести имя файла как команду системы. Скачать _rks_ файлы можно тут по ссылке [http://emu80.org/dl.html](http://emu80.org/dl.html).

### Тестирование

Для проверки правильности цветопередачи можно использовать приложенный файл *test8c.rks*. Он рисует стандартные цветные полосы: белый, желтый, голубой, зеленый, пурпурный, красный, синий, черный.

### 56Гц

Следует учитывать то, что не все VGA мониторы поддерживают 50Гц развертку, поэтому можно скомпилировать проект с ```&#92;define FR56HZ``` в spec.v, это активирует режимом VGA 56 Гц. В режиме 56Гц не будет доступен компонентный выход (т.к. режим это нестандартный режим). 

После смены режима требуется однократная подстройка монитора. При автоматической или ручной подстройке монитора можно использовать приложенный *border.rks*. Это приложение рисует рамку, ограничивающую активную область изображения.

### Тип процессора

Тип процессора можно сменит в файле spec.v. Однако для процессора Vslava не поддерживается турбо-режим.

