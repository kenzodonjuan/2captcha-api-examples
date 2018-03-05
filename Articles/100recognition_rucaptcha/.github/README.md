# Увеличение скорости распознавания капчи

Один из заказчиков исследовал нестандартное использование нашего сервиса  и написал по нашей просьбе статью о своём исследовании. Приводим её как есть:

Недавно рукапча опубликовала статью о том, как работает их “100% распознавание”: https://rucaptcha.com/blog/for_webmaster/100percent

Если посмотреть на логику работы этого алгоритма, то можно заметить, что при помощи него можно повышать скорость распознавания, что особенно актуально при работе с решением капч “solvemedia”.


Если поставить в настройках:

* Минимальное количество попыток = 2
* Минимальное количество одинаковых ответов = 1

![Настройки](settings.png)

То капча будет выдана сразу двум работникам и как только кто-то из них ответит, его ответ сразу же будет отдан нам.

Для меня важно получить ответ как можно быстрее, поэтому я решил провести тестирование, поможет ли использование “100% распознавания” в ускорении решения капчи и не приведёт ли это к падению качества распознавания?


## Что проверяем:
У меня было два предположения, которые я хотел проверить:

1. При увеличении количества работников, решающих капчу средняя скорость распознавания уменьшается, т.к. повышается вероятность попасть на “быстрого” работника.

2. Количество правильных ответов упадёт, т.к. с вероятностью попасть на “быстрого” работника, у нас должна повыситься и вероятность попадения на работника, который ответит “123” и такой ответ он даст быстрее, чем ответ нормального работника.


## Методика исследования:
Мною написан скрипт на PHP, который с таймаутом в 1 секунду засылает картинки из папки и после получения ID капчи начинает каждую секунду запрашивать ответ. После получения ответа скрипт записывает в лог  имя файла, ID капчи, ответ на неё и время за которое она была распознана.
После этого я 5 раз запускал скрипт с одними и теми же картинками. Первый раз я запустил его с обычными настройками, без “100% распознавания”, второй раз я выставил настройки так, чтобы каждая капча выдавалась двум работника, потом запускал  с настройками чтобы капча выдавалась  3, 4, и 5 работникам.

После этого я собрал все логи в единую таблицу в EXCEL и  посчитал статистику по каждой пачке. 
Для теста я использовал 100 капч вида “solvemedia”. Выбор в пользу этих капч был сделан из-за того, что сейчас это самая сложная капча, по моему мнению. Примеры этой капчи:

![Пример капчи](captcha1.gif)
![Пример капчи](captcha2.gif)

Для тех, кто хочет провести собственный тест скрипт и тестовые капчи доступны в этом репозитории.

Результаты:
[xls файл с данными по каждой капче](rucaptcha100percent.xlsx)

Скриншот итоговой статистики
![Статистика](stats.png)






