---
title: Мастер таблицы по Сетевым Моделям и Протоколам
description: Это руководство объединяет две методологически корректные таблицы: одну для концептуальных моделей (OSI и TCP/IP) и одну для конкретных протоколов и технологий.
date: 2025-11-04
category: Сетевые технологии и протоколы
author: veilosophy
---

## 1. Сравнительная Таблица Сетевых Моделей (OSI и TCP/IP)

| Уровень OSI (7 уровней) | Уровень TCP/IP (4 уровня) | Единица Данных (PDU) | Назначение | Примеры Протоколов |
| :--- | :--- | :--- | :--- | :--- |
| **7. Прикладной** (Application) | **4. Прикладной** (Application) | Данные (Data) | **То, что видит пользователь.** Здесь работают программы (браузер, почта, мессенджер). | HTTP, HTTPS, FTP, SMTP, DNS, SSH |
| **6. Представления** (Presentation) | **Функции объединены в Прикладном уровне TCP/IP** | Данные (Data) | **Переводчик и шифровальщик.** Обеспечивает, чтобы данные были понятны обеим сторонам (шифрование, сжатие, кодировка). | TLS/SSL, JPEG, MPEG |
| **5. Сеансовый** (Session) | **Функции объединены в Прикладном уровне TCP/IP** | Данные (Data) | **Организатор сеанса.** Устанавливает, поддерживает и завершает сеанс связи между двумя приложениями. | NetBIOS, RPC, L2TP |
| **4. Транспортный** (Transport) | **3. Транспортный** (Transport) | Сегмент (Segment) / Датаграмма (Datagram) | **Почтальон.** Отвечает за доставку данных от одного приложения к другому. Решает, нужна ли надежность (TCP) или скорость (UDP). | TCP, UDP, SCTP |
| **3. Сетевой** (Network) | **2. Межсетевой** (Internet) | Пакет (Packet) | **Навигатор.** Отвечает за маршрутизацию — находит лучший путь для данных через разные сети (через роутеры). | IP (IPv4, IPv6), ICMP, BGP |
| **2. Канальный** (Data Link) | **1. Доступа к Сети** (Network Access) | Кадр (Frame) | **Дорожный инспектор.** Отвечает за доставку данных между устройствами в пределах одной локальной сети (через коммутаторы). Использует MAC-адреса. | Ethernet, Wi-Fi, ARP, PPP |
| **1. Физический** (Physical) | **Входит в уровень Доступа к Сети** | Бит (Bit) | **Провода и сигналы.** Отвечает за физическую передачу битов (электрических, световых или радиосигналов) по кабелю или воздуху. | Кабели (медные, оптоволокно), Радиоволны, Хабы |

## 2. Таблица Сетевых Протоколов и Технологий

