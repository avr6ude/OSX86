# Установка на Intel-PC
## Подбор и проверка совместимости железа
* **Процессор**: обязательно Intel (существуют варианты установки на AMD, но это по большей части костыль и не стоит того)
* **Видеокарта**: на данный момент можно "завести" любую видеокарту (есть исключения¹).
* **Материнская плата**: частично бывают проблемными материнские платы на X*-чипсетах.
* **Аудио**: работает практически всё, но бывают исключения.
* **Сеть**: заводимо всё, кроме китайских ноунейм LAN-карт.
* **Bluetooth и Wi-Fi**: смотреть [таблицу](https://docs.google.com/spreadsheets/d/1Yxlvo-vK_zupMiR1Ua_NZ1X0j6BSXoICCEgB7wvAQsM/edit#gid=0).
## Настройка BIOS Legacy и BIOS UEFI
* **CSM**: На современных платах и видеокартах при использовании исключительно UEFI-загрузки рекомедуется его выключать
* **Secure Boot**: Other OS(UEFI)
* **SATA**: Обязательно AHCI, иначе работать не будет
* **HPET**: Включен
* **Fast Boot** и **Hardware Fast Boot** Выключить.
* **Above 4G Decoding** Включить.
* Отключаем USB 3.0 и 3.1 во избежание проблем во время установки
* Отключаем Serial-порты и подобные неиспользуемые интерфейсы
* Отключаем Bluetooth
### Примечания:
* На сборках с двумя CPU требуется поставить двухядерный режим на обоих CPU
* Видеокарта должна быть на время установки одна и установлена в первый слот
* Отключить все мониторы, кроме основного.

## Clover
**Clover** - это загрузчик, который позволяет на обычном компьютере запустить **macOS**. **Apple** этого делать не разрешает, в первую очередь мотивируя тем, что “мы не можем обеспечить работоспособность на компьютерах, произведенными не компанией **Apple**”. Поэтому ставим систему на свой страх и риск.

## config.plist
Этот файл используется для настройки загрузчика **Clover**. Он - основа всего, то, что заставить вашу систему работать правильно.
**Clover** умеет генерировать файл конфигурации (далее - **конфиг**), основанный на вашем "железе" самостоятельно, но как вы знаете, нет ничего идеального. Поэтому у пользователя есть возможность менять параметры "конфига" напрямую в файле или на ходу в настройках **Clover'a**. Файл написан на языке **XML**, что существенно упрощает работу с ним, так как этот язык является user-friendly. Файл должен находится в **EFI/CLOVER**. Его можно редактировать как с помощью простых редакторов(Notepad, Sublime Text, Atom, `nano`, `vim`), так и с более специализированными под это дело(**PlistEdit**, **Clover Configurator**). Также, с недавнего времени, появился веб-редактор, заточенный под "конфиг". Его название **CloverCloudEditor**. Он доступен [здесь](http://cloudclovereditor.altervista.org/cce/index.php).

## Видео
В данный момент большая часть поддерживаемых системой видеокарт заводятся через плагин [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases) к [Lilu.kext](https://github.com/acidanthera/Lilu/releases). Инструкции по его использованию к конкретным видеокартам – ниже по этому тексту. 
## Звук
**Существует два метода "завода" звука: AppleALC и VoodooHDA.**
### AppleALC:  
> Этот метод является динамическим патчингом нативного AppleHDA.
* Само расширение сделано для Realtek ALC кодеков, которые сейчас являются самыми популярными среди производителей материнских плат. 
* Также работает для "завода" звука через HDMI на картах Intel, AMD и NVIDIA.
* Список поддерживаемых кодеков доступен [здесь](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs).

**Установка:**
* Скачиваем [Lilu](https://github.com/acidanthera/Lilu/releases) и сам [AppleALC](https://github.com/acidanthera/AppleALC/releases);
* Кладём оба кекста в **CLOVER/EFI/kexts/Other**.
* Выключаем FixHDA, AddHDMI, UseIntelHDMI в `config.plist`;
* В `config.plist` в **строке** `Devices/Audio/Inject` пишем NO;
* В `Boot/Arguments` добавляем `alcid=X`, где X - номер layout-а, который идёт вместе с кодеком в таблице;
* Перезагружаемся.
> Примечание: если звук так и не появился, то пробуем другой layout. 

### VoodooHDA: 
* Сможет "завести" почти любой аудиокодек, но настройка самого расширения иногда очень проблематична. 

**Установка:**
* Скачиваем сам [кекст](https://sourceforge.net/projects/voodoohda/files/VoodooHDA.kext-2.9.0d10.zip/download) или [установщик](https://sourceforge.net/projects/voodoohda/files/VoodooHDA-2.8.8.pkg.zip/download).
* Кладем кекст в `/System/Library/Extensions` и чиним права, или устанавливаем через [Kext Utility](http://cvad-mac.narod.ru/files/Kext_Utility.app.v2.6.6.zip).
* Перезагружаемся.
* Про дополнительную настройку VoodooHDA можно почитать [здесь](https://applelife.ru/posts/589135).
## Создание загрузочной USB
Самым лучшим и правильным способом по мнению русского хак-коммьюнити является установка чистого образа из App Store. С помощью программы **BootDiskUtility** (в сокращении - BDU) и образа `.hfs` можно получить наиболее чистую систему. 
Естественно, существует не один способ установки Хакинтоша, но сейчас мы рассмотрим наиболее популярный. 
1. Скачиваем **BootDiskUtility** [отсюда](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5).
2. Распаковываем утилиту в любую папку. 
3. Скачиваем образ **macOS** [отсюда](https://mac-ru.net/viewtopic.php?t=41), [отсюда](https://nnmclub.to/forum/viewtopic.php?t=1069291) или с [магнет-ссылки](magnet:?dn=BDUOSXDISTR&xt=urn:btih:64125b9f1387632e1b35b8da27eba422f9821d43). 
4. Распаковываем образ из архива.
5. Открываем **BootDiskUtility**, заходим в секцию настроек, нажимаем **Check Now**. Это проверит последнюю версию **Clover** и выберет её в качестве версии для записи на USB. 
6. Выбираем своё USB-устройство, нажимаем **Format Disk**. Дожидаемся записи бутлоадера на USB. 
> На этом шаге у вас уже должен быть скачан образ **macOS** в виде `5.hfs`.  
7. Нажимаем на значок `+` рядом с названием USB. Если вы ничего не меняли в настройках, то у вас появится два раздела, один из которых будет иметь название `CLOVER`, а другой `NONAME`.
8. Выбираем `Part2`, который имеет название `NONAME`. Нажимаем кнопку **Restore Partition** и указываем прежде скачанный `5.hfs`. Начнется запись образа на USB. 

Теперь у вас есть готовая USB с образом **macOS**. Вы совершили свой первый шаг к установке Хакинтоша.

## Установка образа на HDD/SSD
1. Для начала рекомендуется внести минимальные правки в config.plist, прописав в `Boot/Arguments` `-v debug=0x100 keepsyms=1`, а если ставите High Sierra, то и добавить [патч на показ паники](https://4pda.ru/forum/index.php?act=findpost&pid=62112835&anchor=Spoil-62112835-1).
2. Положите kext-ы на сеть, звук и видео. 
> В случае High Sierra и новее не забудьте скопировать `ApfsDriverLoader-64.efi` из папки drivers-Off в drivers64 или drivers64UEFI в зависимости от типа загрузки.
3. Загружаемся с готовой USB в Clover и выбираем пункт **Boot macOS from OS X Base System**. 
> При первом запуске (если он успешен), вас встретит дружелюбное окно с выбором языка.
4. Выбираем нужный язык, нажимаем **Далее**
> Если вы уже отформатировали диск или раздел в HFS+, то переходим к шагу 8
5. Дальше нам нужно отформатировать диск. Наводим на верхнюю панель, в ней нажимаем **Утилиты - Дисковая утилита**. 
6. Выбираем нужный нам раздел, нажимаем **Стереть**. Вводим название, формат **OS X Extended(журналируемый)** и таблицу **GUID**.
7. Дожидаемся окончания форматирования и закрываем утилиту.
8. Нажимаем далее и выбираем свежеотформатированный диск.
9. После завершения установки вам надо будет перезагрузить систему, но на этот раз в Clover надо выбирать **Boot macOS from %названиедиска%**
10. Как только произойдет загрузка системы, вам предложат настроить основные компоненты.
После окончания настройки у вас будет чистая система **macOS**, но, к сожалению, загрузка возможно только с USB. Чтобы это исправить нужно установить **Clover** в _EFI_ раздел, процесс установки которого я опишу ниже.

## Установка Clover на EFI раздел





# Полезные ссылки 
## Главное 
* Дистрибутивы — http://osxpc.ru/category/downloads/osx/
* Кексты 1 – https://www.applelife.ru/threads/2942933
* Кексты 2 — http://osxpc.ru/downloads/k/kexts/
* Запаска SLE — http://osxpc.ru/zapaska/
* Clover — https://sourceforge.net/projects/cloverefiboot/files/latest/download
* Клевер цвета хаки 4542 — https://i.applelife.ru/2018/06/431578_Klever_cveta_xaki_4542.pdf
* "Чистый" config.plist для редактирования под себя – https://sourceforge.net/p/cloverefiboot/code/HEAD/tree/CloverPackage/CloverV2/EFI/CLOVER/config-sample.plist 
* Настройка BIOS (общее) — http://osxpc.ru/faq/settings_bios/
### Обсуждение 
* Clover — https://applelife.ru/threads/42089
* Mojave – https://applelife.ru/threads/2942975
* High Sierra – https://applelife.ru/threads/2210706
* Sierra – https://applelife.ru/threads/2929575
* El Capitan — https://applelife.ru/threads/517495
* Yosemite — https://applelife.ru/threads/41758
## Графика
### Intel
* Актуальный мануал – https://applelife.ru/posts/729378
* Skylake HD – http://osxpc.ru/zavod/gpu/intel/skylake/
* Broadwell HD – http://osxpc.ru/zavod/gpu/intel/broadwell/
* Haswell HD – http://osxpc.ru/zavod/gpu/intel/haswell/
* HD4000 — http://osxpc.ru/zavod/gpu/intel/hd4000/
* HD3000 — http://osxpc.ru/zavod/gpu/intel/hd3000/
* GMA X3100 — https://applelife.ru/threads/36617
* GMA 950 — https://applelife.ru/threads/22726

### Radeon
* FAQ по WhateverGreen – https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.Radeon.ru.md
* Патч фреймбуфера — http://osxpc.ru/zavod/gpu/ati/patch/
* HD4X00, HD5000, HD6000 — https://applelife.ru/threads/zavod-ati-hd–6xxx–5xxx–4xxx.28890/
* HD7000, R5, R7, R9, RX — https://applelife.ru/threads/amd-hd7xx0-r5-r7-r9-rx.36269/

### Nvidia

* Fermi – https://applelife.ru/threads/27607
* Kepler — https://applelife.ru/threads/37131
* Maxwell/Pascal – https://applelife.ru/threads/1546195

## Звук
### AppleALC:

* Релизы (скачивание) – http://github.com/vit9696/AppleALC/releases
* Поддерживаемые кодеки – http://github.com/vit9696/AppleALC/wiki/Supported-codecs
* Видео по установке – https://www.youtube.com/watch?v=xbLn_OkVuKY

* AppleHDA (Если нет поддержки со стороны AppleALC) — http://osxpc.ru/kexts/audio/applehda/
* VoodooHDA (Полностью рабочий аналог AppleHDA) — https://sourceforge.net/projects/voodoohda/files/latest/download
* Toleda HDMI [устарело] — http://tonymacx86.com/threads/audio-hdmi-audio-applehda-guide.143760/

### Обсуждение:

* AppleALC — https://applelife.ru/threads/applealc-dinamicheskij-patching-applehda.1171672/
* VoodooHDA — https://applelife.ru/threads/delaem-zvuk-na-osnove-voodoohda.18413/

## СЕТЬ

### RJ-45 (LAN):

* Полный список + обсуждение — https://applelife.ru/forums/setevye-karty.40/
* Самые популярные — http://osxpc.ru/category/kexts/internet/

### Wi-Fi (WLAN):

* Новая таблица (NGFF+PCI-E) — https://pp.vk.me/c630723/v630723383/271b8/8P0Uz2vtNIE.jpg
* Старая таблица (только PCI-e) — https://new.vk.com/doc-12954845_437058293
* Также стоит взглянуть — https://github.com/toleda/wireless_half-mini

## PS/2, I2C (Клавиатура, мышь, тачпад)

* Десктопный вариант — http://osxpc.ru/kexts/ps2/vdps2/
* ELAN — http://osxpc.ru/kexts/ps2/elan/
* Synaptic и прочие — http://osxpc.ru/kexts/ps2/synaptic/

## АККУМУЛЯТОР

* Кекст — https://bitbucket.org/RehabMan/os-x-acpi-battery-driver/downloads/
* Инструкция по патчингу DSDT – https://www.tonymacx86.com/threads/116102
* Патчи для DSDT (репозиторий) — http://raw.github.com/RehabMan/Laptop-DSDT-Patch/master

## USB
* USBInjectAll.kext – https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/
* Большой мануал по заводу USB – https://applelife.ru/posts/550233
* Создание USBLegacy.kext – https://applelife.ru/posts/537459

## МАТЕРИНСКИЕ ПЛАТЫ

* Предпочтительны к покупке — http://osxpc.ru/motherboards/

### Обсуждения:

* Все — https://applelife.ru/categories/materinskie-platy.26/
* Asrock — https://applelife.ru/forums/asrock.29/
* Asus — https://applelife.ru/forums/asus.28/
* Gigabyte — https://applelife.ru/forums/gigabyte.33/
* Intel — https://applelife.ru/forums/intel.34/
* MSI — https://applelife.ru/forums/msi.35/


## СИСТЕМА И ЮЗАБЕЛЬНОСТЬ

* Завод MacAppStore и iCloud; iMessage и FaceTime; HandOff и Continuity — https://applelife.ru/posts/727913
* Работа с ACPI (DSDT, SSDT) — http://osxpc.ru/faq/acpi-manual/
* Регулировка яркости в ноутбуках — http://osxpc.ru/faq/brightness-laptop/
* Регулировка яркости клавишами Fn — http://osxpc.ru/faq/backlight-fn/
* Ошибка boot0: error — http://osxpc.ru/faq/boot0-error/
