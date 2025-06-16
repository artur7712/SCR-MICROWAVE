# Systemy czasu rzeczywistego – projekt

## Tytuł modelu:

**Kuchenka mikrofalowa**

## Dane studenta:

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
### Podsystem interfejsu - UI_Subsystem
### Podsystem grzewczy - Heating_Subsystem
