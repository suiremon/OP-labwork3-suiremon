[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12444699&assignment_repo_type=AssignmentRepo)
# Лабораторная работа 3

## Задача

Реализовать упрощенную [модель песчаной кучи](https://en.wikipedia.org/wiki/Abelian_sandpile_model), которая позволяет сохранять свои состояния в картинку в [формате BMP](https://en.wikipedia.org/wiki/BMP_file_format).

Изначальное состояние задается входным файлом.

Размер сетки может изменяться в процессе работы программы.

Реализация - консольное приложение, поддерживающее следующие аргументы командной строки:

  **-i, --input**    - [tsv-файл](https://en.wikipedia.org/wiki/Tab-separated_values) (tab-separated values) c начальными данными

  **-o, --output**   - путь к директории для сохранения картинок

  **-m, --max-iter** - максимальное количество итераций модели

  **-f, --freq**     - частота, с которой должны сохранятся картинки (если 0, то сохраняется только последнее состояние)

## Начальное состояние

Начальное состояние задается файлом со значением количества песчинок в каждой ячейке, кроме пустых. Размер сетки следует рассчитать на основании этих данных - минимальный прямоугольник в который попадают все ячейки.

Формат файла:
Каждая строчка содержит информацию об одной ячейке, в виде (x-координаты, y-координаты, количество песчинок), разделенных символом табуляции. Количество песчинок гарантированно влезет в `uint64_t`, координаты гарантированно влезают в `int16_t`

## Примечания к модели

1. Новые песчинки добавляются только при инициализации.

2. Состояние следующего поколения ячеек зависит только от предыдущего состояния сетки.

3. В случае если песчинки пытаются обвалиться за границу сетки, ее размер увеличивается на 1 в соответствующую сторону.

## Результат работы - программа

Программа должна пересчитывать состояние модели согласно начальным данным, а также сохранять промежуточные состояния с заданной частотой в виде картинки в формате bmp.

Картинка для текущего состояния формируется по следующим правилам:

1. Размер картинки равен размеру поля.

2. Каждый пиксель соответствует ячейке поля.

3. Цвет пикселя зависит от количества песчинок в ячейке.

    + 0 - белый
    + 1 - зеленый
    + 2 - желтый
    + 3 - фиолетовый
    + \> 3 - черный

4. Кодирование 1 пикселя должно занимать не более 4 бит.

Программа должна закончить свою работу в случае если модель достигла стабильного состояния, либо номера заданной изначально итерации.

## Ограничения

1. Пользовать сторонними библиотеками, кроме стандартной, запрещено. В частности это означает, что Вы должны *сами* спроектировать и реализовать функции для работы с картинками в формате bmp.

2. Использование контейнеров стандартной библиотеки (`std::vector`, `std::list` и тд) - запрещено.

## Примечание

1. Для реализации Вам может пригодиться [библиотека](https://en.cppreference.com/w/cpp/filesystem) для работы с файловой системой из стандартной библиотеки.
2. В данной лабе Вам дано только описание. Структура проекта и организация сборки также ваша задача. Использовать для сборки не cmake - запрещено.
3. Важно помнить, что размер структуры может быть не равен сумме размеров ее полей за счет [выравнивания](https://en.cppreference.com/w/c/language/object). Данную проблему можно решить за счет [директив препроцессора](https://en.cppreference.com/w/cpp/preprocessor/impl).

## Deadline

1. 31.10.23 24:00 - 0.8
2. 07.11.23 24:00 - 0.65
3. 14.11.23 24:00 - 0.5

Данная работа оценивается 15 баллами.
