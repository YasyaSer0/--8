# МІНІСТЕРСТВО ОСВІТИ І НАУКИ УКРАЇНИ  
## КИЇВСЬКИЙ ФАХОВИЙ КОЛЕДЖ ЗВ’ЯЗКУ  

---

# ЗВІТ  
## про виконання лабораторної роботи №8
### з дисципліни «Операційні системи»

---

**Тема:**  
Збереження службових даних системи та її мережева конфігурація

---

**Виконала:**  
студентка групи **БІКС-33**  
**Сербіна Ярослава Вячеславівна**

---

**Перевірила:**  
**Сушанова Вікторія Сергіївна**

---

**Київ - 2026**

---

# Лабораторна робота №8
## Операційні системи

---

## Тема
Збереження службових даних системи та її мережева конфігурація

---

## Мета роботи
1. Отримання практичних навиків роботи з командною оболонкою Bash.
2. Знайомство з базовими структурами для збереження системних даних - процеси, память, лог-файли  та повідомлення про стан ядра.
3. Знайомство зі стандартом FHS.
4. Знайомство з діями при налаштуванні мережі.

---

## Матеріальне забезпечення занять:
1. ЕОМ типу IBM PC.  
2. ОС сімейства Windows та віртуальна машина VirtualBox (Oracle).  
3. ОС GNU/Linux (будь-який дистрибутив).  
4. Сайт мережевої академії Cisco netacad.com та його онлайн курси по Linux.

---

## Завдання для попередньої підготовки
### Glossary of Basic English Terms

**Kernel - accepts commands from the user and manages processes, providing access to system resources such as memory, disks, and network interfaces.**

**Process - a running program that is managed by the kernel and identified by a process ID (PID).**

**/proc - a pseudo filesystem that provides information about running processes, hardware, and kernel configuration.**

**Pseudo filesystem - a filesystem that appears as real files but exists only in memory, not on disk.**

**/sys - a pseudo filesystem that contains information about hardware devices.**

**/dev - directory that contains special files representing hardware devices.**

**Memory - managed by the kernel and shared between processes using virtual addressing.**

**Virtual memory - uses disk space to extend physical memory and allow processes to access more memory.**

**Kernel space - protected memory area where the kernel code is executed.**

**User space - memory area available for users and applications.**

**free - displays information about memory usage.**

**Log files - files that store messages about system activity, errors, and processes.**

**/var/log - directory where log files are stored.**

**journalctl - used to view logs managed by systemd-journald.**

**dmesg - displays kernel messages from the system startup and runtime.**

**FHS (Filesystem Hierarchy Standard) - defines how files and directories are organized in Linux.**

**Host - a device that communicates via a network with another device.**

**Network - a collection of two or more hosts that are able to communicate with each other.**

**Server - a host that provides a service to another host or client.**

**Client - a host that is accessing a server.**

**Router - a machine that connects hosts from one network to another network.**

**IP address - a unique number assigned to a host on a network.**

**DNS - provides the service of translating domain names into IP addresses.**

**DHCP - defines how network information is assigned to client hosts.**

**Packet - used to send network communication between hosts.**

**ifconfig - used to display network configuration information.**

**ip addr show - displays IP address information and is a modern replacement for ifconfig.**

**route - used to view a table that describes where network packages are sent.**

**ping - used to determine if another machine is reachable.**

**netstat - provides information about network connections and routing.**

**ss - shows socket statistics and network connections.**

**dig - performs queries on the DNS server to determine if information is available.**

**host - associates a hostname with an IP address.**

**ssh - allows connection to another machine and execution of tasks remotely.**

## Відповіді на теоретичні питання

**1. Псевдо файлова система**

Псевдо файлова система - це така система файлів, яка виглядає як звичайна (з папками і файлами), але насправді не зберігається на диску, а існує тільки в оперативній пам’яті.
Вона потрібна для того, щоб система могла надавати інформацію про процеси, обладнання та стан ядра у зручному вигляді через файли (наприклад, /proc або /sys).

