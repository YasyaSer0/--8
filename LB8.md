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
