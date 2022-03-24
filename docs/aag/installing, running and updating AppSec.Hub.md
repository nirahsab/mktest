# Установка, запуск и обновление AppSec.Hub
## Требования к инфраструктуре

    <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.appsec.android.activity.publicactivity" >
    <application
    android:allowBackup="false"
    android:icon="@drawable/ic_launcher"
    android:label="@string/app_name" >
    <!-- Public Activity -->
    <!-- *** 1 *** Явно указывайте атрибут exported="true" -->
    <activity
    android:name=".PublicActivity"
    android:label="@string/app_name"
    android:exported="true">
    <!-- Обьявление intent фильтра для получения неявных Intent'ов с определённым Action -->
    <intent-filter>
    <action android:name="com.appsec.android.activity.MY_ACTION" />
    <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
    </activity>
    </application>
    </manifest>

asd


    package com.appsec.android.activity.publicactivity;
    import android.app.Activity;
    import android.content.Intent;
    import android.os.Bundle;
    import android.view.View;
    import android.widget.Toast;
    public class PublicActivity extends Activity {
	@Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        
        // *** 2 *** Проводите проверку и безопасную обработку полученного Intent
        // Т.к. это public Activity, то возможно что отправителем Intent'a является вредоносное приложение
        // См.п. "Безопасная обработка входных данных"
		
		String param = getIntent().getStringExtra("PARAM");
    	Toast.makeText(this, String.format("Received param: \"%s\"", param), Toast.LENGTH_LONG).show();
	}
	public void onReturnResultClick(View view) {
		
		// *** 3 *** Не включайте в Intent результата чувствительную информацию
		// Т.к. это public Activity, то возможно что получателем Intent'a будет вредоносное приложение
		Intent intent = new Intent();
		intent.putExtra("RESULT", "Not Sensitive Info");
		setResult(RESULT_OK, intent);
		finish();
	}
    }

!!! example "Например"
    Текст примечания.

        first string
        first string
        second string


!!! note "Примечание"
    Текст примечания.

!!! danger "Опасно"
    Текст предостережения

!!! important "Важно"
    Важное замечание.

!!! danger highlight blink "Не пытайтесь посторить это в домашних условиях"
    Вообще важное замечание.


Установленные для эксплуатации AppSec.Hub технические средства должны быть совместимы между собой и поддерживать сетевой протокол TCP/IP.

Для работы программы в качестве сервера используется компьютер с операционной системой:

* Ubuntu Server 18.04.6 x64.
* Linux CentOS 7 и выше.
* Linux RHEL 7 и выше.

Рекомендуемые технические характеристики серверного оборудования:

* Процессор: 4×CPU 2 ГГц.
* Оперативная память: 16 Гб.
* Свободное дисковое пространство: 150 Гб для размещения прикладных систем и баз данных AppSec.Hub.

ПО поддерживает следующие типы ОС и ПО для полноценного функционирования.

Операционная система|Архитектура|Платформа
----|:----:|----
Linux|64-bit|Ubuntu Server 18.04.6 x64
Linux|64-bit|Centos/RHEL 7 и выше

## Процесс установки
### Проверка инфраструктуры

Дополнительные пакеты, которые необходимо установить на сервере AppSec.Hub перед началом инсталляции AppSec.Hub:

* Docker версии 19.03.3 и выше.
* Docker-compose версии 1.24.1 и выше.

Проверить версию установленных пакетов Docker и Docker-compose можно с помощью команд:

    docker --version
    docker-compose ––version

## Установка AppSec.Hub
Программа AppSec.Hub разворачивается в инфраструктуре с использованием контейнеров Docker.

Настройте соединение с репозиторием, в котором выложен дистрибутив AppSec.Hub:

    docker login cbr-docker-ext-distr-test.nexus-cd.int.yourcompany.ru

Скачайте инсталляционный образ:

    docker pull cbr-docker-ext-distr-test.nexus-cd.int.yourcompany.ru/hub-installer:<version>