Рисунок 1 - Перегляд вмісту каталогу /proc

<img width="850" height="553" alt="image" src="https://github.com/user-attachments/assets/600d9bb8-1258-4714-84b3-c44ae69142b0" />

Рисунок 2 - Перегляд вмісту каталогу /sys

<img width="582" height="115" alt="image" src="https://github.com/user-attachments/assets/b961142a-9cce-4268-b3bb-65e6fdec0b3a" />

**2. Чому користувачі не звертаються напряму до /proc**

Користувачі рідко працюють напряму з каталогом /proc, тому що там дуже багато технічної інформації у незручному вигляді.
Замість цього використовують команди (наприклад, top, free, mount), які самі читають дані з /proc і показують їх у більш зрозумілому форматі.

**3. Призначення файлів /proc/cmdline, /proc/meminfo, /proc/modules**

/proc/cmdline - містить параметри, які були передані ядру під час запуску системи.

/proc/meminfo - показує інформацію про використання пам’яті.

/proc/modules - містить список модулів, які зараз завантажені в ядро.

Рисунок 3 - Отримання інформації з /proc (meminfo)

<img width="532" height="522" alt="image" src="https://github.com/user-attachments/assets/f33fccb6-7b4d-414f-8904-55d1b97ded48" />

**4. Призначення команди free**

Команда free використовується для перегляду інформації про оперативну пам’ять (RAM), а також про використання віртуальної пам’яті.
Вона показує, скільки пам’яті використовується, скільки вільної та загальний обсяг.

Рисунок 4 - Вивід інформації про пам’ять (команда free)

<img width="845" height="135" alt="image" src="https://github.com/user-attachments/assets/6661b386-e589-4ea1-bb6f-9ede5cbe9056" />

**5. Для чого потрібні лог-файли**

Лог-файли потрібні для збереження інформації про роботу системи та програм.
Вони допомагають знаходити помилки, аналізувати роботу системи та перевіряти безпеку.

Приклади:
- перевірка помилок під час запуску системи (boot.log);
- аналіз роботи служб і процесів;
- перевірка спроб входу в систему (secure);
- діагностика проблем з обладнанням або мережею.

Рисунок 5 - Перегляд каталогу /var/log

<img width="758" height="425" alt="image" src="https://github.com/user-attachments/assets/be814731-2ff7-4246-afee-c2680e7064eb" />

Рисунок 6 - Перегляд файлу dmesg

<img width="831" height="529" alt="image" src="https://github.com/user-attachments/assets/190462d0-f939-4619-9d9f-c86f1107bb1f" />

**6. Призначення файлу /var/log/dmesg**

Файл /var/log/dmesg містить повідомлення ядра, які були створені під час запуску системи.
Він використовується для діагностики проблем із завантаженням або обладнанням.

**7. Для чого розроблено FHS**

FHS (Filesystem Hierarchy Standard) - це стандарт, який визначає, як повинні бути організовані файли та каталоги в Linux.
Він потрібен для того, щоб у різних дистрибутивах була зрозуміла і однакова структура файлової системи.

**8. Основні команди для мережі в Linux**

Основні команди для перегляду та налаштування мережі:
- ifconfig - перегляд мережевих налаштувань;
- ip addr show - сучасна команда для перегляду IP-адрес;
- route - перегляд таблиці маршрутизації;
- ping - перевірка доступності іншого пристрою;
- netstat - інформація про мережеві з’єднання;
- ss - перегляд сокетів і з’єднань;
- dig - перевірка роботи DNS;
- host - визначення IP за доменним ім’ям;
- ssh - підключення до віддаленого комп’ютера.

Рисунок 7 - Перегляд мережевих інтерфейсів (ip addr show)

<img width="822" height="542" alt="image" src="https://github.com/user-attachments/assets/119196c6-4b58-464b-b296-64c4c7fa15cf" />

Рисунок 8 - Перевірка мережі (ping)

