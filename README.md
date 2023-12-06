# Домашнее задание к занятию «ELK»


### Задание 1. Elasticsearch 

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty'', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.


### Задание 1. Elasticsearch

### Решение 1

*Скриншот запущенных контейнеров Elasticsearch, Kibana, Logstash*

![Commit Task1](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task1p1.png)


*Скриншот выполнения команды 'curl -u elastic:test -X GET 'localhost:9200/_cluster/health?pretty''*

![Commit Task1](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task1p2.png)


---

### Задание 2. Kibana

Установите и запустите Kibana.

*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.


### Решение 2

*Скриншот выполнения команды 'GET /_cluster/health?pretty' в консоли Kibana*

![Commit Task2](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task2p1.png)


---

### Задание 3. Logstash

Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.*


### Решение 3


В данном решении Logstash сам выступает сборщиком логов для передачи их в Kibana.
Для этих целей в конфигурации NGINX логи настраиваются для передечи в формате syslog
в виде потока данны:


![Commit Task3](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task3p0.png)


Настройка конфигурации Logstash в формате json:

'''

	input {
  	    syslog {
    	    port => 5044
	}
	}

'''



*Запрос картинки в NGINX*

![Commit Task3](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task3p1.png)

*Скриншот логов полученных с Logstash. Логи Logstash получает в формате syslog от NGINX напрямую*

![Commit Task3](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task3p2.png)


---

### Задание 4. Filebeat. 

Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.*


### Решение 4


В данном решении Logstash получает логи от сбощика логов Filebeat для передачи их в Kibana.
Для этих целей в конфигурации NGINX настраиваются логи для сохранения в файл:

![Commit Task4](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task4p0.png)


Настройка конфигурации Logstash в формате json:

'''

	input {
	  beats {
    	port => 5044
	}
	}

'''


*Скриншот логов полученных с Logstash. Логи NGINX Logstash получает от Filebeat*

![Commit Task4](https://github.com/AndrewZnamenskiy/ELK/blob/main/img/task4p1.png)



