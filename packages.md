# Пакеты

Этот репозиторий в основном настроен на использование пакетов для ESPhome, которые представляют собой отдельные файлы, содержащие все связанные конфигурации для определенной функции.

## airgradient_api_d1_mini_no_sgp41.yaml

Загружает данные датчиков на [Панель управления AirGradient](https://app.airgradient.com/dashboard). Этот файл предназначен для устройств на базе чипа D1 Mini (AG Basic и AG Pro), которые не включают датчик SGP41 для VOC/NOx

## airgradient_api_d1_mini.yaml

Загружает данные датчиков на [Панель управления AirGradient](https://app.airgradient.com/dashboard). Этот файл предназначен для устройств на базе чипа D1 Mini (AG Basic и AG Pro) со всеми текущими датчиками, включая SGP41

## airgradient_api_d1_mini_insecure.yaml

Загружает данные датчиков на [Панель управления AirGradient](https://app.airgradient.com/dashboard) с использованием http вместо https. Некоторые платы, такие как ESP8266 D1 Mini, иногда могут попасть в цикл перезагрузки при общении по https. Оригинальная прошивка использовала http без проблем, поэтому предлагается этот вариант для устройств, которые в нем нуждаются.

Этот файл предназначен для устройств на базе чипа D1 Mini (AG Basic и AG Pro) со всеми текущими датчиками, включая SGP41

## airgradient_api_esp32-c3_dual_pms5003t.yaml

Загружает данные датчиков на [Панель управления AirGradient](https://app.airgradient.com/dashboard). Этот файл предназначен для устройств на базе чипа ESP32-C3 (AG ONE и OpenAir) с двумя датчиками PMS5003t. Разработан для модели Outdoor OpenAir O-PPT1

## airgradient_api_esp32-c3.yaml

Загружает данные датчиков на [Панель управления AirGradient](https://app.airgradient.com/dashboard). Этот файл предназначен для устройств на базе чипа ESP32-C3 (AG ONE и OpenAir) со всеми текущими датчиками для внутренних моделей

## airgradient_d1_mini_board.yaml

Конфигурация платы для устройств на базе чипа D1 Mini (AG Basic и AG Pro), теперь использующая фреймворк esp-idf, который уменьшает использование памяти и позволяет включить новые функции

## airgradient_esp32-c3_board_arduino.yaml

Конфигурация платы для устройств на базе чипа ESP32-C3 (AG ONE и OpenAir) с использованием оригинального фреймворка Arduino

## button_factory_reset.yaml

Включает кнопку для сброса устройства к заводским настройкам, что стирает всю nvram и все сохраненные настройки.

Полезно, если появляются предупреждающие сообщения о невозможности сохранения настроек

## captive_portal.yaml

Настраивает устройство для предоставления портала захвата для создания точки доступа, если wifi не подключен, чтобы его можно было подключить к новой сети wifi без переконфигурации файла конфигурации

## config_button.yaml

Включает кнопку конфигурации на устройстве AirGradient. Конфигурация по умолчанию предназначена для устройств на базе чипа ESP32-C3, но можно добавить дополнительную конфигурацию для изменения контакта для поддержки D1 Mini, если на устройстве установлена физическая кнопка (уже является частью конфигурационного файла для AG Pro v4.2)

```yaml
binary_sensor:
  - id: !extend config_button
    pin:
      number: D7
```

* Короткое нажатие - Переключение отображения температуры между C и F
* Нажатие и удержание до 5 секунд - Инициирование ручной калибровки Senseair S8 CO2. Убедитесь, что устройство уже находится на улице или возле открытого окна в течение 5+ минут перед инициированием

## diagnostic_esp32.yaml

Включает отладочную информацию датчиков для чипа ESP32-C3, которая очень подробна.

## diagnostic_esp8266.yaml

Включает отладочную информацию датчиков для чипа ESP8266 (D1 Mini), которая очень подробна.

## display_sh1106_multi_page.yaml

Конфигурация дисплея для AG Pro и ONE. Поддерживает несколько страниц, которые можно переключать, включив переключатели в интерфейсе Home Assistant

Доступна регулировка контрастности, которая может значительно затемнить дисплей, но не отключит его полностью

Потребляет больше оперативной памяти, чем конфигурация с одной страницей. Если возникают проблемы с устройствами, особенно с D1 Mini, рассмотрите возможность использования конфигурации с одной страницей.

* Страница по умолчанию AirGradient
* Страницы сводки с большим шрифтом
* Качество воздуха только со значениями CO2 и PM2.5
* Температура и влажность воздуха
* Значения VOC и NOx
* Комбинированная страница с несколькими значениями датчиков

## display_sh1106_single_page.yaml

Конфигурация дисплея для AG Pro и ONE. Отображает только одну страницу на основе стандартного вида AirGradient

Доступна регулировка контрастности, которая может значительно затемнить дисплей, но не отключит его полностью

## display_ssd1306.yaml

Конфигурация дисплея для AG Basic

## led_co2.yaml

Светодиодная полоса в AG ONE, отражающая значения нескольких датчиков.

Смешивает цвета от зеленого>желтого>оранжевого>красного>фиолетового на основе чисел, предоставленных AirGradient. Значения для каждого цвета можно изменить, добавив раздел подстановок в вашу конфигурацию.

```yaml
substitutions:
  co2_green: '400'
  co2_yellow: '1000'
  co2_red: '2000'
  co2_purple: '4000'
```

## led_combo.yaml

Светодиодная полоса в AG ONE, отражающая значения нескольких датчиков. Левые 5 светодиодов отражают уровни CO2, средние 5 светодиодов отражают уровни PM2.5, крайний правый указывает на TVOC. (То же, что и дисплей)

Смешивает цвета от зеленого>желтого>оранжевого>красного>фиолетового на основе чисел, предоставленных AirGradient. Значения для каждого цвета можно изменить, добавив раздел подстановок в вашу конфигурацию.

```yaml
substitutions:
  co2_green: '400'
  co2_yellow: '1000'
  co2_red: '2000'
  co2_purple: '4000'
  pm_2_5_green: '0'
  pm_2_5_yellow: '11'
  pm_2_5_red: '56'
  pm_2_5_purple: '201'
  voc_green: '100'
  voc_yellow: '150'
  voc_red: '250'
  voc_purple: '400'
  voc_blue: '50'
```

  ![1715467068556](image/README/1715467068556.png)

## led_pm25.yaml

Светодиодная полоса в AG ONE отражает уровни PM2.5.

Смешивает цвета от зеленого>желтого>оранжевого>красного>фиолетового на основе чисел, предоставленных AirGradient. Значения для каждого цвета можно изменить, добавив раздел подстановок в вашу конфигурацию.

```yaml
substitutions:
  pm_2_5_green: '0'
  pm_2_5_yellow: '11'
  pm_2_5_red: '56'
  pm_2_5_purple: '201'
```

## led_tvoc.yaml

Светодиодная полоса в AG ONE отражает уровни VOC.

Смешивает цвета от синего>зеленого>фиолетового на основе чисел, предоставленных AirGradient. Значения для каждого цвета можно изменить, добавив раздел подстановок в вашу конфигурацию.

```yaml
substitutions:
  voc_green: '100'
  voc_yellow: '150'
  voc_red: '250'
  voc_purple: '400'
  voc_blue: '50'
```

## led.yaml

Настраивает 11-сегментную светодиодную полосу в моделях AG ONE.

Также включает переключатель Вкл/Выкл, яркость и затухание светодиодов

## sensor_nowcast_aqi.yaml

Настраивает датчики для значений AQI и NowCast и категории непосредственно на устройстве.

Предоставлено пользователем GitHub @Ex-Nerd

## sensor_bme680.yaml

Настраивает датчики из чипа BME 680 для предоставления температуры, влажности, давления, IAQ, эквивалента CO2 и дыхательного VOC.

Не является надежным источником CO2 или VOC.

## sensor_pms5003_extended_life.yaml

Настраивает датчик Plantower PMS5003.

По умолчанию собирает показания каждую секунду. Поскольку это устройство имеет ограниченный срок службы, можно продлить его жизнь, собирая показания реже. Может привести к новому режиму отказа, так как вентилятор выключается, позволяя насекомым проникнуть внутрь мимо вентилятора, который больше не вращается после 30 секунд.

Собирает показания каждые 2 минуты по умолчанию, но можно изменить, добавив запись в разделе подстановок, убедившись, что значение окружено двойными кавычками
`pm_update_interval: "2min"`

## sensor_pms5003t_2_extended_life.yaml

Настраивает второй датчик Plantower PMS5003T, когда установлено 2, например, в модели Open Air O-1PPT. Отчитывается о PM2.5, температуре и влажности.

Также применяет алгоритм компенсации от AirGradient для коррекции показаний температуры и влажности при использовании внутри корпуса Open Air

В дополнение к включению датчиков со второго устройства, также создает датчики, которые сообщают среднее значение двух устройств.

По умолчанию собирает показания каждую секунду. Поскольку это устройство имеет ограниченный срок службы, можно продлить его жизнь, собирая показания реже. Может привести к новому режиму отказа, так как вентилятор выключается, позволяя насекомым проникнуть внутрь мимо вентилятора, который больше не вращается после 30 секунд.

Собирает показания каждые 2 минуты по умолчанию, но можно изменить, добавив запись в разделе подстановок, убедившись, что значение окружено двойными кавычками
`pm_update_interval: "2min"`

## sensor_pms5003t_2.yaml

Настраивает второй датчик Plantower PMS5003T, когда установлено 2, например, в модели Open Air O-1PPT. Отчитывается о PM 2.5, температуре и влажности.

Также применяет алгоритм компенсации от AirGradient для коррекции показаний температуры и влажности при использовании внутри корпуса Open Air

В дополнение к включению датчиков со второго устройства, также создает датчики, которые сообщают среднее значение двух устройств.

## sensor_pms5003t_extended_life.yaml

Настраивает датчик Plantower PMS5003T. Отчитывается о PM 2.5, температуре и влажности.

Также применяет алгоритм компенсации от AirGradient для коррекции показаний температуры и влажности при использовании внутри корпуса Open Air

По умолчанию собирает показания каждую секунду. Поскольку это устройство имеет ограниченный срок службы, можно продлить его жизнь, собирая показания реже. Может привести к новому режиму отказа, так как вентилятор выключается, позволяя насекомым проникнуть внутрь мимо вентилятора, который больше не вращается после 30 секунд.

Собирает показания каждые 2 минуты по умолчанию, но можно изменить, добавив запись в разделе подстановок, убедившись, что значение окружено двойными кавычками
`pm_update_interval: "2min"`

## sensor_pms5003t_uncorrected.yaml

Настраивает датчик Plantower PMS5003T. Отчитывается о PM 2.5, температуре и влажности.

Не применяет алгоритм компенсации для предоставления значений непосредственно с датчика

## sensor_pms5003t.yaml

Настраивает датчик Plantower PMS5003T. Отчитывается о PM 2.5, температуре и влажности.

Также применяет алгоритм компенсации от AirGradient для коррекции показаний температуры и влажности при использовании внутри корпуса Open Air

## sensor_pms5003_uncorrected.yaml

Настраивает датчик Plantower PMS5003, используя необработанные значения с датчика

Отчитывается о PM 2.5, PM 10, PM 1.0, PM 0.3 и индексе качества воздуха на основе текущих показаний.

## sensor_pms5003.yaml

Настраивает датчик Plantower PMS5003.

Применяет алгоритмы коррекции, предоставленные AirGradient

https://www.airgradient.com/documentation/correction-algorithms/

Отчитывается о PM 2.5, PM 10, PM 1.0, PM 0.3 и индексе качества воздуха на основе текущих показаний.

## sensor_s8.yaml

Настраивает датчик Senseair S8.

Reports CO2 levels and enables buttons to initiate a manual baseline correction, show the correction interval, and disable/enable Automatic Baseline Correction feature

Also supports a substitution to introduce an offset to the CO2 readings.  May be helpful if wanting to calibrate to a number different than 400 ppm, or if the sensor is off by a known number.

To your main YAML file, add the following to the substitution section.  Numbers must be surrounded by single quotes and may be positive or negative.

```yaml
substitutions:
  co2_offset: '0'
```

## sensor_sgp41.yaml

Configures a Sensirion SGP41 sensor.

Reports VOC and NOx Index values.

Now supports modifying VOC and NOx learning time offset hours by adding the substitutions

```yaml
substitutions:
  # 12, 60, 120, 360, 720 are suggested values from AirGradient (range 1..1000)
  voc_learning_time_offset_hours: '12'
  nox_learning_time_offset_hours: '12'
```

## sensor_sht30.yaml

Configures a Sensirion SHT30 sensor

Reports temperature and humidity

## sensor_sht40.yaml

Configures a Sensirion SHT40 sensor

Reports temperature and humidity

## sensor_uptime.yaml

Configures an Uptime sensor

Reports how long since the last reboot in seconds

## sensor_wifi.yaml

Configures a WiFi sensor

These values are always negative and the closer they are to zero, the better the signal is.

## switch_safe_mode.yaml

Configures a switch to enable Safe Mode

This is useful in certain situations where a misbehaving component, or low memory state is preventing Over-The-Air updates from completing successfully.

## watchdog.yaml

Configures a hardware watchdog for devices that have one installed, such as AG ONE and Open Air

Sends a notification to the watchdog every 2.5 minutes to indicate it is still alive. If not received after ~5 minutes, device will reset