<img width="816" height="522" alt="image" src="https://github.com/user-attachments/assets/be5c32d9-4905-4a5f-a807-f9022ff2d417" />

Рисунок 9 - Перегляд мережевих з’єднань (ss)

<img width="820" height="515" alt="image" src="https://github.com/user-attachments/assets/a6315194-3360-4e2f-9ec0-e2c5197017bc" />

### 2. Опрацювання команд Lab 13 - Where Data is Stored

| Назва команди | Її призначення та функціональність |
|---|---|
| su | Використовується для зміни поточного користувача (наприклад, на root). |
| ls /proc | Перегляд вмісту каталогу /proc, який містить інформацію про процеси, систему та обладнання. |
| cat /proc/1/cmdline | Виводить команду запуску процесу з PID 1. |
| echo | Використовується для переходу на новий рядок після виводу cat. |
| ps -p 1 | Відображає інформацію про процес з PID 1. |
| cat /proc/cmdline | Показує параметри, передані ядру під час запуску системи. |
| sysctl | Використовується для перегляду або зміни параметрів ядра. |
| ping localhost > /dev/null | Виконує ping і приховує результат (перенаправлення у /dev/null). |
| Ctrl + C | Завершує процес у foreground. |
| ping localhost > /dev/null & | Запускає процес у фоновому режимі. |
| jobs | Показує список фонових процесів. |
| fg %1 | Переводить процес у foreground. |
| Ctrl + Z | Призупиняє процес. |
| bg %1 | Продовжує процес у фоні. |
| kill %3 | Завершує процес за номером задачі. |
| killall ping | Завершує всі процеси ping. |
| top | Відображає процеси у реальному часі. |
| k (в top) | Завершує процес у top (через введення PID). |
| q (в top) | Вихід із top. |
| kill (signal 15) | Стандартне завершення процесу (SIGTERM). |
| kill (signal 9) | Примусове завершення процесу (SIGKILL). |
| sleep 888888 & | Запускає довготривалий процес у фоні. |
| ps | Відображає процеси поточного сеансу. |
| kill PID | Завершує процес за PID. |
| pkill -15 sleep | Завершує процеси за ім’ям. |
| ps -e | Виводить усі процеси системи. |
| ps -o pid,tty,time,%cpu,cmd | Виводить процеси з заданими параметрами. |
| ps -o pid,tty,time,%mem,cmd --sort %mem | Сортує процеси за використанням пам’яті. |
| free | Показує використання оперативної пам’яті. |
| ls /var/log | Перегляд лог-файлів. |
| ssh localhost | Підключення до локального сервера. |
| tail -5 /var/log/auth.log | Виводить останні записи лог-файлу. |
| man kill | Відображає довідку по команді kill. |

### 3. Опрацювання команд Lab 14 - Network Configuration

| Назва команди | Її призначення та функціональність |
|---|---|
| ifconfig | Відображає інформацію про мережеві інтерфейси (IP-адреси, IPv4, IPv6, MAC-адресу). |
| route | Відображає таблицю маршрутизації мережі. |
| cat /etc/hosts | Виводить вміст файлу hosts, де зберігаються відповідності IP-адрес і імен хостів. |
| grep 127.0.0.1 /etc/hosts | Пошук запису localhost у файлі hosts. |
| ping localhost | Перевіряє доступність хоста (без обмеження кількості пакетів). |
| ping -c4 localhost | Перевіряє доступність хоста, відправляючи 4 пакети. |
| Ctrl + C | Зупиняє виконання команди ping. |
| cat /etc/resolv.conf | Виводить налаштування DNS (nameserver). |
| dig localhost.localdomain | Визначає IP-адресу для доменного імені. |
| sudo /etc/init.d/bind9 restart | Перезапускає DNS-сервер. |
| dig cserver.example.com | Визначає IP-адресу для повного доменного імені (FQDN). |
| dig -x 192.168.1.2 | Виконує зворотне DNS-перетворення (IP → hostname). |
| netstat --help | Відображає довідку по команді netstat. |
| netstat -tl | Показує TCP-порти, що прослуховуються. |
| netstat -tln | Показує TCP-порти у числовому форматі. |
| netstat -ltn | Показує TCP порти, що прослуховуються, у числовому форматі. |
| start_webserver | Запускає тестовий вебсервер для створення мережевого трафіку. |
| ss | Відображає активні мережеві з’єднання та статистику. |

