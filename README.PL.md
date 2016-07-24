# Moduł PayU dla PrestaShop
``Moduł jest wydawana na licencji GPL.``

**Jeżeli masz jakiekolwiek pytania lub chcesz zgłosić błąd zapraszamy do kontaktu z naszym wsparciem pod adresem: tech@payu.pl.**

## Spis treści

* [Cechy i kompatybilność](#cechy-i-kompatybilno)
* [Wymagania](#wymagania) 
* [Instalacja](#instalacja)
* [Aktualizacja](#aktualizacja)
* [Konfiguracja](#konfiguracja)
* [Więcej o cechach](#wicej-o-cechah)
    * [Wielowalutowość](#wielowalutowo)
    * [Wyświetlenie metod płatności](#wywietlanie-metod-patnoci)
    * [Ponowienie płatności](#ponowienie-platnoci)

## Cechy i kompatybilność
Moduł płatności PayU dodaje do PrestaShop opcję płatności PayU i pozwala na następujące operacje:

| Cecha | Presta 1.4 | Presta 1.5 | Presta 1.6 |
|---------|:-----------:|:-----------:|:-----------:|
| Utworzenie płatności (wraz z rabatami) | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Odebranie lub odrzucenie płatności (w przypadku wyłączonego autoodbioru) | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Utworzenie zwrotu (pełnego lub częściowego) | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Wyświetlenie metod płatności i wybranie metody na stronie podsumowania zamówienia | :x: | :white_check_mark: | :white_check_mark: |
| Ponowienie płatności przez klienta w przypadku anluowania | :x: | :white_check_mark: | :white_check_mark: |
| Wielowalutowość | :white_check_mark: | :white_check_mark: | :white_check_mark: |

Więcej informacji o cechach można znaleźć w rozdziale [Więcej o cechach](#wicej-o-cechah) 

**Wszyskie opisy w tej instrukcji odnoszą się do PrestaShop 1.6, w wersji 1.5 i 1.4 należy używać opcji analogicznych**.

## Wymagania

**Ważne:** Moduł ta działa tylko z punktem płatności typu `Checkout`.

Do prawidłowego funkcjonowania modułu wymagane są następujące rozszerzenia PHP: [cURL][ext1] i [hash][ext2].

## Instalacja

### Opcja 1 
**przeznaczona dla użytkowników bez dostępu poprzez FTP do instalacji PrestaShop**

1. Pobierz moduł z [repozytorium GitHub][ext3] jako plik zip
1. Rozpakuj pobrany plik
1. **Utwórz archiwum zip z katalogu `payu`**
1. Przejdź do strony administracyjnej swojego sklepu PrestaShop [http://adres-sklepu/adminxxx].
1. Przejdź do `Moduły` » `Moduły i usługi`
1. Naciśnij przycisk `Dodaj nowy moduł` i wybierz plik z archiwum modułu (utworzonej w punkcie 3)
1. Naciśnij przycisk `Prześlij moduł`

### Opcja 2 
**przeznaczona dla użytkowników z dostępem poprzez FTP do instalacji PrestaShop**
1. Pobierz moduł z [repozytorium GitHub][ext3] jako plik zip
1. Rozpakuj pobrany plik
1. Połącz się z serwerem ftp i skopiuj katalog `payu` z rozpakowanego pliku do katalogu `modules` swojego sklepu PrestaShop  

## Aktualizacja

1. Zaktualizuj piki moduł zgodnie z punkctem [Instalacja](#instalacja)
1. Przejdź do `Moduły` » `Moduły i usługi` - zostanie przeprowadzona automatyczna aktualizacja modułu jeżli jest wymagana 
1. Przejdź do `Parametry zaawansowane` » `Wydajność` i naciśnij przycisk `Wyczyść pamięć podręczną`  

## Konfiguracja

1. Przejdź do strony administracyjnej swojego sklepu PrestaShop [http://adres-sklepu/adminxxx].
1. Przejdź do `Moduły` » `Moduły i usługi`
1. Wyszukaj `PayU` i naciśnij `Konfiguruj`

### Parametry konfiguracyjne

#### Sposób integracji

| Parameter | Opis | 
|---------|-----------|
| Wyświetlaj metody płatności na stronie podsumowania zamówienia w PrestaShop | **Tak** - motedy płatności zostaną wyświetlone na stronie podsumowania zamównia w PrestaShop<br>**Nie** - po złożeniu zamówienia a PrestaShop nastąpi automatyczne przekierwoanie do PayU |


#### Parametry POS-ów

Dla każdej waluty w dodanej w PrestaShop należy dodać parametry:

| Parameter | Opis | 
|---------|-----------|
| Id punktu płatności| Identyfikator POS-a z systemu PayU |
| Drugi klucz MD5 | Drugi klucz MD5 z systemu PayU |
| OAuth - client_id | client_id dla protokołu OAuth z systemu PayU |
| OAuth - client_secret | client_secret for OAuth z systemu PayU |

##### Przykład konfiguracji POS-a

PrestaShop:

![presta_pos_config][img1]

Konfiguracja POS-a w panelu administracyjnym PayU:

![pos_configuration_keys][img2]

#### Statusy płatności
Mapowanie statusów płatności w PayU na statusy w skepie PrestaShop

| Parameter | Opis | Domyślna wartość | 
|---------|-----------|-----------|
| Rozpoczęta | Płatność w statusie `NEW` i `PENDING` | Płatność PayU rozpoczęta |
| Oczekuje na odbiór | Płatność w statusie `WAITING_FOR_CONFIRMATION` i `REJECTED` | Płatność PayU oczekuje na odbiór |
| Zakończona | Płatność w statusie `COMPLETED` | Płatność zaakceptowana |
| Anulowana | Płatność w statusie `CANCELED` | Płatność PayU anulowana |

### Więcej o cechach

#### Wielowalutowość
W systemach PayU w ramach POS-a można posługiwać się tylko jedną walutą. Jeżeli chcemy procesować transakcje w sklepie PrestaShop w wielu walutach niezbędne jest dodanie konfiguracji dla każdej waluty z osobna.   

#### Wyświetlenie metod płatności 
Przy ustawionej opcji **Wyświetlaj metody płatności na stronie podsumowania zamówienia w PrestaShop** na `Tak` po wybraniu metody płatności PayU wyświetli się strona z ikonami banków bezpośrednio w sklepie PrestaShop.
Ikony banków, które są wyświetlane pobierane są z konfiguracji POS-a w PayU w zależności od wybranej waluty.  

![payment_methods][img3]

Po wybraniu banku lub płatności kartą i naciśnięciu przycisku `Potwierdzam zamówienie i płacę` nastąpi bezpośrednie przekierowanie na stronę banku lub w przypadku płatności kartą na stronę formatki kartowej.  

#### Ponowienie płatności
W przypadku nieudanej płatności w PayU możliwe jest ponowienie takiej płatności samodzielnie przez kupującego.

Żeby kupujący mógł ponowić płatność muszą być spełnione następujace warunki: 
* status ostatniej płatności z PayU musi mieć status CANCELED
* status zamówienia w PrestaShop musi być zgodny ze statusem wybranym w konfiguracji wtyczki `Statusy płatności` » `Anulowana`    

Kupującemu w `Szczegółach zamówinia` wyświetlany jest przycisk `Ponów płatność z PayU` 

![retry_payment][img4]

W panelu administracyjnym w szczegółach zamówienia wyświetlane są wszystkie utworzone płatności w PayU wraz ze statusami.

<!--LINKS-->

<!--external links:-->
[ext1]: http://php.net/manual/en/book.curl.php
[ext2]: http://php.net/manual/en/book.hash.php
[ext3]: https://github.com/PayU/plugin_prestashop

<!--images:-->
[img1]: https://raw.github.com/PayU/plugin_prestashop/master/readme_images/presta_pos_config.png
[img2]: https://raw.github.com/PayU/plugin_prestashop/master/readme_images/pos_configuration_keys.png
[img3]: https://raw.github.com/PayU/plugin_prestashop/retryPayment/readme_images/bramki_platnosci.png
[img4]: https://raw.github.com/PayU/plugin_prestashop/retryPayment/readme_images/ponow_platnosc.png