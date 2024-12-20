# Домашнее задание к занятию "Микросервисы: подходы"

---

### Задание 1


Предложите решение для обеспечения процесса разработки: хранение исходного кода, непрерывная интеграция и непрерывная поставка. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.  
Решение должно соответствовать следующим требованиям:  
облачная система;  
- система контроля версий Git;  
- репозиторий на каждый сервис;  
- запуск сборки по событию из системы контроля версий;  
- запуск сборки по кнопке с указанием параметров;  
- возможность привязать настройки к каждой сборке;  
- возможность создания шаблонов для различных конфигураций сборок;  
- возможность безопасного хранения секретных данных (пароли, ключи доступа);  
- несколько конфигураций для сборки из одного репозитория;  
- кастомные шаги при сборке;  
- собственные докер-образы для сборки проектов;  
- возможность развернуть агентов сборки на собственных серверах;  
- возможность параллельного запуска нескольких сборок;  
- возможность параллельного запуска тестов.  
Обоснуйте свой выбор.  

### Ответ:

Я бы предложил GitLab в сочетании с HashiCorp Vault. По мне так это мощное и гибкое решение, которое отвечает всем указанным требованиям.  

 **Обоснование выбора:**

**1) GitLab как основная платформа:**

- Облачная система: GitLab можно развернуть в любом популярном облаке (AWS, GCP, Azure и т.д.), что обеспечивает гибкость и масштабируемость.
- Встроенная система контроля версий Git с возможностью создания неограниченного количества репозиториев.
- Мощная система CI/CD (GitLab CI/CD), которая позволяет настраивать сложные пайплайны с различными триггерами, включая события в VCS и ручной запуск.
- Гибкая система настройки переменных и параметров для каждой сборки.
- Поддержка шаблонов для пайплайнов, что упрощает создание типовых конфигураций.
- Возможность использования Docker-образов, включая собственные, для сборки проектов.
- Гибкая система GitLab Runner для выполнения задач CI/CD, которую можно развернуть на собственных серверах.
- Поддержка параллельного выполнения задач, включая тесты.

**2) HashiCorp Vault для безопасного хранения секретов:**

- Интеграция с GitLab для безопасного хранения и управления конфиденциальными данными.
- Поддерживает различные механизмы аутентификации и авторизации.
- Предоставляет API для программного доступа к конфиденциальным данным.

**Обоснование выбора:**

1) Комплексное решение: GitLab предоставляет единую платформу для управления кодом, CI/CD и совместной работы, что упрощает процессы и снижает накладные расходы на интеграцию различных инструментов.
2) Гибкость и масштабируемость: GitLab можно легко масштабировать в облаке, а также настраивать под конкретные нужды проекта.
3) Безопасность: Интеграция с HashiCorp Vault обеспечивает надежное управление секретами, что критично для безопасности проекта.
4) Поддержка Docker: Возможность использования и создания собственных Docker-образов упрощает процесс сборки и обеспечивает идентичность между различными средами.
5) Автоматизация: Мощная система CI/CD позволяет автоматизировать процессы сборки, тестирования и развертывания.
6) Кастомизация: Возможность создания собственных шагов и использования скриптов в пайплайнах обеспечивает высокую степень гибкости.
7) Параллелизм: Поддержка параллельного выполнения задач повышает эффективность процессов CI/CD.
   
### Задание 2

Предложите решение для обеспечения сбора и анализа логов сервисов в микросервисной архитектуре. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:

- сбор логов в центральное хранилище со всех хостов, обслуживающих систему;
- минимальные требования к приложениям, сбор логов из stdout;
- гарантированная доставка логов до центрального хранилища;
- обеспечение поиска и фильтрации по записям логов;
- обеспечение пользовательского интерфейса с возможностью предоставления доступа разработчикам для поиска по записям логов;
- возможность дать ссылку на сохранённый поиск по записям логов.
Обоснуйте свой выбор.