### Виконання практичних завдань
#### Дослідження команди cat

Команда cat (від англ. concatenate) використовується в операційній системі Linux для роботи з файлами. Вона дозволяє переглядати вміст файлів, об’єднувати декілька файлів в один, створювати нові файли та перенаправляти дані.

Основне призначення команди cat - це виведення вмісту файлів у термінал. Вона є однією з найпростіших і найчастіше використовуваних команд у Linux.

Команда cat може використовуватись для таких задач:
- перегляд вмісту текстових файлів;
- створення нових файлів;
- об’єднання кількох файлів в один;
- перенаправлення виводу в інший файл;
- обробка текстових даних у командному рядку.

#### Приклади використання команди cat

1. Створення нового файлу

Команда дозволяє створити файл та записати в нього текст:
```bash
cat > file1.txt
```
Після введення команди користувач вводить текст, а для завершення використовується комбінація клавіш Ctrl + D.

Рисунок 1 - Створення файлу за допомогою команди cat

<img width="458" height="77" alt="image" src="https://github.com/user-attachments/assets/bdb8cc23-1ea9-4f70-aaa3-0fe2f5737358" />

2. Перегляд вмісту файлу

Команда використовується для виведення вмісту файлу у термінал:
```bash
cat file1.txt
```
Рисунок 2 - Створення файлу та перегляд його вмісту за допомогою команди cat

<img width="434" height="98" alt="image" src="https://github.com/user-attachments/assets/3b177781-25e3-473c-9bb0-e5801429d544" />

3. Перенаправлення інформації у файл

Команда використовується для запису вмісту одного файлу в інший:
```bash
cat file1.txt > file2.txt
```
Рисунок 3 - Перенаправлення вмісту файлу

<img width="549" height="122" alt="image" src="https://github.com/user-attachments/assets/9a6bd07e-547b-4a51-b478-064c48efcd75" />

4. Об’єднання кількох файлів в один

Команда дозволяє об’єднати кілька файлів:
```bash
cat file1.txt file2.txt > result.txt
```
Рисунок 4 - Об’єднання файлів

<img width="650" height="168" alt="image" src="https://github.com/user-attachments/assets/1345539a-b12d-4fc5-9b84-ae311dc3cebe" />й

#### Параметри команди cat

Команда cat має додаткові параметри для розширення функціональності:

-n - нумерує всі рядки файлу:
```bash
cat -n file.txt
```
-b - нумерує лише непорожні рядки:
```bash
cat -b file.txt
```
-s - видаляє зайві порожні рядки:
```bash
cat -s file.txt
```
-A - відображає всі символи, включаючи недруковані:
```bash
cat -A file.txt
```
Рисунок 5 - Використання параметрів команди cat

<img width="462" height="315" alt="image" src="https://github.com/user-attachments/assets/5d1b9e07-9add-4471-baa9-1daeaee3f54e" />

#### Можливості команди dig

Команда dig (Domain Information Groper) використовується для отримання інформації про DNS. Вона дозволяє визначити IP-адресу за доменним ім’ям, перевірити роботу DNS-серверів та виконувати зворотне перетворення (IP → ім’я хоста).

Команда dig широко використовується для діагностики мережі та перевірки коректності роботи DNS.

Основні можливості:
- визначення IP-адреси за доменним ім’ям;
- перевірка відповіді DNS-сервера;
- отримання інформації про домен;
- зворотне DNS-перетворення (IP → hostname);
- аналіз часу відповіді DNS.

