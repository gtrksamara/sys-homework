# Домашнее задание к занятию "`Что такое DevOps. СI/СD`" - `Корнилов Андрей`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Задание 1
Что нужно сделать:

Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
Установите на машину с jenkins golang.
Используя свой аккаунт на GitHub, сделайте себе форк репозитория. В этом же репозитории находится дополнительный материал для выполнения ДЗ.
Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта go test . и docker build ..
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.



![menu](https://github.com/gtrksamara/sys-homework/blob/main/img/menu.jpg)
![menu2](https://github.com/gtrksamara/sys-homework/blob/main/img/menu2.jpg)
![console_output](https://github.com/gtrksamara/sys-homework/blob/main/img/console_output.jpg)
![console_output2](https://github.com/gtrksamara/sys-homework/blob/main/img/console-output2.jpg)


---

### Задание 2

Создайте новый проект pipeline.
Перепишите сборку из задания 1 на declarative в виде кода.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.



![pipe](https://github.com/gtrksamara/sys-homework/blob/main/img/pipe.jpg)
![outpipe](https://github.com/gtrksamara/sys-homework/blob/main/img/outpipe.jpg)
![outpipe2](https://github.com/gtrksamara/sys-homework/blob/main/img/outpipe2.jpg)


---

### Задание 3

Задание 3
Что нужно сделать:

Установите на машину Nexus.
Создайте raw-hosted репозиторий.
Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
Загрузите файл в репозиторий с помощью jenkins.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.



1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода
pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://192.168.1.108:8081' 
        NEXUS_REPO = 'my_repo' 
        NEXUS_CREDENTIALS_ID = 'admin:password' 
    }

    stages {
        stage('Clone') {
            steps {
                git url:'https://github.com/AndreyTest010/sdvps-materials.git', branch:'main'  
            }
        }

        stage('Build') {
            steps {
                sh 'go build -o myapp .' 
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    def fileToUpload = 'myapp'  
                    def nexusCredentials = "${NEXUS_CREDENTIALS_ID}"
                    sh """
                        curl -v --user $nexusCredentials --upload-file ${fileToUpload} ${NEXUS_URL}/repository/${NEXUS_REPO}/${fileToUpload}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Build and upload to Nexus completed successfully!'
        }
        failure {
            echo 'Build or upload failed.'
        }
    
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