| Протокол / Технология | Уровень OSI / TCP-IP | Основное Назначение | Как Работает (Ключевые Детали) | Риски Безопасности / Уязвимости | Инструменты и Команды |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Ethernet** (IEEE 802.3) | L1 (Физ.) / L2 (Кан.) | Проводная передача данных в локальной сети (LAN). | Определяет формат кадров (Frames) и MAC-адресацию. | VLAN Hopping, ARP Spoofing, MAC Flooding. | `ip link`, `ethtool`, `Wireshark` |
| **Wi-Fi** (IEEE 802.11) | L1 (Физ.) / L2 (Кан.) | Беспроводная передача данных в локальной сети. | Использует радиоволны (2.4/5/6 ГГц) и стандарты WPA2/WPA3 для шифрования. | WPA2/WPA3 Cracking, Evil Twin, Deauthentication Attacks. | `aircrack-ng`, `iw` |
| **ARP** (Address Resolution Protocol) | L2 (Канальный) | Находит физический адрес (MAC) устройства по его логическому адресу (IP) в локальной сети. | Broadcast-запрос (кто имеет IP X, скажи свой MAC) и Unicast-ответ. | ARP Spoofing (MITM), ARP Cache Poisoning. | `arp -a`, `arping`, `Wireshark` |
| **IPv4 / IPv6** | L3 (Сетевой) | Доставка данных между разными сетями (маршрутизация). | IPv4: 32-битные адреса. IPv6: 128-битные адреса, автоконфигурация (SLAAC). | IP Spoofing, Fragmentation Attacks, NDP Spoofing (IPv6). | `ping`, `traceroute`, `ip route`, `ndp` (для IPv6) |
| **ICMP** (Internet Control Message Protocol) | L3 (Сетевой) | Диагностика и передача служебных сообщений об ошибках. | Используется командами `ping` и `traceroute`. Не имеет портов. | ICMP Flood (DoS), ICMP Tunneling (передача данных через ICMP). | `ping`, `traceroute`, `hping3` |
| **BGP** (Border Gateway Protocol) | L3 (Сетевой) | "Карта Интернета". Определяет, как данные будут ходить между крупными сетями (провайдерами). | Обмен информацией о маршрутах (префиксах) между Автономными Системами (AS). | Route Hijack (угон префикса), Prefix Injection. | Router CLI, `bgpmon` |
| **TCP** (Transmission Control Protocol) | L4 (Транспортный) | Надежная доставка данных с проверкой. "Почтальон с подписью". | 3-way Handshake, сегментация, подтверждение (ACK), повторная передача. | SYN Flood (DoS), Session Hijacking, RST Attack. | `ss -tulpn`, `nmap` |
| **UDP** (User Datagram Protocol) | L4 (Транспортный) | Быстрая доставка данных без проверки. "Почтальон без подписи". | Передача датаграмм без подтверждения и повторной передачи. | Amplification Attacks (DNS, NTP), Flood Attacks. | `ss -u`, `tcpdump`, `hping3` |
| **DNS** (Domain Name System) | L7 (Прикладной) | Переводит понятные имена (google.com) в IP-адреса. | Работает преимущественно через **UDP/53** (запросы) и **TCP/53** (передача зон). | Cache Poisoning, Amplification Attacks (через UDP), DNS Tunneling. | `dig`, `nslookup`, `host`, `Wireshark` |
| **DHCP** (Dynamic Host Configuration Protocol) | L7 (Прикладной) | Автоматически выдает IP-адреса устройствам в сети. | Использует Broadcast (L2) и UDP (L4) для обнаружения сервера (DORA process). | Rogue DHCP Server, DHCP Starvation, MITM. | `dhclient`, `dhcpdump`, `Wireshark` |
| **Load Balancing** | L4 (Трансп.) / L7 (Прикл.) | Равномерно распределяет запросы между несколькими серверами. | L4: на основе IP/порта. L7: на основе HTTP-заголовков, Cookie, URL. | Misconfiguration (DoS), Session Fixation, Backend Probing. | `HAProxy`, `Nginx`, `iptables` (для L4 NAT) |
| **HTTP / HTTPS** | L7 (Прикладной) | Основа для работы веб-сайтов и API. | Запрос-ответ модель. HTTPS использует **TLS/SSL** (L6) для шифрования. | MITM (если нет TLS), XSS, CSRF, TLS Downgrade. | `curl`, `Burp Suite`, `Wireshark` |
| **SSH / Telnet** | L7 (Прикладной) | Удаленное управление серверами через командную строку. | SSH: Шифрованный. Telnet: Нешифрованный (Plaintext). | Bruteforce, Credential Theft, Key Hijacking (SSH). | `ssh`, `telnet`, `nmap` |
| **NAT / PAT** | L3 (Сетевой) / L4 (Трансп.) | Позволяет нескольким устройствам в частной сети выходить в Интернет через один публичный IP. | NAT: Private IP → Public IP. PAT (NAPT): Private IP:Port → Public IP:Port. | Complicates Logging, NAT Traversal Attacks (STUN/TURN). | `iptables -t nat`, `ip route` |
| **VLAN / VXLAN** | L2 (Канальный) | Логически разделяет одну физическую сеть на несколько виртуальных. | VLAN: Добавление тега (802.1Q) к кадру. VXLAN: Инкапсуляция L2-кадров в UDP-пакеты (L4). | VLAN Hopping, Double Tagging. | Switch CLI, `Wireshark` |
| **MPLS** (Multi-Protocol Label Switching) | L2.5 (Между Кан. и Сет.) | Высокоскоростная маршрутизация в крупных сетях (провайдеры). | Замена IP-маршрутизации на коммутацию по меткам (Labels). | Misconfiguration (утечка трафика), Label Spoofing. | Router CLI, `Wireshark` |
| **LDAP / Kerberos** | L7 (Прикладной) | Централизованная аутентификация и управление пользователями. | LDAP: Протокол доступа к каталогу. Kerberos: Система тикетов для SSO. | Weak Passwords, Pass-the-Hash (Kerberos), LDAP Injection. | `ldapsearch`, `Wireshark` |
| **SNMP** (Simple Network Management Protocol) | L7 (Прикладной) | Мониторинг и управление сетевыми устройствами. | Использует Community Strings (пароли) для доступа к информации MIB. | Default Community Strings (public/private), DoS. | `snmpwalk`, `snmpget`, `Wireshark` |
| **SMB / NFS** | L7 (Прикладной) | Предоставление общего доступа к файлам и папкам по сети. | SMB (Windows), NFS (Unix/Linux). | Ransomware, Lateral Movement, Null Sessions (SMB). | `smbclient`, `mount`, `Wireshark` |