**Приклади використання**

1. Визначення IP-адреси домену
```bash
dig localhost.localdomain
```
команда повертає IP-адресу для вказаного доменного імені.

<img width="811" height="503" alt="image" src="https://github.com/user-attachments/assets/b1aa6322-209a-4501-b9e7-15675f9a22b4" />

2. Визначення IP-адреси для повного доменного імені (FQDN)
```bash
dig cserver.example.com
```
показує IP-адресу сервера та DNS-відповідь.

<img width="827" height="540" alt="image" src="https://github.com/user-attachments/assets/9c2eedec-1a81-4c06-acbd-262b8938429a" />

3. Зворотне DNS-перетворення
```bash
dig -x 192.168.1.2
```
дозволяє визначити ім’я хоста за IP-адресою.

<img width="829" height="540" alt="image" src="https://github.com/user-attachments/assets/ab515ddb-be89-4aad-acb6-c66034d9d4a7" />

#### Можливості команди netstat

Команда netstat використовується для перегляду інформації про мережеві з’єднання, порти, маршрутизацію та статистику мережі. Вона допомагає визначити, які служби працюють у системі та які порти відкриті.

Команда netstat є важливим інструментом для діагностики мережі та перевірки стану з’єднань.

Основні можливості:
- перегляд активних мережевих з’єднань;
- визначення відкритих портів;
- перевірка служб, що прослуховують порти;
- перегляд таблиці маршрутизації;
- отримання статистики мережі.

**Приклади використання**

1. Перегляд відкритих TCP-портів
```bash
netstat -tl
```
показує TCP-порти, які знаходяться у стані прослуховування.

<img width="832" height="271" alt="image" src="https://github.com/user-attachments/assets/4aef7468-b690-48f7-a78b-1ea8c3b5647d" />

2. Перегляд портів у числовому вигляді
```bash
netstat -tln
```
відображає IP-адреси та порти без перетворення в імена.

<img width="806" height="293" alt="image" src="https://github.com/user-attachments/assets/4817f6e3-1ae7-4310-b775-e5008c0da9ac" />

3. Перегляд тільки listening-портів
```bash
netstat -ltn
```
показує лише ті порти, які очікують підключення.

<img width="812" height="278" alt="image" src="https://github.com/user-attachments/assets/0d4ce6d2-ffcb-4982-bd57-baff2d04692d" />

4. Довідка по команді
```bash
netstat --help
```
виводить список доступних параметрів та можливостей команди.

<img width="809" height="512" alt="image" src="https://github.com/user-attachments/assets/9ea479f1-cdf3-4fa1-9958-c1a6a5a2fd3d" />

### Контрольні запитання

**1. Як пов'язані між собою команди cat та tac?** 

Команди cat і tac виконують схожі функції - вони виводять вміст файлів у термінал. Різниця в тому, що команда cat виводить текст у звичайному порядку, а tac - у зворотному (з кінця до початку).

Рисунок 1 - Порівняння команд cat та tac

На рисунку показано різницю між командами cat та tac: команда cat виводить вміст файлу у звичайному порядку, а tac — у зворотному.

<img width="461" height="186" alt="image" src="https://github.com/user-attachments/assets/84750a07-f6bb-4e0c-845b-bd23c0fb8a02" />

**2. Що робить команда ss?**

Команда ss використовується для перегляду мережевих з’єднань і сокетів. Вона показує активні з’єднання, відкриті порти та статистику мережі. Це сучасна альтернатива команді netstat.

Рисунок 2 - Використання команди ss

На рисунку показано результат виконання команди ss, яка відображає активні мережеві з’єднання та сокети.

<img width="829" height="558" alt="image" src="https://github.com/user-attachments/assets/923110fd-070c-465c-981e-a7f1f44fc086" />

**3. В чому відмінність між командами ps --forest та pstree?**

Команда ps --forest показує процеси у вигляді дерева прямо у списку процесів.

