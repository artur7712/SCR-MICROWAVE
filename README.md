# Systemy czasu rzeczywistego

## 1. Tytuł modelu:
Mikrofalówka

## 2. Dane studentów:
```
Błażej Dudek
Artur Bogacki
bdudek@student.agh.edu.pl
abogacki@student.agh.edu.pl
```

## 3. Opis modelowanego systemu
### Opis ogólny
```Zamodelowany system to inteligentna mikrofalówka wyposażona w klasyczne funkcje podgrzewania, rozmrażania i grillowania, z dodatkowymi elementami bezpieczeństwa, czujnikami oraz interfejsem użytkownika. System uwzględnia detekcję obecności drzwi, monitorowanie temperatury, kontroli czasu pracy, a także uwzględnia możliwość zatrzymania pracy przez użytkownika w dowolnym momencie.```

### Opis szczegółowy
```System umożliwia przygotowanie potraw w trzech trybach: podgrzewanie mikrofalowe, grillowanie oraz tryb mieszany (mikrofale + grill). Użytkownik może wybrać tryb, czas, moc i wagę potrawy z poziomu panelu dotykowego. Po zatwierdzeniu parametrów mikrofalówka uruchamia wybrany proces.```
```Bezpieczeństwo zapewniają czujniki otwarcia drzwi, czujniki temperatury oraz detektory obecności jedzenia. Praca mikrofalówki zostanie natychmiast zatrzymana w przypadku otwarcia drzwi lub przegrzania. W sytuacjach awaryjnych, takich jak iskrzenie czy dym, aktywowany jest tryb awaryjny, który wyłącza wszystkie źródła energii i uruchamia wentylację.```
```System posiada funkcję inteligentnego rozmrażania, która automatycznie dobiera czas i moc na podstawie masy produktu, a także czujnik pary, który pozwala zakończyć gotowanie w momencie uzyskania pożądanej wilgotności potrawy.```
```Czas pracy kontrolowany jest przez osobny wątek, który może zostać nadpisany np. przez naciśnięcie przycisku STOP lub przez system bezpieczeństwa.```

## 4. Komponenty systemu:

### Główna logika sterująca

    system MicrowaveController – główny komponent zarządzający pracą mikrofalówki, koordynuje komunikację i reakcje urządzeń.

### Urządzenia fizyczne

    device MicrowaveEmitter – generator mikrofal odpowiedzialny za podgrzewanie jedzenia.

    device GrillElement – element grzewczy do grillowania.

    device TurntableMotor – silnik obracający talerz.

    device DoorSensor – czujnik zamknięcia drzwi (przerywa pracę przy otwartych drzwiach).

    device TemperatureSensor – czujnik temperatury wewnątrz komory.

    device HumiditySensor – czujnik pary/wilgotności wewnątrz komory.

    device SmokeDetector – detektor dymu wykrywający możliwe awarie (np. przypalenie).

    device FoodPresenceSensor – czujnik wykrywający obecność jedzenia w komorze.

    device WeightSensor – czujnik masy potrawy (dla automatycznego doboru parametrów).

### Interfejs użytkownika

    device TouchPanel – panel dotykowy do wprowadzania parametrów pracy.

    device StartButton – przycisk uruchamiający pracę mikrofalówki.

    device StopButton – przycisk natychmiastowego zatrzymania pracy.

    device DisplayScreen – ekran wyświetlający ustawienia i komunikaty.

    device LEDIndicator – wskaźnik stanu (np. gotowe, praca, błąd).

### Funkcje i wątki pomocnicze

    thread CookingTimer – wątek odliczający czas pracy mikrofalówki.

    thread SafetyMonitor – wątek stale monitorujący temperaturę, drzwi i inne czujniki.

    thread AutoDefrostController – wątek automatyzujący rozmrażanie na podstawie wagi.

    thread SteamDetectorControl – kontrola zakończenia gotowania na podstawie pary.

    thread EmergencyShutdown – natychmiastowe zatrzymanie działania w przypadku awarii.

### Komunikacja

    bus CommunicationBus – magistrala komunikacyjna łącząca wszystkie komponenty systemu.
