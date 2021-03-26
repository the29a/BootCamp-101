# Шорткаты

Есть много шорткатов, которые мы можем использовать, чтобы упростить и ускорить работу с Linux. После того, как мы ознакомимся с наиболее важными из них и сделаем их привычкой, мы сэкономим много времени на вводе текста. Некоторые из них даже помогут нам избежать использования мыши в терминале.
Автозаполнение

[TAB] - запускает автозаполнение. Это предложит нам различные варианты на основе предоставленного нами STDIN. Это могут быть конкретные предложения, такие как каталоги в нашей текущей рабочей среде, команды, начинающиеся с того же количества символов, которое мы уже набрали, или параметры.
Движение курсора

[CTRL] + A - переместить курсор в начало текущей строки.

[CTRL] + E - переместить курсор в конец текущей строки.

[CTRL] + [←] / [→] - переход к началу текущего / предыдущего слова.

[ALT] + B / F - переход назад / вперед на одно слово.
Стереть текущую строку

[CTRL] + U - стереть все от текущей позиции курсора до начала строки.

[Ctrl] + K - стереть все от текущей позиции курсора до конца строки.

[Ctrl] + W - стереть слово, предшествующее позиции курсора.
Вставить стертое содержимое

[Ctrl] + Y - вставляет стертый текст или слово.
Завершает задачу

[CTRL] + C - Завершает текущую задачу / процесс, отправляя сигнал SIGINT. Например, это может быть сканирование, выполняемое инструментом. Если мы наблюдаем за сканированием, мы можем остановить его / остановить этот процесс с помощью этого ярлыка. Пока не настроен и не разработан используемым нами инструментом. Процесс будет остановлен без запроса подтверждения.
Конец файла (EOF)

[CTRL] + D - закрыть канал STDIN, также известный как конец файла (EOF) или конец передачи.
Очистить терминал

[CTRL] + L - очищает терминал. Альтернативой этому ярлыку является команда clear, которую вы можете ввести, чтобы очистить наш терминал.
Справочная информация о процессе

[CTRL] + Z - приостановить текущий процесс, отправив сигнал SIGTSTP.
Поиск в истории команд

[CTRL] + R - поиск в истории команд ранее введенных команд, соответствующих нашим шаблонам поиска.

[↑] / [↓] - переход к предыдущей / следующей команде в истории команд.
Переключение между приложениями

[ALT] + [TAB] - переключаться между открытыми приложениями.
Увеличить

[CTRL] + [+] - увеличить.

[CTRL] + [-] - Уменьшить.