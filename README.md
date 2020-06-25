# About

Система медиа-мониторинга, покрывающая целый ряд задач:

- Парсинг ресурсов,в том числе и конфигурируемый Spider (<b>Scrapy</b>) 
- Хранение (<b>Redis, PostgreSQL, Elasticsearch</b>)
- Обработка данных (<b>PyMorphy2, NLTK, Gensim</b>) 
- Построение тематических моделей (<b>LDA, BigARTM, ETM</b>), в том числе и динамических (<b>Custom DTM, DETM</b>)
- Классификация документов по множеству критериев (<b>Personal insights, Custom Bayes Model</b>)
- Визуализация. (<b>Django, HTML+CSS+JS, Plotly, MapBox</b>)
- Автоматические формирование отчетов. (<b>LaTex</b>)

# Architecture

![architecture](https://i.ibb.co/BtRjSmy/arch.jpg)

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

    1) Парсинг соц-сетей, формирование корпуса с привязкой непосредственно к блогеру
    2) Тематическая модель корпуса, представление его в пространстве "контенто-тем". Тем самым мы через топик-эмбеддинг, определяем причастность непосредственно блогера к "контенто-теме"
    3) Модель, которая будет получать признаковое описание бизнеса, и выдавать наиболее релевантную "контенто-тему".
