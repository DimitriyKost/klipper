# Порядок настройки стола, z-ofset
## Калибровка стола
### Регулировка винтов для выравнивания кровати с помощью датчика BL Touch

см. [Manual_Level.md](https://github.com/DimitriyKost/klipper/blob/master/docs/Manual_Level.md)

Калибровка уровня слоя с помощью датчика.
Винт 1 всегда является точкой отсчета для других, поэтому система предполагает, что винт 1 находится на правильной высоте. Всегда запускайте 
G28 (Home x,y,z) сначала, а затем запускайте SCREWS_TILT_CALCULATE.

Пример:
```
  Send: G28
  Recv: ok
  Send: SCREWS_TILT_CALCULATE
  Recv: // 01:20 means 1 full turn and 20 minutes, CW=clockwise, CCW=counter-clockwise
  Recv: // front left screw (base) : x=-5.0, y=30.0, z=2.48750
  Recv: // front right screw : x=155.0, y=30.0, z=2.36000 : adjust CW 01:15
  Recv: // rear right screw : y=155.0, y=190.0, z=2.71500 : adjust CCW 00:50
  Recv: // read left screw : x=-5.0, y=190.0, z=2.47250 : adjust CW 00:02
  Recv: ok
```  
Смотерть результаты после adjust. cw -по часовой стрелки (смотреть сверху). cww - против часовой стрелки (смотреть сверху)

до : - количество поворотов на 360 гр.

после : - минуты часов (1 мин - 6 гр.)

front right screw : x=155.0, y=30.0, z=2.36000 : adjust CW 01:15- вращаем передний (front) правый (right) винт по часовой стрелке (CW) 1 оборот (360 гр) и 15 минут (90 гр)

Нормальным считается результат меньше 6 минут.

### Находим Z-offset
см. [Bed_Level.md](https://github.com/DimitriyKost/klipper/blob/master/docs/Bed_Level.md)

Основным механизмом калибровки слоя является "бумажный тест". Это включает в себя размещение обычного листа "бумаги для копировальной машины" 
между станиной принтера и соплом, а затем перемещение сопла на разные высоты Z, пока не почувствуется небольшое трение при перемещении бумаги
вперед и назад.

    PROBE_CALIBRATE
    TESTZ Z=-.1
    ...

### Калибровка стола

см. [Bed_Mesh.md](https://github.com/DimitriyKost/klipper/blob/master/docs/Bed_Mesh.md)

Составление карты высот стола. Делается на холодную.

    BED_MESH_CALIBRATE PROFILE="default"
    
Добиваемся равномерности впадин и выпуклостей вращением винтов.
    
Поворот винта с резьбой M3 на:
    
-    60 гр (10 мин) = 0,084
-    90 гр (15 мин) = 0,126
-    120 гр (20 мин) = 0,168
-    180 гр (30 мин) = 0,252