Команда pstree також відображає процеси у вигляді дерева, але більш наочно і компактно. Тобто pstree зручніша для візуального перегляду структури процесів.

Рисунок 3 - Перегляд процесів (ps --forest та pstree)

На рисунку показано відображення процесів у вигляді дерева за допомогою команд ps --forest та pstree.

<img width="904" height="691" alt="image" src="https://github.com/user-attachments/assets/8526b50a-1258-4a68-81f4-39dfe27f86b8" />

**4. У яких каталогах зберігаються налаштування системи?**

Основні налаштування системи зберігаються у каталозі /etc. Там знаходяться конфігураційні файли різних програм і служб.

Рисунок 4 - Вміст каталогу /etc

На рисунку показано результат виконання команди ls /etc, яка дозволяє переглянути конфігураційні файли системи.

<img width="925" height="673" alt="image" src="https://github.com/user-attachments/assets/45fec918-b0e5-4189-a59f-12ab9de2e4b8" />

**5. У яких каталогах можна знайти встановлені в системі програми, доступні для користувача?**

Програми, доступні звичайному користувачу, знаходяться в каталогах /usr/bin та /bin.

Рисунок 5 - Каталоги з програмами користувача (/bin, /usr/bin)

На рисунку показано вміст каталогів /bin та /usr/bin, де зберігаються програми, доступні користувачам.

<img width="863" height="755" alt="image" src="https://github.com/user-attachments/assets/e8f56296-16fa-4dbc-b1b8-ca0a94aba72a" />

<img width="882" height="753" alt="image" src="https://github.com/user-attachments/assets/70ae048e-c5ec-4034-97b2-4e2026baba5c" />

**6. У яких каталогах можна знайти встановлені системні програми і програми для суперкористувача?**

Системні програми та програми для адміністратора знаходяться у каталогах /sbin та /usr/sbin.

Рисунок 6 - Каталоги системних програм (/sbin, /usr/sbin)

На рисунку показано вміст каталогів /sbin та /usr/sbin, де знаходяться системні програми та утиліти для адміністратора.

<img width="921" height="746" alt="image" src="https://github.com/user-attachments/assets/ca4cf792-a447-4a2b-8f5c-1db4f95effae" />

<img width="922" height="704" alt="image" src="https://github.com/user-attachments/assets/2ff89ebf-cdbc-410d-9e75-b7db768cd6bf" />

**7. Поясніть призначення команд ping, ifconfig, traceroute.**

- Команда ping використовується для перевірки доступності іншого пристрою в мережі.
- Команда ifconfig використовується для перегляду та налаштування мережевих інтерфейсів.
- Команда traceroute показує шлях, який проходять пакети до іншого вузла в мережі.

Рисунок 7 - Використання команд ping та ifconfig

На рисунку показано результат виконання команд ping та ifconfig, які використовуються для перевірки мережі та перегляду мережевих інтерфейсів.

<img width="923" height="713" alt="image" src="https://github.com/user-attachments/assets/a427fa42-daff-4951-987d-9aeac87ed40c" />

**8. Як називаються мережеві інтерфейси в Linux?**

Мережеві інтерфейси в Linux мають назви типу eth0, eth1 (Ethernet), lo (loopback), а також сучасні назви, наприклад enp0s3.

**9. Як за допомогою команди ifconfig вивести параметри тільки одного інтерфейсу (наприклад, eth1)?**

Для цього потрібно вказати назву інтерфейсу після команди:
```bash
ifconfig eth1
```
Ця команда покаже інформацію тільки для заданого мережевого інтерфейсу.

Рисунок 8 - Перегляд параметрів окремого інтерфейсу (ifconfig enp0s3)

На рисунку показано результат виконання команди ifconfig enp0s3, яка дозволяє переглянути параметри конкретного мережевого інтерфейсу.

<img width="902" height="316" alt="image" src="https://github.com/user-attachments/assets/c3a7e8a5-4eed-495e-b934-19bd588f4c6a" />
