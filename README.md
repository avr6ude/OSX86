# Предыстория
*дописать*

# Установка на Intel-PC
## Подбор и проверка совместимости железа
* **Процессор**: обязательно Intel (есть варианты установки на AMD, но это по-большей части костыль и не стоит того)
* **Видеокарта**: на данный момент можно "завести" любую видеокарту(есть исключения¹).
* **Материнская плата**: частично бывают проблемными материнские платы на X* чипсетах.
* **Аудио**: работает практически все, но бывают исключения.
* **Сеть**: заводимо все, кроме китайских ноунейм LAN-карт.
* **Bluetooth и Wi-Fi**: смотреть [таблицу](https://docs.google.com/spreadsheets/d/1Yxlvo-vK_zupMiR1Ua_NZ1X0j6BSXoICCEgB7wvAQsM/edit#gid=0).

## Создание загрузочной USB
Самым лучшим и правильным способом по мнению русского хак-коммьюнити является установка чистого образа из App Store. С помощью программы **BootDiskUtility** (в сокращении - BDU) и образа `.hfs` можно получить наиболее чистую систему. 
Естественно, существует не один способ установки Хакинтоша, но сейчас мы рассмотрим наиболее популярный. 
1. Скачиваем **BootDiskUtility** [отсюда](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5).
2. Распаковываем утилиту в любую папку. 
3. Скачиваем образ **macOS** [отсюда](https://mac-ru.net/viewtopic.php?t=41), [отсюда](https://nnmclub.to/forum/viewtopic.php?t=1069291) или с [магнет-ссылки](http://xn--80agpnh5a.tk/#magnet:?dn=BDUOSXDISTR&xt=urn:btih:64125b9f1387632e1b35b8da27eba422f9821d43). 
4. Распаковываем образ из архива.
5. Открываем **BootDiskUtility**, заходим в секцию настроек, нажимаем **Check Now**. Это проверит последнюю версию **Clover'а** и выберет ее в качестве версии для записи на USB. 
6. Выбираем свое USB-устройство, нажимаем **Format Drive**. Дожидаемся записи бутлоадера на USB. 
> На этом шаге у вас уже должен быть скачан образ **macOS** в виде `5.hfs`.  
7. Нажимаем на значок `+` рядом с названием USB. Если вы ничего не меняли в настройках, то у вас появится два раздела, один из которых будет иметь название `CLOVER`, а другой `NONAME`.
8. Выбираем `Part2`, который имеет название `NONAME`. Нажимаем кнопку **Restore Partition** и указываем прежде скачанный `5.hfs`. Начнется запись образа на USB. 

Теперь у вас есть готовая USB с образом **macOS**. Вы совершили свой первый шаг к установке Хакинтоша.






# Полезные ссылки 
## Главное 
* Дистрибутивы — http://osxpc.ru/category/downloads/osx/
* Кексты — http://osxpc.ru/downloads/k/kexts/
* Запаска SLE — http://osxpc.ru/zapaska/
* Clover — https://sourceforge.net/projects/cloverefiboot/files/latest/download
* Клевер цвета хаки 3262 — https://new.vk.com/doc44638855_430072084
* Настройка BIOS (общее) — http://osxpc.ru/faq/settings_bios/
### Обсуждение 
* Clover — https://applelife.ru/threads/clover.42089/
* El Capitan — https://applelife.ru/threads/ustanovka-os-x-el-capitan–10–11-na-intel-pc.517495/
* Yosemite — https://applelife.ru/threads/ustanovka-os-x-yosemite–10–10-na-intel-pc.41758/
## Графика
### Intel
* Skylake HD – http://osxpc.ru/zavod/gpu/intel/skylake/
* Broadwell HD – http://osxpc.ru/zavod/gpu/intel/broadwell/
* Haswell HD – http://osxpc.ru/zavod/gpu/intel/haswell/
* HD4000 — http://osxpc.ru/zavod/gpu/intel/hd4000/
* HD3000 — http://osxpc.ru/zavod/gpu/intel/hd3000/
* GMA X3100 — https://applelife.ru/threads/intel-gma-x3100-zavod.36617/
* GMA 950 — https://applelife.ru/threads/intel-gma950–32bit-only.22726/

### Radeon

* Патч фреймбуфера — http://osxpc.ru/zavod/gpu/ati/patch/
* HD4X00, HD5000, HD6000 — https://applelife.ru/threads/zavod-ati-hd–6xxx–5xxx–4xxx.28890/
* HD7000, R5, R7, R9, RX — https://applelife.ru/threads/amd-hd7xx0-r5-r7-r9-rx.36269/

### Nvidia

* Fermi – https://applelife.ru/threads/zavod-nvidia-gt-x–465–470–480–560–570–580–590–610–620–630-fermi.27607/
* Kepler — https://applelife.ru/threads/nvidia-gt-x–640–650–670–680–690–770–780-titan-kepler.37131/
* Maxwell – https://applelife.ru/threads/nvidia-gt-x–980–970–750ti–750-maxwell.44019/

## Звук
### AppleALC:

* Релизы (скачивание) – http://github.com/vit9696/AppleALC/releases
* Поддерживаемые кодеки – http://github.com/vit9696/AppleALC/wiki/Supported-codecs
* Видео по установке – https://www.youtube.com/watch?v=xbLn_OkVuKY

* AppleHDA (Если нет поддержки со стороны AppleALC) — http://osxpc.ru/kexts/audio/applehda/
* VoodooHDA (Полностью рабочий аналог AppleHDA) — https://sourceforge.net/projects/voodoohda/files/latest/download
* Toleda HDMI — http://tonymacx86.com/threads/audio-hdmi-audio-applehda-guide.143760/

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

* Кекст — https://bitbucket.org/RehabMan/os-x-acpi-battery-driver/downloads/RehabMan-Battery-2015-1230.zip
* Патчи для DSDT (репозиторий) — http://raw.github.com/RehabMan/Laptop-DSDT-Patch/master

## МАТЕРИНСКИЕ ПЛАТЫ

* Предпочтительны к покупке — http://osxpc.ru/motherboards/

### Обсуждения:

* Все — https://applelife.ru/categories/materinskie-platy.26/
* Asrock — https://applelife.ru/forums/asrock.29/
* Asus — https://applelife.ru/forums/asus.28/
* Gigabyte — https://applelife.ru/forums/gigabyte.33/
* Intel — https://applelife.ru/forums/intel.34/
* MSI — https://applelife.ru/forums/msi.35/

## НОУТБУКИ

* Все — https://applelife.ru/forums/noutbuki.42/
* Acer — https://applelife.ru/search/1296474/?q=Acer&o=relevance&c[node]=42
* Asus — https://applelife.ru/search/1296475/?q=Asus&o=relevance&c[node]=42
* Dell — https://applelife.ru/search/1296476/?q=Dell&o=relevance&c[node]=42
* Lenovo — https://applelife.ru/search/1296473/?q=Lenovo&o=relevance&c[node]=42
* Samsung — https://applelife.ru/search/1296478/?q=Samsung&o=relevance&c[node]=42
* Toshiba — https://applelife.ru/search/1296480/?q=Toshiba&o=relevance&c[node]=42
* HP – https://applelife.ru/search/1296481/?q=HP&o=relevance&c[node]=42

## СИСТЕМА И ЮЗАБЕЛЬНОСТЬ

* Завод MacAppStore и iCloud; iMessage и FaceTime; HandOff и Continuity — http://osxpc.ru/faq/apple-services
* Работа с ACPI (DSDT, SSDT) — http://osxpc.ru/faq/acpi-manual/
* Регулировка яркости в ноутбуках — http://osxpc.ru/faq/brightness-laptop/
* Регулировка яркости клавишами Fn — http://osxpc.ru/faq/backlight-fn/
* Ошибка boot0: error — http://osxpc.ru/faq/boot0-error/
