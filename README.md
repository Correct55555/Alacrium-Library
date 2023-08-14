# Alacrium-Library

Здесь описаны все функции библиотеки Alacrium-Library. (документация)
** ! - Если вы не проксидел/читодел/кодер на php; c; можете не читать эту запись, она создана для тех, кто хочет разобраться в этом **

### Подключение библиотеки к php

Рассмотрим пример с банальной функции в php
$lib = FFI::cdef("
extern startProxy(char* address);
//и другие функции...
", "./libalacrium.so");
Дальше, можно использовать функции библиотеки как в стандартном php ($lib->startProxy("example.com:19132";)

## Функции библиотеки

Здесь описаны все функции которая дает библиотека

startProxy(char* address)
Дает возможность запуска прокси на указанный сервер

spoofDeviceOS(int os)
Дает возможность спуфа DeviceOS (default: 0)

spoofDeviceModel(char* model)
Дает возможность спуфа DeviceModel (default: "unkown")

spoofInputMode(int mode)
Дает возможность спуфа InputMode (default: 0)

setClientPiqHandler(void(*fn)(const int piq))
Дает возможность поставить хендлер-функцию piq от клиента

setServerPiqHandler(void(*fn)(const int piq))
Дает возможность поставить хендлер-функцию piq от сервера

sendToClient(char* buffer, int length)
Дает возможность отправку баффера клиенту

sendToServer(char* buffer, int length)
Дает возможность отправку баффера серверу

convertPiq(int piq)
Дает возможность конвертирования piq в привичный тип (описаны ниже)

## Piq

Скажу сразу, все функции импортируются как выше

### Типы при конвертировании:

Lib::UnkownPiq - ?
  Lib::TextPiq - Отправляется когда игрок написал что-то в чат, или ему (зависит откуда он получен)
  Принимает: getTextMessage(), getTextType()
  Lib::DisconnectPiq - Отправляется когда игрока кикнули (только в Server?)
  Принимает: getDisconnectReason()
  Lib::StartGamePiq - Отправляется когда игрок начал игру (только в Server)
  Принимает: getEntityRuntimeID(), getEntityUniqueID()
