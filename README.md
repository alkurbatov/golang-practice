# golang-practice

Набор практических заданий для изучения языка `Go`.
В рамках цикла заданий обучающийся создаст свой сервис для управления
личной книжной библиотекой.

> :construction: Задания рассчитаны на разработчиков уровня Middle и выше.
Если вы только начинаете изучать `Go`, воспользуйтесь любым из курсов по
основам языка, например [Основы Go](https://practicum.yandex.ru/go-basics/)
от `Yandex` (~30 часов).

## Задания

- [Задание 1 (Hello world)](./tasks/1.md)
- [Задание 2 (Управление библиотекой)](./tasks/2.md)
- [Задание 3 (Контроль качества кода)](./tasks/3/3.md)
- [Задание 4 (Конфигурирование и сохранение состояния)](./tasks/4.md)
- [Задание 5 (Логирование)](./tasks/5.md)

## Как проходит code review

Для проведения ревью кода и более аккуратного донесения смысла комментариев
(например, критичность дефекта, необходимость доработки, стилистические
особенности) используются ключевые слова из списка
[Conventional comments](https://conventionalcomments.org/).

## Материалы для ознакомления

- [Awesome Go][awesome-go] - хороший список библиотек и проектов по Go. Подойдет
  для быстрого поиска популярной реализации инструментов для решения задачи.

- [100 ошибок Go и как их избежать][100-go-errors] - подробное описание самых
  популярных ошибок при написании программ на языке `Go`.

- [Go101][go-101] - набор онлайн книг по `Go` на разные темы.

- [Чистый код, Роберт Мартин][clean-code] - классическая и горячо обсуждаемая
  книга о написании хорошего и поддерживаемого кода.

- [Чистая архитектура, Роберт Мартин][clean-architecture] - книга описывает как
  строить архитектуру приложения для достижения наибольшей гибкости и упрощения
  внесения изменений.

[awesome-go]: https://github.com/avelino/awesome-go
[clean-architecture]: https://www.chitai-gorod.ru/product/chistyy-kod-sozdanie-analiz-i-refaktoring-2231825
[clean-code]: https://www.chitai-gorod.ru/product/chistaya-arhitektura-iskusstvo-razrabotki-programmnogo-obespecheniya-2640391
[100-go-errors]: https://www.chitai-gorod.ru/product/100-oshibok-go-i-kak-ih-izbezhat-3004794
[go-101]: https://go101.org/

## Консультации

Этот курс бесплатен и находится открытом доступе, но для более полного изучения
языка и ревью предлагаемых решений вам понадобится ментор. Запросить консультацию
у автора этого курса можно через платформу
[GetMentor.dev](https://getmentor.dev/mentor/aleksandr-kurbatov-3515)

## Решение проблем с Docker

В случае невозможности скачать образы `Docker` (например, в связи с блокировкой
российских IP-адресов) необходимо использовать `VPN` или один из следующих
`proxy`:

- [timeweb.cloud](https://dockerhub.timeweb.cloud/)
- [huecker](https://huecker.io/)