### Ответ:

Я думаю, что для вышеуказаных требований подходит ELK (Elasticsearch, Logstash, Kibana)  и является хорошим выбором для решения поставленной задачи.  

 **Обоснование выбора:**

 **1) Elasticsearch:**
- Обеспечивает централизованное хранилище для логов.  
- Предоставляет мощные возможности для поиска и фильтрации.  
- Хорошо масштабируется для обработки больших объемов данных.
    
**2) Logstash (или Filebeat):**  
- Собирает логи из различных источников.  
- Обеспечивает гарантированную доставку логов до Elasticsearch.  
- Позволяет преобразовывать и фильтровать логи перед отправкой.
      
**3) Kibana:**  
- Предоставляет удобный пользовательский интерфейс для поиска и анализа логов.  
- Поддерживает создание дашбордов и визуализаций.  
- Позволяет сохранять поисковые запросы и делиться ими через ссылки.  
  
**Обоснование выбора:**  

1) Соответствие требованиям: ELK полностью удовлетворяет всем указанным требованиям.  
2) Минимальное влияние на приложения: Сбор логов из stdout не требует изменений в самих приложениях.  
3) Масштабируемость: ELK хорошо масштабируется для работы с большими объемами данных в микросервисной архитектуре.  
4) Гибкость: Возможность настройки индексов, маппингов и фильтров позволяет адаптировать систему под конкретные нужды.  
5) Популярность и поддержка: Широкое сообщество пользователей, обширная документация и коммерческая поддержка от Elastic.  
6) Интеграция: ELK легко интегрируется с другими инструментами и системами.  
7) Безопасность: Возможность настройки аутентификации и авторизации для доступа к логам.  


### Задание 3

Предложите решение для обеспечения сбора и анализа состояния хостов и сервисов в микросервисной архитектуре. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.
Решение должно соответствовать следующим требованиям:

- сбор метрик со всех хостов, обслуживающих систему;
- сбор метрик состояния ресурсов хостов: CPU, RAM, HDD, Network;
- сбор метрик потребляемых ресурсов для каждого сервиса: CPU, RAM, HDD, Network;
- сбор метрик, специфичных для каждого сервиса;
- пользовательский интерфейс с возможностью делать запросы и агрегировать информацию;
- пользовательский интерфейс с возможностью настраивать различные панели для отслеживания состояния системы.
Обоснуйте свой выбор.

### Ответ:

Я бы предлжил использование в связки Prometheus и Grafana для мониторинга микросервисной архитектуры.
Решение: Prometheus + Grafana + Node Exporter + kube-state-metrics (для Kubernetes)

 **Обоснование выбора:**

**1) Prometheus:**

- Эффективный сбор метрик с различных источников.
- Мощный язык запросов PromQL для анализа данных.
- Поддержка многомерных данных и меток.
- Встроенная система оповещений.

**3) Grafana:**

- Богатый пользовательский интерфейс для визуализации данных.
- Возможность создания настраиваемых дашбордов.
- Поддержка различных источников данных, включая Prometheus.
- Возможность настройки оповещений.

**3) Node Exporter:**

- Сбор системных метрик с хостов (CPU, RAM, HDD, Network).
- Легкая интеграция с Prometheus.

**4) kube-state-metrics (для Kubernetes окружений):**

- Сбор метрик о состоянии объектов Kubernetes.
- Предоставление информации о ресурсах, используемых подами и контейнерами.

**Соответствие требованиям:**

- Сбор метрик со всех хостов: Node Exporter + Prometheus.
- Сбор метрик состояния ресурсов хостов: Node Exporter.
- Сбор метрик потребляемых ресурсов для каждого сервиса: kube-state-metrics (для Kubernetes).
- Пользовательский интерфейс для запросов и агрегации: Grafana + PromQL.
- Настройка панелей мониторинга: Grafana.




















