Запустите инсталляцию командой:

    docker run -v /hub/install/path:/opt/apphub -ti \
    cbr-docker-ext-distr-test.nexus-cd.int.yourcompany.ru/hub-installer:<version>

где:

* `/hub/install/path` — папка, куда будут скопированы конфигурационные файлы, этот параметр можно поменять, в этом случае мы рекомендуем указать директорий /opt/apphub. При этом содержимое папки, при совпадении имен файлов, будет очищено. В этой же папке будет по умолчанию расположена папка с БД.
* `version` — версия релиза, который необходимо установить.
* В файле `.env` будут сгенерированы пароли и ключи.
* В процессе инсталляции будет предложено ввести URL или IP адрес вашего сервера, по которому будет доступен веб интерфейс AppSec.Hub.
* В процессе инсталляции так же будет предложено внести в базу данных системы демо-данные.

## Запуск AppSec.Hub

В папке `/hub/install/path` выполните команды:

    docker-compose up -d

Подождите примерно 2–3 минуты, пока закончится выполнение этой команды. AppSec.Hub будет доступен через веб-интерфейс по указанному вами URL или IP адресу сервера.

## Остановка AppSec.Hub

В папке `/hub/install/path` выполните команду:

    docker-compose down

## Обновление системы

1. Остановите AppSec.Hub, см. раздел «Остановка AppSec.Hub».
2. Укажите новые версии образов в файле docker-compose.yml.
3. Загрузите новые версии контейнеров из соответствующего репозитория в Nexus CD. Для этого в папке, указанной при установке (см. раздел «Установка AppSec.Hub», по умолчанию /opt/apphub) выполните команду:
    docker-compose pull
4. После загрузки образов запустите систему, см. раздел «Запуск AppSec.Hub».

## Резервное копирование

Для резервного копирования необходимо:

* Остановить AppSec.Hub, см. раздел «Остановка AppSec.Hub».
* Сделать резервную копию директорию установки AppSec.Hub (по умолчанию, /opt/apphub).
* Выполнить резервное копирование директорий, относящихся к docker volumes, но расположенных за пределами директории установки.
* Запустить AppSec.Hub, см. раздел «Запуск AppSec.Hub».

## Восстановление из резервной копии
Для восстановления необходимо проделать следующие шаги:

* Если на сервере ранее был установлен AppSec.Hub:
    1. Остановить AppSec.Hub, см. раздел «Остановка AppSec.Hub».
    2. Переместить или переименовать директорию установки AppSec.Hub (по умолчанию, `/opt/apphub`).
    3. Переместить или переименовать директории, относящиеся к docker volumes, но расположенные за пределами директории установки (если такие имеются).
    4. Восстановить из резервной копии установочную директорию AppSec.Hub (по умолчанию, `/opt/apphub`).
    5. Восстановить из резервной копии директории, относящиеся к docker volumes, но расположенные за пределами директории установки.
    6. Запустить AppSec.Hub, см. раздел «Запуск AppSec.Hub».
* Если на сервере ранее не был установлен AppSec.Hub
    1. Восстановить из резервной копии установочную директорию AppSec.Hub (по умолчанию, `/opt/apphub`).
    2. Восстановить из резервной копии директории, относящиеся к docker volumes, но расположенные за пределами директории установки (если такие имеются).
    3. Запустить AppSec.Hub, см. раздел «Запуск AppSec.Hub».
    
Выполните базовый тест восстановленной установки:

* Авторизация.
* Просмотр списка инструментов, проверка соединения с ними (Test connection).
* Просмотр списка приложений.
* Просмотр результатов сканирования (Issues) и дефектов ИБ (Defects).
* Выборочный запуск DevSecOps пайплайнов.
* Просмотр результатов нового сканирования.

## Настройка антивирусной защиты
На сервере с установленным AppSec.Hub необходимо установить антивирусное программное обеспечение в соответствии с политиками компании в области антивирусной защиты.

--8<-- "includes/abbreviations.md"