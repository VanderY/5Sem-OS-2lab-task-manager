## 2 лабараторная по ОС вариант диспетчер процессов

```
Написать диспетчер процессов, который бы постоянно держал в памяти указанное количество экземпляров заданного
(командной строкой) приложения. В случае, если экземпляр приложения работает более заданного времени,
то диспетчер должен принудительно завершить данный экземпляр приложения. Диспетчер должен выставлять себе
приоритет выше, чем приоритет запускаемых приложений. Вывод приложений должен игнорироваться.
При завершении основной программы завершить дочерние процессы
```


Всё завязано на мьютексах, при каждом изменении в состояниях процессов выводится на экран лог.

Скедулер просто гоняет нон-стоп каждые 100 миллисекунд, чекает чтобы время существования потока не было больше заданного, если больше заданного то он его
дестроит и отправляет сигнал логгеру, который выкидывает всю тучу приколов тебе в лицо.

Ну в целом всё, всего получается 3 потока (мейн логгер и скедулер) + все те, которые в тредпуле валяются до истечения времени.

     condition_variable cv;
     mutex m;                     <- Во эти три красавца, которые заставляют всю эту ----- работать.
     bool threadPoolChanged;             (на самом деле тут всё на магии, while(true) и ифах работает)

В методе вроде описаны типы CV и мьютексов, прочитаешь не сложно вроде.

гуд лак

