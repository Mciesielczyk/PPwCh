# Automatyzacja wdrożenia forum phpBB3 w chmurze Azure

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

## Uwagi końcowe

Po zakończeniu instalacji, ze względów bezpieczeństwa, zaleca się **usunięcie katalogu instalacyjnego** z serwera.

---

## Autorzy:
* Michał Antosiewicz
* Michał Ciesielczyk

