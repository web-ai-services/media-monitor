# About
```
@article{26583204_325243423_2019, 
    author = {Vladimir Barakhnin and Olga Kozhemyakina and Ravil Mukhamediev and Yulia Borzilova and Kirill Yakunin}, 
    keywords = {natural language processing, streaming word processing, text analysis information systemdevelopment of a text corpus processing system},
    title = {The design of the structure of the software system for processing text document corpus},
    year = {2019},
    number = {4 Vol.13},
    pages = {60-72},
    url = {https://bijournal.hse.ru/en/2019--4 Vol.13/325243423.html},
}
```

Система медиа-мониторинга, покрывающая целый ряд задач:

- Парсинг ресурсов,в том числе и конфигурируемый Spider (<b>Scrapy</b>) 
- Хранение (<b>Redis, PostgreSQL, Elasticsearch</b>)
- Обработка данных (<b>PyMorphy2, NLTK, Gensim</b>) 
- Построение тематических моделей (<b>LDA, BigARTM, ETM</b>), в том числе и динамических (<b>Custom DTM, DETM</b>)
- Классификация документов по множеству критериев (<b>Personal insights, Custom Bayes Model</b>)
- Визуализация. (<b>Django, HTML+CSS+JS, Plotly, MapBox</b>)
- Автоматические формирование отчетов. (<b>LaTex</b>)

# Architecture

Все компоненты системы организованы в виде Docker-контейнеров. Такая реализация обеспечивает работу подсистем в виде независимых компонентов, каждый из которых возможно заменить при необходимости.

<div align="center">
    <img src=https://i.ibb.co/BtRjSmy/arch.jpg" >
    <p>Architecture</p>
</div>

<b>Airflow</b> выступает в роли основного <b>data-driver</b>, на нем в первую очередь реализована логика парсинга новостных медиа-ресурсов,конфигурируемый Spider(<b>Scrapy</b>) позволяет не опускаться до анализа реализации каждого ресурса. Далее, с помощью все того же __Airflow__, спарсенные данные, складывается в 
<b>PostgreSQL</b>, который выполняет роль персистентного хранилища для структурированных данных. Его использование обусловлено широкими возможностями данной реляционной БД (среди свободно распространяемых продуктов). После промежуточных расчетов, модификаций и построения моделей, некоторые данные переносятся в <b>ElasticSearch</b>, которое выступает как основное хранилище для кэширования определённых результатов вычислений, необходимых для построения дашбордов и отчётов в системе. Данные прошедшие полный pipeline по подготовке, напрямую используются в __Web__ части проекта.

# Interface
![geo](https://i.imgur.com/cdWbEnj.jpg)
![dashboard](https://i.imgur.com/I1IFM5a.jpg)
__Дашборды__ - это наборы виджетов (карточек-визуализаций), наиболее репрезентативная и гибкая часть системы, вся вышеуказанная визуализация может быть минимизирована и собрана в рамках одного дашборда. Дашборд может формироваться в зависимости от потребностей заказчика и __не нуждается в дополнительной разработке__, так как пользователю доступен функционал выбора *Объектов мониторинга*, где на внутреннем языке запросов ```1(Банк) AND 2(1(Gold) $ 1(Kaspi | Каспийский | Каспи))```, формируется фильтрация к корпусу, тем самым образуя релевантный корпус новостей, для которого строится тематическая модель и дальнейшая аналитика по распределению источников, динамики различных критериев, статистики по наиболее и наименее репрезентативным новостям, поиск инфоповодов и гео-аналитика.

# Perspectives
Возможные варианты переосмысления, имеющейся реализации [Media Analytics](https://nlp.iict.kz/):
1. Аналог [ALEM MEDIA MONITORING](https://alem.kz/product-1/), сервиса, направленного на:

    > Полный контроль информационного поля, включая СМИ (Интернет, телевидение, радио, газеты) и социальные медиа

    > Управление репутацией, контроль имиджа, повышение эффективности связи с общественностью

    > Принятие правильных управленческих решений, основанных на достоверных фактах

    > Гибкая конфигурация отчетов и аналитических записок
    
    ___
    ##### Вкратце
    Обработка входящего NER реквеста с формированием отчета об освещаемости входящей сущности, тональной окраске. Составление KPI рекламных компаний, регулирование PR отделов, сравнение с конкурентами итд.

2. Сервис по поиску наиболее релевантного в плане интеграции, инфлюэнсера (блогера) из пространства: YouTube, Instagram, Facebook, итд. Ближайший похожий сервис это [GetBlogger](https://getblogger.ru/). Пайплайн примерно следующий:

    > Парсинг соц-сетей, формирование корпуса с привязкой непосредственно к блогеру
    
    > Тематическая модель корпуса, представление его в пространстве "контенто-тем". Тем самым мы через топик-эмбеддинг, определяем причастность непосредственно блогера к "контенто-теме"
    
    > Модель, которая будет получать признаковое описание бизнеса, и выдавать наиболее релевантную "контенто-тему".
