---
title: Размещение Eleventy на GitHub pages
description: Размещение статического сайта созданного с помощью Eleventy на GitHub pages
date: 2024-12-10
tags: ["eleventy", "github"]
---
[Ссылка](https://quinndombrowski.com/blog/2022/05/07/hosting-eleventy-on-github-pages/) на оригинал статьи.   
Мне очень понравилось создавать сайты с помощью Eleventy вместо Jekyll. Я всё ещё изучаю некоторые из крутых 
возможностей работы с данными, но NodeJS оказался гораздо более приятным в использовании, чем Ruby, и это 
само по себе многого стоит.

Я понимаю, что Netlify сделает хостинг сайтов Eleventy очень простым, но я не хочу добавлять ещё одну платформу 
к набору инструментов, с которыми мне приходится иметь дело, особенно когда я использую GitHub Pages для сайтов 
Jekyll, которые я всё ещё запускаю. Когда я просматривал руководства по хостингу Eleventy на GitHub Pages, я не 
мог заставить работать ни одно из них - всегда было что-то немного не то для моего варианта использования. Но с 
помощью [Кэсси Лоттман](https://www.cassey.dev/) я заставил это работать с моим первым сайтом Eleventy, и с тех 
пор я использовал эту конфигурацию для нескольких других сайтов.

## Общая картина

GitHub Pages предполагает, что вы используете Jekyll, если вы не укажете иное. Вместо использования автоматических 
рабочих процессов GitHub Pages для создания сайтов Jekyll вы будете использовать 
[Github Pages action by Peace Iris](https://github.com/peaceiris/actions-gh-pages), которое может создавать другие виды 
статических сайтов и перемещать их в ветку, где будут размещены файлы HTML. Вам нужно будет добавить несколько новых файлов в ваш репозиторий GitHub, чтобы это произошло.

## Новые файлы в вашем репозитории GitHub

- **Файл .nojekyll**: Откройте текстовый редактор и сохраните пустой файл в корне вашего репозитория (где у вас есть 
*.eleventy.js*) с именем файла *.nojekyll*. Это остановит попытки GitHub создать ваш сайт как сайт Jekyll.
- **Каталог .github**: Создайте новый каталог в корне вашего репозитория и назовите его *.github* (да, начиная с точки). 
Внутри этого каталога создайте каталог с именем *workflows*. Откройте текстовый редактор и сохраните файл в каталоге workflows
с именем *build.yml*. Скопируйте [содержимое из моего файла build.yml сюда](https://github.com/quinnanya/quinnanya.github.io/blob/main/.github/workflows/build.yml).

*Примечание: мой файл build.yml был обновлён 14.06.23 с улучшениями версии Node благодаря Саймону Уайлсу*

В зависимости от настроек Eleventy вам может потребоваться изменить `publish_dir` в файле build.yml. Мой сайт Eleventy 
собирается в папку *dist*. Если ваш сайт собирается в папку с другим именем, измените его в этом файле.

## Конфигурация GitHub

### Создание ветки gh-pages

Используя интерфейс GitHub, вам нужно будет создать новую ветку вашего репозитория под названием *gh-pages*, где будет 
размещена собранная версия вашего сайта. Если вы просматриваете свой репозиторий на GitHub, вы должны увидеть маленькую 
кнопку с надписью *main* в верхнем левом углу под вкладкой *<> Code*. Нажмите эту кнопку, затем введите *gh-pages* в поле 
с надписью *Find or create a branch*. Это создаст новую ветку с надписью *gh-pages*.

### Конфигурация действий (action)

Перейдите в настройки вашего репозитория, нажмите *Actions (Действия)* в наборе вкладок слева, затем *General (Общие)*. 
Убедитесь, что выбрано 
