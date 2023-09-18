# Решение от Артура Пирожкова и Александра Реввы

## Предполагаемая схема сети
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/0f579c2e-7be0-4a92-abac-a87db990b18e)
## Пример адресации
|     Устройство      |     Интерфейс    |     IP               |
|---------------------|------------------|----------------------|
|     CLI             |     To CLI       |     3.3.3.10         |
|     ISP             |     to CLI       |     3.3.3.1          |
|                     |     to HQ-R      |     4.4.4.1          |
|                     |     to BR-R      |     5.5.5.1          |
|     HQ-R            |     to ISP       |     4.4.4.2          |
|                     |     to HQ-SRV    |     192.168.100.1    |
|     BR-R            |     to ISP       |     5.5.5.2          |
|                     |     to BR-SRV    |     172.16.100.1     |
|     HQ-SRV          |     to HQ-R      |     192.168.1.10     |
|     BR-SRV          |     to BR-R      |     172.16.100.10    |

## Модуль 1
### Первоначальная настройка ISP
### Задание "А"
Монтируем диск demo2024.iso (он находится по пути \\R406-PC14 ). Затем выполняем команды ниже и пишем любое название для нашего диска
#### ISP
```ISP
apt-cdrom add
nano /etc/apt/sources.list
```
Комментируем строчку с репозиторием астры, оставляем наш диск
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d585a88-0694-47d3-b559-940b07d93131)<br>
Устанавливаем пакеты
#### ISP
```ISP
apt update
apt install network-manager openssh-server -y
nano /etc/sysctl.conf
```
Убираем комментарий со строки<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/716ede2a-3fb6-4b43-9299-95c72709bb67)<br>
Переходим в network-manager командой:
#### ISP
```ISP
nmtui
```
Меняем в зависимости от названия нашего устройства<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/de5788ae-3520-4936-8ce3-c31ed2016d13)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/49078755-20eb-44c3-af64-f90f0d38ce8d)<br>

Переходим в любое соединение и смотрим куда он смотрит (обязательно проверяем совпадение MAC Address), в данном случае интерфейс смотрит в сторону ISP<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/10e4a99d-8a5b-48d7-960b-aa8e4c7184c8)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/3abbfefb-e724-42cc-bf39-688295295eda)<br>

Выбираем ручную конфигурацию Ipv4 и указываем IP адрес нашего устройства, не забываем про шлюз. В данном случае мы конфигурируем один из интерфейсов в сторону ISP
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/d182671c-c0d1-4383-b1fe-a1fee9232e5e)

### Первоначальная настройка HQ-R

Монтируем диск demo2024.iso (он находится по пути \\R406-PC14 ). Затем выполняем команды ниже и пишем любое название для нашего диска
#### HQ-R
```HQ-R
apt-cdrom add
nano /etc/apt/sources.list
```
Комментируем строчку с репозиторием астры, оставляем наш диск
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d585a88-0694-47d3-b559-940b07d93131)<br>
Устанавливаем пакеты
#### HQ-R
```HQ-R
apt update
apt install network-manager openssh-server frr isc-dhcp-server -y
nano /etc/sysctl.conf
```
Убираем комментарий со строки<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/716ede2a-3fb6-4b43-9299-95c72709bb67)<br>
Переходим в network-manager командой:
#### HQ-R
```HQ-R
nmtui
```
Меняем в зависимости от названия нашего устройства<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/de5788ae-3520-4936-8ce3-c31ed2016d13)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/49078755-20eb-44c3-af64-f90f0d38ce8d)<br>

Переходим в любой соединение и смотрим куда он смотрит (обязательно проверяем совпадение MAC Address), в данном случае интерфейс  смотрит в сторону ISP<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/10e4a99d-8a5b-48d7-960b-aa8e4c7184c8)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/3abbfefb-e724-42cc-bf39-688295295eda)<br>

Выбираем ручную конфигурацию Ipv4 и указываем IP адрес нашего устройства, не забываем про шлюз. В данном случае мы конфигурируем один из интерфейсов в сторону ISP
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/d182671c-c0d1-4383-b1fe-a1fee9232e5e)

### Первоначальная настройка BR-R

Монтируем диск demo2024.iso (он находится по пути \\R406-PC14 ). Затем выполняем команды ниже и пишем любое название для нашего диска
#### BR-R
```BR-R
apt-cdrom add
nano /etc/apt/sources.list
```
Комментируем строчку с репозиторием астры, оставляем наш диск
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d585a88-0694-47d3-b559-940b07d93131)<br>
Устанавливаем пакеты
#### BR-R
```BR-R
apt update
apt install network-manager openssh-server frr -y
nano /etc/sysctl.conf
```
Убираем комментарий со строки<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/716ede2a-3fb6-4b43-9299-95c72709bb67)<br>
Переходим в network-manager командой:
#### BR-R
```BR-R
nmtui
```
Меняем в зависимости от названия нашего устройства<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/de5788ae-3520-4936-8ce3-c31ed2016d13)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/49078755-20eb-44c3-af64-f90f0d38ce8d)<br>

Переходим в любой соединение и смотрим куда он смотрит (обязательно проверяем совпадение MAC Address), в данном случае интерфейс  смотрит в сторону ISP<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/10e4a99d-8a5b-48d7-960b-aa8e4c7184c8)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/3abbfefb-e724-42cc-bf39-688295295eda)<br>

Выбираем ручную конфигурацию Ipv4 и указываем IP адрес нашего устройства, не забываем про шлюз. В данном случае мы конфигурируем один из интерфейсов в сторону ISP
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/d182671c-c0d1-4383-b1fe-a1fee9232e5e)

### Первоначальная настройка HQ-SRV

Монтируем диск demo2024.iso (он находится по пути \\R406-PC14 ). Затем выполняем команды ниже и пишем любое название для нашего диска
#### HQ-SRV
```HQ-SRV
apt-cdrom add
nano /etc/apt/sources.list
```
Комментируем строчку с репозиторием астры, оставляем наш диск
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d585a88-0694-47d3-b559-940b07d93131)<br>
Устанавливаем пакеты
#### HQ-SRV
```HQ-SRV
apt update
apt install network-manager openssh-server -y
nmtui
```
Выбираем ручную конфигурацию Ipv4 и указываем IP адрес нашего устройства, не забываем про шлюз.<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d1133cf-cd68-4c09-9670-963bc0b0083e)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/d182671c-c0d1-4383-b1fe-a1fee9232e5e)

### Первоначальная настройка BR-SRV

Монтируем диск demo2024.iso (он находится по пути \\R406-PC14 ). Затем выполняем команды ниже и пишем любое название для нашего диска
#### BR-SRV
```BR-SRV
apt-cdrom add
nano /etc/apt/sources.list
```
Комментируем строчку с репозиторием астры, оставляем наш диск
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/8d585a88-0694-47d3-b559-940b07d93131)<br>
Устанавливаем пакеты
#### BR-SRV
```BR-SRV
apt update
apt install network-manager openssh-server -y
nmtui
```
Выбираем ручную конфигурацию Ipv4 и указываем IP адрес нашего устройства, не забываем про шлюз.<br>
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/c6c21f5c-f034-4726-ba91-a210fd2b94d8)
![изображение](https://github.com/nevazno00/demo2024_astra/assets/67695125/d182671c-c0d1-4383-b1fe-a1fee9232e5e)
