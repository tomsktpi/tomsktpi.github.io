---
layout: post
title: Настройка CamillaDSP для CM6206
---

Внешняя USB звуковая карта на cm6206 7.1  
В линуксе как ICUSBAUDIO7D  

![Карта на алике](../images/camilla/cm6206.png){:class="img-responsive"}  

**Понадобится**  
1. Raspberry Pi или PC (X86/X64)  
2. USB карта с несколькими выходами с поддержкой в Linux (взята cm6206)  
3. Стерео усилители по количеству полос колонки (у меня 3)  
4. Сами колонки (Heco Victa 700)  
5. Паяльник (удалить фильтры и припаять конденсатор на пищалку)  
6. Пучёк проводов для соединения всего со всем  
7. Измерительный микрофон  
8. Второй компьютер с установленной программой [REW](https://www.roomeqwizard.com/)  


**Начать:**  

По инструкции запустить [Volumio OS](https://volumio.com/get-started/)  
В секции плагины - поставить FusionDSP
В настройках плагина выбрать  Pure CamillaDSP gui  

![Вот так](../images/camilla/FusionDSPsettings.png)  

Жмакнуть кнопку Access to Camilla gui  

и вот оно..  

![ЮАЙ](../images/camilla/camillaGui.png)  


Теперь на странице http:\\volumio.local\**dev** включить терминал  

в терминале запустить alsamixer   
F6 для выбора карты (у меня ICUSBAUDIO7D), на вход выбрать Line  


Загрузить [файл](../images/camilla/LINE_IN_MEAS_v2.yml)  

Применить...

Ко входу подключить выход компа с REW  

Запусть музло..  

Можно мерять.  

Мерять каждый канал, отключая остальные в Mixer-е (не забывать загружать в DSP)  

Конфиг сделан для измерения с Use Acoustic Timing Reference  

По результатам  разработать фильтры, добавить в Filters и их добавить в Pipeline  

Добавить задержки, инерсию канала - для получения красивого импульса  

В [этом](https://www.youtube.com/watch?v=5x1hHGyCs_U) видео про импульс есть, ну и метод настройки  

Импульс без задержки твитера  

![Импульс без задержки](../images/camilla/StepNoDelay.png)  

Стремиться надо примерно к этому..

![Импульс с задержкой](../images/camilla/StepWithDelay.png)  

![задержка](../images/camilla/tweetDelay.png)  








