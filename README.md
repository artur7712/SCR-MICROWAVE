# Systemy czasu rzeczywistego – projekt

## Tytuł modelu:

**Kuchenka mikrofalowa**

## Dane studentów:

Błażej Dudek - bdudek@student.agh.edu.pl
Artur Bogacki - arturbogacki@student.agh.edu.pl

---

## Opis modelowanego systemu:

### Opis ogólny

Zamodelowany system przedstawia działanie mikrofalówki jako złożonego systemu czasu rzeczywistego. Głównymi elementami systemu są interfejs użytkownika oraz system grzewczy. Użytkownik poprzez przyciski steruje pracą mikrofalówki (rozpoczęcie podgrzewania, ustawienie czasu, zatrzymanie pracy). System grzewczy odpowiada za fizyczne działanie lampy grzewczej oraz talerza obrotowego, a także za monitorowanie temperatury i stanu drzwi. 

System zapewnia wzajemną komunikację między podsystemami za pomocą portów danych i zdarzeń oraz uwzględnia wymagania niskiego zużycia przepustowości oraz budżetu MIPS dla procesorów i pamięci.

---

### Opis szczegółowy

Użytkownik mikrofalówki może za pomocą przycisku Start rozpocząć proces podgrzewania potrawy. Wybór czasu podgrzewania realizowany jest przy pomocy selektora czasu. Informacje o stanie mikrofalówki (np. zakończenie podgrzewania) prezentowane są na wyświetlaczu oraz sygnalizowane za pomocą sygnału dźwiękowego (buzzer).

System mikrofalówki automatycznie kontroluje bezpieczeństwo – np. blokuje drzwi w trakcie pracy lub nie pozwala na uruchomienie, gdy drzwi są otwarte. System grzewczy steruje lampą grzewczą oraz talerzem obrotowym i kontroluje temperaturę wewnątrz urządzenia. 

Dodatkowo czujniki temperatury i położenia drzwi umożliwiają dynamiczne dostosowanie działania mikrofalówki do aktualnych warunków w komorze grzewczej. 

Wszystkie elementy są połączone z dedykowanymi procesorami, pamięcią i magistralami danych, co umożliwia wydajną i bezpieczną pracę systemu w czasie rzeczywistym.

---

## Komponenty:

### data:
- `MicrowaveCommand` – struktura danych reprezentująca polecenia przesyłane pomiędzy komponentami (`String`).
- `TemperatureValue` – wartość temperatury odczytywana z czujnika temperatury (`Integer`).
- `DoorStatus` – status drzwi mikrofalówki, informujący czy drzwi są otwarte lub zamknięte (`Boolean`).
- `TurntableCommand` – komenda sterująca talerzem obrotowym; przyjmuje wartości `"START"` lub `"STOP"` (enumeracja).
- `MagnetronCommand` – komenda sterująca magnetronem; przyjmuje wartości `"ON"` lub `"OFF"` (enumeracja).
- `TimeSetting` – wartość ustawionego przez użytkownika czasu pracy mikrofalówki (`Integer`).
- `DisplayText` – tekst wyświetlany na ekranie mikrofalówki (`String`).

### system:
- `MicrowaveSystem` – system nadrzędny, integrujący podsystem interfejsu użytkownika i podsystem grzewczy.
- `UI_Subsystem` – podsystem obsługujący interakcję z użytkownikiem.
- `Heating_Subsystem` – podsystem odpowiedzialny za realizację procesu podgrzewania.

### device:
- `StartButton` – przycisk uruchamiający proces podgrzewania.
- `StopButton` – przycisk zatrzymujący pracę mikrofalówki.
- `TimeSelector` – selektor umożliwiający ustawienie czasu podgrzewania.
- `Display` – wyświetlacz informujący użytkownika o stanie urządzenia.
- `Buzzer` – sygnalizator dźwiękowy informujący o zakończeniu podgrzewania.
- `LightLamp` – lampa wewnętrzna mikrofalówki.
- `DoorLock` – mechanizm blokujący drzwi w czasie pracy.
- `Magnetron` – lampa grzewcza.
- `Turntable` – silnik obracający talerz wewnątrz mikrofalówki.
- `TempSensor` – czujnik temperatury wewnątrz komory grzewczej.
- `DoorSensor` – czujnik otwarcia drzwi.

