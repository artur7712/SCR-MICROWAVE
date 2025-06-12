# Systemy czasu rzeczywistego

## 1. Tytuł modelu:
Mikrofalówka

## 2. Dane studentów:
```
Błażej Dudek
Artur Bogacki
bdudek@student.agh.edu.pl
arturbogacki@student.agh.edu.pl
```

## 3. Opis modelowanego systemu
```
Zamodelowany system to inteligentna mikrofalówka wyposażona w klasyczne funkcje podgrzewania, rozmrażania i grillowania, wzbogacona o rozbudowane mechanizmy bezpieczeństwa, czujniki oraz nowoczesny interfejs użytkownika. System został podzielony na dwa niezależne, współpracujące podsystemy: Sterowania i Interfejsu Użytkownika oraz Wykonawczy i Bezpieczeństwa. Podsystemy te komunikują się ze sobą za pośrednictwem wspólnej magistrali komunikacyjnej.
'''

'''
Mikrofalówka umożliwia przygotowanie potraw w trzech trybach: podgrzewanie mikrofalowe, grillowanie oraz tryb mieszany (mikrofale + grill). Użytkownik ma możliwość wyboru trybu, czasu, mocy i wagi potrawy z poziomu dotykowego panelu sterowania. Proces rozpoczyna się po zatwierdzeniu ustawień, a jego przebieg i stan są prezentowane na ekranie urządzenia. System wyposażony jest w czujniki otwarcia drzwi, temperatury, obecności jedzenia, a także detektor dymu i czujnik pary. W razie wykrycia nieprawidłowości praca mikrofalówki zostaje natychmiast wstrzymana, a w sytuacji awaryjnej aktywowany jest specjalny tryb wyłączający źródła energii i uruchamiający wentylację. Inteligentne rozmrażanie dobiera automatycznie optymalne parametry na podstawie masy potrawy i poziomu wilgotności.
```


## 4. Komponenty systemu:

## Podsystem 1: Sterowania i Interfejsu Użytkownika

### Główna logika sterująca
    system MicrowaveController – główny komponent zarządzający konfiguracją i przebiegiem pracy mikrofalówki, koordynujący działania podsystemów.

### Interfejs użytkownika

    device TouchPanel – panel dotykowy umożliwiający wybór trybu pracy, czasu, mocy oraz masy potrawy.

    device StartButton – przycisk uruchamiający pracę mikrofalówki zgodnie z ustawionymi parametrami.

    device StopButton – przycisk natychmiastowego zatrzymania pracy urządzenia.

    device DisplayScreen – ekran wyświetlający aktualne parametry pracy, komunikaty oraz stany urządzenia.

    device LEDIndicator – diodowy wskaźnik stanu informujący o trybie pracy mikrofalówki (gotowość, praca, błąd).

### Funkcje 

    device TouchPanel – panel dotykowy do wprowadzania parametrów pracy.

    device StartButton – przycisk uruchamiający pracę mikrofalówki.

    device StopButton – przycisk natychmiastowego zatrzymania pracy.

    device DisplayScreen – ekran wyświetlający ustawienia i komunikaty.

    device LEDIndicator – wskaźnik stanu (np. gotowe, praca, błąd).

### Funkcje i wątki pomocnicze

    thread CookingTimer – wątek odliczający czas pracy mikrofalówki, umożliwiający wstrzymanie odliczania w razie potrzeby (np. wciśnięcie STOP, awaria).

    thread SteamDetectorControl – wątek monitorujący poziom pary wodnej dla automatycznego zakończenia gotowania po osiągnięciu pożądanej wilgotności.

## Podsystem 1: Sterowania i Interfejsu Użytkownika

### Urządzenia wykonawcze
    
    device MicrowaveEmitter – generator mikrofal odpowiedzialny za podgrzewanie jedzenia.

    device GrillElement – element grzewczy służący do grillowania potraw.

    device TurntableMotor – silnik napędzający obrót talerza w komorze mikrofalówki.

### Czujniki bezpieczeństwa i kontroli
    device DoorLockSensor – czujnik kontrolujący stan drzwi, uniemożliwiający rozpoczęcie lub kontynuację pracy przy otwartych drzwiach.

    device TemperatureSensor – czujnik mierzący temperaturę wewnątrz komory grzewczej.

    device HumiditySensor – czujnik wilgotności/pory monitorujący poziom pary w komorze.

    device SmokeDetector – detektor dymu wykrywający potencjalne zagrożenia (przypalenie, iskrzenie).

    device FoodPresenceSensor – czujnik wykrywający obecność jedzenia w komorze.

    device WeightSensor – czujnik masy potrawy wykorzystywany w trybie automatycznego rozmrażania i doboru parametrów grzania.
### Funkcje i wątki pomocnicze
    thread SafetyMonitor – wątek stale monitorujący stan drzwi, temperaturę, obecność jedzenia oraz ewentualne zagrożenia wykrywane przez detektor dymu.

    thread EmergencyShutdown – wątek odpowiedzialny za natychmiastowe wyłączenie wszystkich źródeł energii i uruchomienie wentylacji w przypadku wykrycia awarii.

## Komunikacja

    bus CommunicationBus – magistrala komunikacyjna łącząca podsystemy Sterowania i Interfejsu Użytkownika z podsystemem Wykonawczym i Bezpieczeństwa, zapewniająca przepływ danych i poleceń między komponentami systemu.
