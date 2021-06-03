# Дополнительное задание ШРИ по теме "Асинхронность" (rxjs)

Вам дан файл [index.html](https://github.com/stromov/shri-rxjs-hw/blob/master/index.html) в котором с cdn подключена библиотека rxjs (версия 7.1.0), написаны стили, а также присутсвуют элементы: инпут, два div-контейнера и кнопка. В конце тега body, в теге script присутствует функция getApiResponse, которая эмулирует ответ некоторого API: принимает на вход строку, а возвращает Promise, который будет переведён в состояние resolved через случайное время (от 0.5 секунды до 5 секунд).

[Ссылка](https://rxjs.dev/guide/overview) на документацию к билиотеке rxjs версии 7.1.0.

```js
const {foo} = rxjs; // пример импорта функционала из rxjs
const {bar} = rxjs.operators; // пример импорта функционала из rxjs/operators
```

Результат разместить на отдельной страничке и выложить её на GitHub Pages.


## Задание 1

В теге script файла index.html нужно (с использованием функционала библиотеки rxjs) добавить кнопке с id "button" следующий функционал: при нажатии на кнопку должно очищаться поле ввода инпута и пропадать текст из div-контейнеров "response-container" и "cancel-prev-request-container".

## Задание 2

В теге script файла index.html нужно создать стрим, из событий изменения значения инпута, а также написать (с использованием функционала библиотеки rxjs) и вызвать функцию resolveCancelRequest, внутри которой будет создаваться подписка на стрим, и, на каждое изменение значения в инпуте, будет эмулироваться запрос к API через функцию getApiResponse. Причём, если запрос не успел выполниться до начала нового, то старый запрос должен быть отменён. Результат последнего выполненного запроса должен быть записан в контейнер с id "cancel-prev-request-container".

Например, мы ввели в инпут строку "42". У нас отправился запрос со строкой "4", а затем со строкой "42". При этом, если запрос со строкой "4" не был разрезолвен раньше отправки запроса со строкой "42", то запрос со строкой "4" должен быть отменён, а в контейнере с id "cancel-prev-request-container" должна быть отображена только строка "42".
## Задание 1

В теге script файла index.html нужно использовать стрим, созданный во втором задании, а также написать (с использованием функционала библиотеки rxjs) и вызвать функцию resolveRaceCondition, внутри которой будет создаваться подписка на стрим, и, на каждое изменение значения в инпуте, будет эмулироваться запрос к API через функцию getApiResponse. Каждый ответ должен обрабатываться и записываться в контейнер с id "response-container", но только при условии, что длина новой полученной строки больше, чем длина предыдущей полученной строки.

Например, мы вводим и инпут строку "test". Мы должны эмулировать запрос к API с каждой из подстрок "t", "te", "tes" и "test". В ответах будем получать те же подстроки, но их порядок будет не гарантирован, допустим, что полученные Promise будут переведены в состояние resolved в таком порядке: первым будет Promise со значением "te", вторым со значением "t", третьим со значением "test" и четвёртым со значением "tes". Тогда в контейнере с id "response-container" должны последовательно появится строки "te" и "test", а строки "t" и "tes" должны быть проигнорированы.
