# media-monitor

Возможные варианты переосмысления, имеющейся реализации [Media Analytics](https://nlp.iict.kz/):
1. Аналог [ALEM MEDIA MONITORING](https://alem.kz/product-1/), сервиса, направленного на:

    > Полный контроль информационного поля, включая СМИ (Интернет, телевидение, радио, газеты) и социальные медиа

    > Управление репутацией, контроль имиджа, повышение эффективности связи с общественностью

    > Принятие правильных управленческих решений, основанных на достоверных фактах

    > Гибкая конфигурация отчетов и аналитических записок
    
    1) Обработку входящего NER реквеста с формированием отчета об освещаемости входящей сущности, и тональной окраске

2. Сервис по поиску наиболее релевантного в плане интеграции, инфлюэнсера (блогера) из пространства: YouTube, Instagram, Facebook, итд. Пайплайн примерно следующий:

    1) Парсинг соц-сетей, формирование корпуса с привязкой непосредственно к блогеру
    2) Тематическая модель корпуса, представление его в пространстве "контенто-тем". Тем самым мы через топик-эмбеддинг, определяем причастность непосредственно блогера к "контенто-теме"
    3) Модель, которая будет получать признаковое описание бизнеса, и выдавать наиболее релевантную "контенто-тему".
