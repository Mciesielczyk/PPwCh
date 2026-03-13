# Automatyzacja wdrożenia forum phpBB3 w chmurze Azure

## Autorzy

* Michał Antosiewicz
* Michał Ciesielczyk


## Opis projektu

Projekt polega na automatycznym wdrożeniu kompletnego środowiska serwerowego oraz aplikacji forum internetowego **phpBB3** na maszynie wirtualnej w chmurze Microsoft Azure.
Całość konfiguracji została zrealizowana przy użyciu narzędzia **Ansible**.

---

## Wykorzystane technologie

* **Chmura obliczeniowa:** Microsoft Azure (Virtual Machine)
* **System operacyjny:** Ubuntu Server 24.04 LTS
* **Automatyzacja:** Ansible
* **Stos technologiczny (LAMP):**

  * Serwer WWW: Apache
  * Baza danych: MySQL
  * Silnik aplikacji: PHP 
* **Aplikacja końcowa:** phpBB3 (CMS)

---

## Konfiguracja sieci i bezpieczeństwo

Dostęp do serwera jest ograniczony przez **Network Security Group (NSG)** do dwóch niezbędnych portów:

* **Port 22 (SSH)** – dostęp administracyjny zabezpieczony kluczem asymetrycznym (RSA)
* **Port 80 (HTTP)** – publiczny dostęp do interfejsu WWW forum

---

## Struktura plików

* `playbook.yml` – główny plik konfiguracyjny Ansible (instalacja pakietów, konfiguracja bazy, wdrożenie aplikacji)
* `inventory.ini` – plik zawierający adres IP serwera oraz parametry połączenia SSH
* `klucz-forum.pem` – klucz prywatny do autoryzacji SSH (**nie należy publikować w repozytorium publicznym**)

---

## Instrukcja wdrożenia

### 1. Przygotowanie pliku inventory.ini

Zaktualizuj adres IP w pliku `inventory.ini` na aktualny publiczny adres maszyny Azure:

```ini
[webserver]
ADRES_IP_SERWERA ansible_user=azureuser ansible_ssh_private_key_file=klucz-forum.pem
```

---

### 2. Uruchomienie automatyzacji

Z poziomu terminala (np. Azure Cloud Shell) wykonaj:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

### 3. Finalizacja instalacji

Po poprawnym zakończeniu działania Ansible otwórz przeglądarkę i przejdź pod adres:

```
http://ADRES_IP_SERWERA/phpBB3/install
```

Następnie postępuj zgodnie z instrukcjami instalatora graficznego, podając dane bazy danych zdefiniowane w `playbook.yml`.

---
## O aplikacji

Wdrożona aplikacja **phpBB3** to klasyczne forum internetowe umożliwiające komunikację użytkowników w formie wątków dyskusyjnych.
Użytkownicy mogą zakładać nowe tematy, dodawać posty oraz odpowiadać na istniejące dyskusje w formie komentarzy.
![alt text](<Zrzut ekranu 2026-03-13 135102.png>)
![alt text](<Zrzut ekranu 2026-03-13 135034.png>)


---


## Test działania na prezentacji

Podczas prezentacji projektu zostało przetestowane poprawne działanie automatyzacji przy użyciu narzędzia **Ansible**.
W ramach demonstracji wykonano ponowne uruchomienie playbooka (utworzono nowego użytkownika forum o nazwie **patryk**) oraz potwierdzono prawidłową konfigurację środowiska serwerowego.

![alt text](<Zrzut ekranu 2026-03-13 135437.png>)
![alt text](<Zrzut ekranu 2026-03-13 135634.png>)
![alt text](<Zrzut ekranu 2026-03-13 134959.png>)

---


## Przygotowanie środowiska

Przed rozpoczęciem procesu automatyzacji konieczne było utworzenie maszyny wirtualnej w chmurze Microsoft Azure.
Na utworzonej instancji zainstalowano system operacyjny Ubuntu Server oraz skonfigurowano podstawowe ustawienia sieciowe i dostęp SSH z wykorzystaniem klucza prywatnego.
![alt text](<Zrzut ekranu 2026-03-13 135647.png>)


---




