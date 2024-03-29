1. Подробный гайд по Git для новичков
Сегодня поговорим о системе контроля версий — Git (читается как ГИТ).

Без знания и понимания этого инструмента невозможно быть программистом. Само собой, для постоянной работы не нужно держать в голове все команды и возможности. Нужно знать набор команд, которые помогут понимать все, что происходит.

Основы Git
Git — это распределенная система контроля версий нашего кода. Зачем она нам? Для команды нужна какая-то система управления работы. Она нужна, чтобы отслеживать изменения, которые происходят со временем.

То есть шаг за шагом мы видим, какие файлы изменились и как. Особенно это важно, когда анализируешь, что было проделано в рамках одной задачи: это дает возможность возвращаться назад.

Представим себе ситуацию: был работающий код, всё в нем было хорошо, но мы решили что-то улучшить или подправить. Все ничего, но такое улучшение поломало половину функционала, сделало невозможным работу. И что дальше? Без Гита нужно было бы часами сидеть и вспоминать, как же все было изначально. А так мы просто откатываемся на коммит назад — и все.

Или что делать, если есть два разработчика, которые делают одновременно свои изменения в коде? Без Гита это выглядит так: они скопировали код из оригинала, сделали что нужно. Наступает момент, и оба хотят добавить свои изменения в главную папку. И что делать в этой ситуации?..

Таких проблем не будет вовсе, если пользоваться Гитом.

Немного теории
Чтобы быть в теме, желательно добавить в свое обращение несколько новых слов и действий… А то говорить будет не о чем. Конечно, это некий жаргон и калька с английского, поэтому я буду добавлять значения на английском.

Какие слова и действия?

гит репозиторий (git repository);
коммит (commit);
ветка (branch);
смерджить (merge);
конфликты (conflicts);
спулить (pull);
запушить (push);
как игнорировать какие-то файлы (.gitignore).
И так далее.

Состояния в Git
У Гита есть несколько состояний, которые нужно понять и запомнить:

неотслеживаемое (untracked);
измененное (modified);
подготовленное (staged);
закомиченное (committed).
Как это понимать?
Это состояния, в которых находятся файлы из нашего кода. То есть, их жизненный путь обычно выглядит так:

Файл, который создан и не добавлен в репозиторий, будет в состоянии untracked.
Делаем изменения в файлах, которые уже добавлены в гит репозиторий — находятся в состоянии modified.
Из тех файлов, которые мы изменили, выбираем только те (или все), которые нужны нам (например, скомпилированные классы нам не нужны), и эти классы с изменениями попадают в состояние staged.
Из заготовленных файлов из состояния staged создается коммит и переходит уже в гит репозиторий. После этого staged состояние — пустое. А вот modified еще может что-то содержать.

Что такое коммит
Коммит — это основной объект в управлении контроля версий. Он содержит все изменения за время этого коммита. Коммиты связаны между собой как односвязный список.

А именно: есть первый коммит. Когда создается второй коммит, то он (второй) знает, что идет после первого. И таким образом можно отследить информацию.

Также у коммита есть еще своя информация, так называемые метаданные:

уникальный идентификатор коммита, по которому можно его найти;
имя автора коммита, который создал его;
дата создания коммита;
комментарий, который описывает, что было сделано во время этого коммита.
Работа с репозиторием
Полезные горячие клавиши
Чтобы дальше работать, нужно запомнить несколько очень полезных горячих клавиш:

ctrl + t — получить последние изменения с удаленного репозитория (git pull).
ctrl + k — сделать коммит/посмотреть все изменения, которые есть на данный момент. Сюда входят и untracked, и modified файлы (git commit).
ctrl + shift + k — это команда для создания пуша изменений на удаленный репозиторий. Все коммиты, которые были созданы локально и еще не находятся на удаленном, будут предложены для пуша (git push).
alt + ctrl + z — откатить в конкретном файле изменения до состояния последнего созданного коммита в локальном репозитории. Если в левом верхнем углу выделить весь проект, то можно будет откатить изменения всех файлов.
Что мы хотим?
Нам для работы нужно освоить базовый сценарий, который используется везде.

Стоит задача реализовать новую функциональность в отдельной ветке и запушить ее на удаленный репозиторий (дальше нужно создать еще пул-реквест на главную ветку, но это выходит за рамки нашей лекции).

Что для этого нужно сделать?

Получить все изменения на текущий момент в основной ветке (master, например).

На базе этой основной создать отдельную для своей работы.

Реализовать новую функциональность.

Перейти на основную ветку и проверить, не было ли новых изменений за время, пока работали. Если не было, то все хорошо, а если было, то делаем следующее: переходим на работающую ветку и делаем ребейз изменений из основной ветки в нашу. Если все прошло успешно, то отлично. Но вполне могут быть и конфликты. И их как раз можно будет заранее решить, не тратя время на удаленном репозитории.

Казалось бы, зачем это делать? Это правило хорошего тона, которое предотвращает возникновение конфликтов уже после пуша своей ветки на локальный репозиторий (есть, конечно, вероятность,что все равно они будут, но она становится значительно меньше).

Запушить свои изменения на удаленный репозиторий.

Как получить изменения с удаленного сервера
Мы добавили описание в README новым коммитом и хотим эти изменения получить. Предлагается выбор между мерджем и ребейзом в случае, если были сделаны изменения и в локальном репозитории и на удаленном. Выбираем мерж.