# Домашнее задание к занятию  «Защита хоста» Константин Чумаков

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

1. Установите **eCryptfs**.
2. Добавьте пользователя cryptouser.
3. Зашифруйте домашний каталог пользователя с помощью eCryptfs.


*В качестве ответа  пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.*  

### Решение 1 
Устанавливаю пакет   
```
 sudo apt-get install ecryptfs-utils
```

Добавляю пользователя в систему:
```
sudo adduser encrypt-home crypto
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/1.png)   

Захожу под созданным пользователем, создаю два тестовых файла.   
Проверяю шифрование. Данные файлы не видны под другим пользователем.
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/2.png)   



### Задание 2

1. Установите поддержку **LUKS**.
2. Создайте небольшой раздел, например, 100 Мб.
3. Зашифруйте созданный раздел с помощью LUKS.

*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*

### Решение 2    

Устанавливаю LUKS
```
sudo apt install cryptsetup
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/4.png)   

Создаю раздел 100Mb c помощью утилиты fdisk и шифрую его:
```
sudo cryptsetup -y -v --type luks2 luksFormat /dev/sdb1
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/5.png)

Монтирую созданный раздел:
```
sudo cryptsetup luksOpen /dev/sdb1 disk
ls /dev/mapper/disk
```
Форматирую созданный раздел:
```
sudo dd if=/dev/zero of=/dev/mapper/disk
sudo mkfs.ext4 /dev/mapper/disk
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/6.png)    

Создаю скрытую директорию и подключаю к ней диск:
```
mkdir .secret
sudo mount /dev/mapper/disk .secret/
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/7.png)     

Завершаю работу:
```
sudo umount .secret
sudo cryptsetup luksClose disk
```
![alt text](https://github.com/BudyGun/safe-pc/blob/main/images/8.png)   



## Дополнительные задания (со звёздочкой*)

Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале

### Задание 3 *

1. Установите **apparmor**.
2. Повторите эксперимент, указанный в лекции.
3. Отключите (удалите) apparmor.


*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*



