# Agenda
* Podstawy
* Edytory i Driver
* Request Factory
* Jukito - http://jukito.arcbees.com/
* gwt-test-utils - https://github.com/gwt-test-utils/gwt-test-utils
* Połączenie Jukito i GwtTest - @RunWith(JukitoGwtTestRunner.class)
* Moduły Testowe



# Build & Run
* mvn clean install
* mvn gwt:run

 
# Podstawy
* SUT - System Under Test
* DOC - Dependend On  Component
* Fixtura - zbudowanie mikro środowiska dla SUT- czyli  przygotowanie DOC  
* BDD - Given, When, Then
* nazwy testów
* Practical Unit Testing - Tomek Kaczanowski
 
# Edytory i Driver
* Abstrakcja i automat do ustawiania modelu i pobierania modelu z formatki
* Graf edytorów odpowiada grafowi domeny
* Stanowy driver wpisuje modele do edytorów i po zakończeniu edycji przez user'a aktualizuje modele

# Request Factory
* Operowanie na projekcjach modelu JPA
* Brak problemu z Lazy Init
* Automatyczne rewrittery
* Automatyczny binding do Edytorów
* ATP na etapie kompilacji - kontrola kontraktu

# Jukito
http://jukito.arcbees.com/
## Możliwości Jukito
* wstrzykiwanie DOC na pola oraz do metod
* resetowanie DOC oraz SUT przed wykonaniem kolejnej metody testowej  - @TestSingleton
* Własne moduły Guice

## Konfiguracja Jukito
* @RunWith(JukitoRunner.class) na klasie testu
* klasa wewnętrzna z modułami Guice:   public static class A extends JukitoModule


## Przykłady
* RespectProvidesAnnotationInModuleTest (jukito code base)
* RespectTestScopeWhenUsingAbstractModuleTest (jukito code base)
* TestBrowserHistoryTestImpl
* TestEventBusTestImpl

# EDRunner 
* motywacja
* jak działa
* do czego może się przydać
* EnvironmentDependentModulesTest (jukito code base)

## Uwagi
* Scope @TestSingleton jest używany domyślnie dla klas. Interfejsy są bindowane w normalnym Scope

# gwt-test-utils
https://github.com/gwt-test-utils/gwt-test-utils
## Możliwości
* brak problemu z GWT.create()
* symulacja przeglądarki (loopend, wypełnienie pola tekstowego, klikanie, ustawianie locale itp)
* generowanie kodu w teście (Editors, i18n)
 
## Konfiguracja
* extends GwtTest
* @GwtModule("com.efigence.efinity.gxt.Efinity-web-gxt") na klasie testu
* gwt-test-utils.properties w src/test/resources z deklaracjami modułów *.gwt.xml
* com.efigence.efinity.gxt.Efinity-web-gxt = gwt-module

## Przykłady
* ToggleButtonTest
* AutoBeanCodexTest
* MyMessagesTest
* ClientBundleTest
* SafeHtmlTest
* UiBinderWithListBoxTest
* CookiesTest
* FlexTableTest
* SchedulerTest
 

# Połączenie Jukito i GwtTest - @RunWith(JukitoGwtTestRunner.class)
## Możliwości
* Wstrzykiwanie zależności jak w czystym Jukito
* Wszystkie dobrodziejstwa gwt-test-utils

## Konfiguracja
* To co typowo dla gwt-test-utils oraz Jukito
zamiast @RunWith(JukitoRunner.class) stosujemy @RunWith(JukitoGwtTestRunner.class) na klasie testu

## Przykłady
* JukitoGwtTestRunnerTest (gwt-test-utils code base) 
* TestAddressDataEditor - testy prostego edytora
* TestTwoAddressOneDriver - test bardziej złożonego edytora
 
# Pułapki
* niekompletne/nieprawidłowe mockowanie
* deffered command i mockowanie asynchronicznych zdarzeń

# Usecases a la WebDriver
## Jako U rejestruje swój profil
* Otwieram aplikację
* Klikam "rejestruj profil"
* Wypełniam formatkę na ekranie
* Klikam zapisz
* Przeglądam stronę swojego nowego profilu i oczekuję że dane zostały zapisane

## Jako U edytuję swój profil
* Klikam "Edytuj profil"
* Zmieniam adres zamieszkania
* Zapisuje zmiany i oczekuję że mój profil został zakutalizowany