### processor:
- `UICPU` – procesor obsługujący podsystem interfejsu użytkownika.
- `HeatingCPU` – procesor sterujący podsystemem grzewczym.

### memory:
- `UIMemory` – pamięć wykorzystywana przez podsystem interfejsu użytkownika.
- `HeatingMemory` – pamięć wykorzystywana przez podsystem grzewczy.

### bus:
- `UIBus` – magistrala danych w podsystemie interfejsu użytkownika.
- `HeatingBus` – magistrala danych w podsystemie grzewczym.

## Model - rysunek

### Cały system - MicrowaveSystem:
![image](https://github.com/user-attachments/assets/0a4d409c-41ec-4df2-9310-4884d1947401)

### Podsystem interfejsu - UI_Subsystem
![image](https://github.com/user-attachments/assets/f4b9ee8f-e93e-471a-a83a-27e7c16d418a)


### Podsystem grzewczy - Heating_Subsystem
![image](https://github.com/user-attachments/assets/71101a2a-2c22-4bb0-b33c-650cb86e8fdc)



## Analizy
### BoundResourceBudgets:
Processor Summary Report: 
  Processor uiSubsystem.uiCPU: Total MIPS 5,000 MIPS of bound tasks within MIPS capacity 50,000 MIPS of uiSubsystem.uiCPU
  Processor heatingSubsystem.heatCPU: Total MIPS 10,000 MIPS of bound tasks within MIPS capacity 50,000 MIPS of heatingSubsystem.heatCPU

Memory Summary Report: 
  Total RAM 0.0 KB of bound tasks within Memory capacity 64.0 KB of uiSubsystem.uiMem
  Total ROM 0.0 KB of bound tasks within Memory capacity 256.0 KB of uiSubsystem.uiMem
  Total RAM 0.0 KB of bound tasks within Memory capacity 64.0 KB of heatingSubsystem.heatMem
  Total ROM 0.0 KB of bound tasks within Memory capacity 256.0 KB of heatingSubsystem.heatMem


Detailed Workload Report:  for Processor uiSubsystem.uiCPU with Capacity 50,000 MIPS

Component,Budget,Actual
  thread uiSubsystem.uiProcess.uiThread,   5,000 MIPS,  0,000 MIPS,thread MicrowaveSystem_impl_Instance.uiSubsystem.uiProcess.uiThread total 0,000 MIPS below budget 5,000 MIPS (100,0 % slack)
process uiSubsystem.uiProcess, 0,000 MIPS,5,000 MIPS,
Total,,5,000 MIPS


Detailed Workload Report:  for Processor heatingSubsystem.heatCPU with Capacity 50,000 MIPS

Component,Budget,Actual
  thread heatingSubsystem.heatProcess.heatThread,   10,000 MIPS,  0,000 MIPS,thread MicrowaveSystem_impl_Instance.heatingSubsystem.heatProcess.heatThread total 0,000 MIPS below budget 10,000 MIPS (100,0 % slack)
process heatingSubsystem.heatProcess, 0,000 MIPS,10,000 MIPS,
Total,,10,000 MIPS


Detailed Workload Report:  for memory uiSubsystem.uiMem with Capacity 64,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory uiSubsystem.uiMem with Capacity 256,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory heatingSubsystem.heatMem with Capacity 64,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory heatingSubsystem.heatMem with Capacity 256,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,

### BusLoad:
"Physical Bus","Capacity (KB/s)","Budget (KB/s)","Required Budget (KB/s)","Actual (KB/s)"
"uiBus","12500.0","25.0","3.75","0.0"
"heatBus","12500.0","25.0","3.875","0.0"

"Bus uiBus has data overhead of 0 bytes"
"Bound Virtual Bus/Connection","Capacity (KB/s)","Budget (KB/s)","Required Budget (KB/s)","Actual (KB/s)"
"startButton.pressOut -> uiProcess.uiThread.startRequest","","0.125","","0.0"
"timeSelector.timeOut -> uiProcess.uiThread.timeSelectIn","","0.625","","0.0"
"stopButton.pressOut -> uiProcess.uiThread.stopRequest","","0.125","","0.0"
"uiProcess.uiThread.displayOut -> display.displayIn","","2.5","","0.0"
"uiProcess.uiThread.lightLampOut -> lightLamp.lightIn","","0.125","","0.0"
"uiProcess.uiThread.doorLockOut -> doorLock.lockIn","","0.125","","0.0"
"uiProcess.uiThread.buzzerOut -> buzzer.buzzerIn","","0.125","","0.0"

"Bus heatBus has data overhead of 0 bytes"
"Bound Virtual Bus/Connection","Capacity (KB/s)","Budget (KB/s)","Required Budget (KB/s)","Actual (KB/s)"
"tempsensor.tempOut -> heatProcess.heatThread.tempIn","","1.25","","0.0"
"doorSensor.doorOpen -> heatProcess.heatThread.doorStatus","","0.125","","0.0"
"heatProcess.heatThread.magnetronOut -> magnetron.commandIn","","1.25","","0.0"
"heatProcess.heatThread.turntableOut -> turntable.commandIn","","1.25","","0.0"

### BoundResourceBudgets:
Processor Summary Report: 
  Processor uiSubsystem.uiCPU: Total MIPS 5,000 MIPS of bound tasks within MIPS capacity 50,000 MIPS of uiSubsystem.uiCPU
  Processor heatingSubsystem.heatCPU: Total MIPS 10,000 MIPS of bound tasks within MIPS capacity 50,000 MIPS of heatingSubsystem.heatCPU

Memory Summary Report: 
  Total RAM 0.0 KB of bound tasks within Memory capacity 64.0 KB of uiSubsystem.uiMem
  Total ROM 0.0 KB of bound tasks within Memory capacity 256.0 KB of uiSubsystem.uiMem
  Total RAM 0.0 KB of bound tasks within Memory capacity 64.0 KB of heatingSubsystem.heatMem
  Total ROM 0.0 KB of bound tasks within Memory capacity 256.0 KB of heatingSubsystem.heatMem


Detailed Workload Report:  for Processor uiSubsystem.uiCPU with Capacity 50,000 MIPS

Component,Budget,Actual
  thread uiSubsystem.uiProcess.uiThread,   5,000 MIPS,  0,000 MIPS,thread MicrowaveSystem_impl_Instance.uiSubsystem.uiProcess.uiThread total 0,000 MIPS below budget 5,000 MIPS (100,0 % slack)
process uiSubsystem.uiProcess, 0,000 MIPS,5,000 MIPS,
Total,,5,000 MIPS


Detailed Workload Report:  for Processor heatingSubsystem.heatCPU with Capacity 50,000 MIPS

Component,Budget,Actual
  thread heatingSubsystem.heatProcess.heatThread,   10,000 MIPS,  0,000 MIPS,thread MicrowaveSystem_impl_Instance.heatingSubsystem.heatProcess.heatThread total 0,000 MIPS below budget 10,000 MIPS (100,0 % slack)
process heatingSubsystem.heatProcess, 0,000 MIPS,10,000 MIPS,
Total,,10,000 MIPS


Detailed Workload Report:  for memory uiSubsystem.uiMem with Capacity 64,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory uiSubsystem.uiMem with Capacity 256,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory heatingSubsystem.heatMem with Capacity 64,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,


Detailed Workload Report:  for memory heatingSubsystem.heatMem with Capacity 256,000 KBYTE

Component,Budget,Actual
Total, ,0,000 KBYTE,

### WeightAnalysis
uiBus: [L] Sum of weights / gross weight is 0,010 kg (no limit specified)
startButton: [L] Sum of weights / gross weight is 0,050 kg (no limit specified)
display: [L] Sum of weights / gross weight is 0,150 kg (no limit specified)
buzzer: [L] Sum of weights / gross weight is 0,050 kg (no limit specified)
timeSelector: [L] Sum of weights / gross weight is 0,020 kg (no limit specified)
stopButton: [L] Sum of weights / gross weight is 0,050 kg (no limit specified)
lightLamp: [L] Sum of weights / gross weight is 0,100 kg (no limit specified)
doorLock: [L] Sum of weights / gross weight is 0,200 kg (no limit specified)
uiMem: [L] Sum of weights / gross weight is 0,020 kg (no limit specified)
uiCPU: [L] Sum of weights / gross weight is 0,050 kg (no limit specified)
uiSubsystem: [L] Sum of weights / gross weight is 0,700 kg (no limit specified)
heatBus: [L] Sum of weights / gross weight is 0,010 kg (no limit specified)
magnetron: [L] Sum of weights / gross weight is 2,500 kg (no limit specified)
turntable: [L] Sum of weights / gross weight is 0,800 kg (no limit specified)
tempsensor: [L] Sum of weights / gross weight is 0,030 kg (no limit specified)
doorSensor: [L] Sum of weights / gross weight is 0,040 kg (no limit specified)
heatMem: [L] Sum of weights / gross weight is 0,020 kg (no limit specified)
heatCPU: [L] Sum of weights / gross weight is 0,050 kg (no limit specified)
heatingSubsystem: [L] Sum of weights / gross weight is 3,450 kg (no limit specified)
MicrowaveSystem_impl_Instance: [L] Sum of weights / gross weight is 4,150 kg (no limit specified)

### NotBoundResourceBudgets:
Resource Summary: 
  MIPS capacity 100,000 MIPS : MIPS budget 15,000 MIPS
  2 out of 2 with MIPS capacity
  6 out of 6 with MIPS budget

  RAM capacity 128,000 KBYTE : RAM budget 12,000 KBYTE
  4 out of 4 with RAM capacity
  6 out of 6 with RAM budget

  ROM capacity 512,000 KBYTE : ROM budget 48,000 KBYTE
  4 out of 4 with ROM capacity
  6 out of 6 with ROM budget



Detailed Processor MIPS Capacity Report 

Component,Capacity
processor uiSubsystem.uiCPU, 50,000 MIPS,
processor heatingSubsystem.heatCPU, 50,000 MIPS,
Total, 100,000 MIPS,


Detailed MIPS Budget Report 

Component,Budget,Actual,Notes
  device uiSubsystem.startButton,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.display,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.buzzer,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.timeSelector,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.stopButton,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.lightLamp,   0,000 MIPS,  0,000 MIPS,
  device uiSubsystem.doorLock,   0,000 MIPS,  0,000 MIPS,
    thread uiSubsystem.uiProcess.uiThread,     5,000 MIPS,    0,000 MIPS,thread MicrowaveSystem_impl_Instance.uiSubsystem.uiProcess.uiThread total 0,000 MIPS below budget 5,000 MIPS (100,0 % slack)
  process uiSubsystem.uiProcess,   0,000 MIPS,  5,000 MIPS,
system uiSubsystem, 0,000 MIPS,5,000 MIPS,
  device heatingSubsystem.magnetron,   0,000 MIPS,  0,000 MIPS,
  device heatingSubsystem.turntable,   0,000 MIPS,  0,000 MIPS,
  device heatingSubsystem.tempsensor,   0,000 MIPS,  0,000 MIPS,
  device heatingSubsystem.doorSensor,   0,000 MIPS,  0,000 MIPS,
    thread heatingSubsystem.heatProcess.heatThread,     10,000 MIPS,    0,000 MIPS,thread MicrowaveSystem_impl_Instance.heatingSubsystem.heatProcess.heatThread total 0,000 MIPS below budget 10,000 MIPS (100,0 % slack)
  process heatingSubsystem.heatProcess,   0,000 MIPS,  10,000 MIPS,
system heatingSubsystem, 0,000 MIPS,10,000 MIPS,
Total, ,15,000 MIPS,


Detailed RAM Capacity Report 

Component,Capacity
memory uiSubsystem.uiMem, 64,000 KBYTE,
memory heatingSubsystem.heatMem, 64,000 KBYTE,
Total, 128,000 KBYTE,


Detailed RAM Budget Report 

Component,Budget,Actual,Notes
  device uiSubsystem.startButton,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.display,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.buzzer,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.timeSelector,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.stopButton,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.lightLamp,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.doorLock,   0,000 KBYTE,  0,000 KBYTE,
    thread uiSubsystem.uiProcess.uiThread,     4,000 KBYTE,    0,000 KBYTE,thread MicrowaveSystem_impl_Instance.uiSubsystem.uiProcess.uiThread total 0,000 KBYTE below budget 4,000 KBYTE (100,0 % slack)
  process uiSubsystem.uiProcess,   0,000 KBYTE,  4,000 KBYTE,
system uiSubsystem, 0,000 KBYTE,4,000 KBYTE,
  device heatingSubsystem.magnetron,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.turntable,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.tempsensor,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.doorSensor,   0,000 KBYTE,  0,000 KBYTE,
    thread heatingSubsystem.heatProcess.heatThread,     8,000 KBYTE,    0,000 KBYTE,thread MicrowaveSystem_impl_Instance.heatingSubsystem.heatProcess.heatThread total 0,000 KBYTE below budget 8,000 KBYTE (100,0 % slack)
  process heatingSubsystem.heatProcess,   0,000 KBYTE,  8,000 KBYTE,
system heatingSubsystem, 0,000 KBYTE,8,000 KBYTE,
Total, ,12,000 KBYTE,


Detailed ROM Capacity Report 

Component,Capacity
memory uiSubsystem.uiMem, 256,000 KBYTE,
memory heatingSubsystem.heatMem, 256,000 KBYTE,
Total, 512,000 KBYTE,


Detailed ROM Budget Report 

Component,Budget,Actual,Notes
  device uiSubsystem.startButton,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.display,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.buzzer,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.timeSelector,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.stopButton,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.lightLamp,   0,000 KBYTE,  0,000 KBYTE,
  device uiSubsystem.doorLock,   0,000 KBYTE,  0,000 KBYTE,
    thread uiSubsystem.uiProcess.uiThread,     16,000 KBYTE,    0,000 KBYTE,thread MicrowaveSystem_impl_Instance.uiSubsystem.uiProcess.uiThread total 0,000 KBYTE below budget 16,000 KBYTE (100,0 % slack)
  process uiSubsystem.uiProcess,   0,000 KBYTE,  16,000 KBYTE,
system uiSubsystem, 0,000 KBYTE,16,000 KBYTE,
  device heatingSubsystem.magnetron,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.turntable,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.tempsensor,   0,000 KBYTE,  0,000 KBYTE,
  device heatingSubsystem.doorSensor,   0,000 KBYTE,  0,000 KBYTE,
    thread heatingSubsystem.heatProcess.heatThread,     32,000 KBYTE,    0,000 KBYTE,thread MicrowaveSystem_impl_Instance.heatingSubsystem.heatProcess.heatThread total 0,000 KBYTE below budget 32,000 KBYTE (100,0 % slack)
  process heatingSubsystem.heatProcess,   0,000 KBYTE,  32,000 KBYTE,
system heatingSubsystem, 0,000 KBYTE,32,000 KBYTE,
Total, ,48,000 KBYTE,



