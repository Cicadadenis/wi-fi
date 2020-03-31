Wifi
======

Этот репозиторий представляет собой полную переписку [`wifi`] (https://github.com/bednakovdenis/wifi) скрипта Python для аудита беспроводных сетей.

Wifi использует существующие инструменты беспроводного аудита. Хватит запоминать аргументы команды и переключатели!

Wifite предназначен для использования всех известных способов получения пароля беспроводной точки доступа (маршрутизатора). Эти методы включают в себя:
1. WPS: [автономная атака Pixie-Dust] (https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup#Offline_brute-force_attack)
1. WPS: [онлайн-атака с помощью брут-форс-пин-кода] (https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup#Online_brute-force_attack)
2. WPA: [Захват рукопожатия WPA] (https://hashcat.net/forum/thread-7717.html) + автономный кряк.
3. WPA: [Захват PMKID] (https://hashcat.net/forum/thread-7717.html) + автономный взлом.
4. WEP: различные виды атаки на WEP, в том числе * фрагментация *, * chop-chop *, * aireplay * и т. Д.
Запустите wifi, выберите ваши цели, и Wifi автоматически начнет пытаться захватить или взломать пароль.

Поддерживаемые операционные системы
---------------------------
Wifi разработан специально для последней версии [** Kali ** Linux] (https://www.kali.org/). [ParrotSec] (https://www.parrotsec.org/) также поддерживается.

Другие дистрибутивы для тестирования пера (такие как BackBox или Ubuntu) имеют устаревшие версии инструментов, используемых Wifi. Не ожидайте поддержки, если вы не используете последние версии * Required Tools *, а также [исправленные беспроводные драйверы, поддерживающие инъекцию] ().

Необходимые инструменты
-------------- Прежде всего, вам понадобится беспроводная карта, поддерживающая «Режим мониторинга» и внедрение пакетов (см. [Это руководство для проверки совместимости вашей беспроводной карты]) (http: //www.aircrack-ng.org/doku.php?id=compatible_cards), а также [это руководство] (https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup#Offline_brute-force_attack)). В интернет-магазинах есть много дешевых беспроводных карт, подключаемых к USB.

Во-вторых, поддерживаются только последние версии этих программ, и они должны быть установлены для правильной работы Wifi:

** Необходимые: **
* `python`: Wifi совместим как с` python2`, так и с `python3`.
* [`iwconfig`] (https://wiki.debian.org/iwconfig): для идентификации беспроводных устройств, уже находящихся в режиме мониторинга.
* [`ifconfig`] (https://en.wikipedia.org/wiki/Ifconfig): для запуска / остановки беспроводных устройств.
* [`Aircrack-ng`] (http://aircrack-ng.org/) комплект включает в себя:
   * [`airmon-ng`] (https://tools.kali.org/wireless-attacks/airmon-ng): для перечисления и включения режима мониторинга на беспроводных устройствах.
   * [`aircrack-ng`] (https://tools.kali.org/wireless-attacks/aircrack-ng): для взлома файлов .cap WEP и захвата рукопожатия WPA.
   * [`aireplay-ng`] (https://tools.kali.org/wireless-attacks/aireplay-ng): для деавторизации точек доступа, воспроизведения файлов захвата, различных WEP-атак.
   * [`airodump-ng`] (https://tools.kali.org/wireless-attacks/airodump-ng): для сканирования цели и создания файла захвата.
   * [`packetforge-ng`] (https://tools.kali.org/wireless-attacks/packetforge-ng): для подделки файлов захвата.

** Необязательно, но рекомендуется: **
* [`tshark`] (https://www.wireshark.org/docs/man-pages/tshark.html): для обнаружения сетей WPS и проверки файлов захвата рукопожатия.
* [`reaver`] (https://github.com/t6x/reaver-wps-fork-t6x): для атак WPS Pixie-Dust и грубой силы.
   * Примечание: инструмент Reaver `wash` можно использовать для обнаружения сетей WPS, если` tshark` не найден.
* [`bully`] (https://github.com/aanarchyy/bully): для атак WPS Pixie-Dust и грубой силы.
   * Альтернатива Reaver. Укажите `--bully` для использования Bully вместо Reaver.
   * Bully также используется для получения PSK, если «взломщик» не может после взлома WPS PIN.
* [`coWPAtty`] (https://tools.kali.org/wireless-attacks/cowpatty): для обнаружения захвата рукопожатия.
* [`pyrit`] (https://github.com/JPaulMora/Pyrit): для обнаружения захвата рукопожатия.
* [`hashcat`] (https://hashcat.net/): для взлома PMKID-хэшей.
   * [`hcxdumptool`] (https://github.com/ZerBea/hcxdumptool): для записи хэшей PMKID.
   * [`hcxpcaptool`] (https://github.com/ZerBea/hcxtools): для преобразования захватов пакетов PMKID в формат` hashcat`.Run Wifi
----------
```
git clone https://github.com/bednakovdenis/wifi.git
cd wi-fi
sudo ./Wifi.py
```

Установить Wifi
--------------
Чтобы установить на свой компьютер (чтобы вы могли просто запустить `wifite` из любого терминала), запустите:

`` `Баш
sudo python setup.py установить
`` `

Это установит `wifi` в` / usr / sbin / wifi`, который должен находиться в вашем терминальном пути.

** Примечание: ** Удаление не так просто (https://stackoverflow.com/questions/1550226/python-setup-py-uninstall#1550235). Единственный способ удалить это записать файлы, установленные вышеуказанной командой, и * удалить * эти файлы:
```bash
sudo python setup.py install --record files.txt \
  && cat files.txt | xargs sudo rm \
  && rm -f files.txt
```
