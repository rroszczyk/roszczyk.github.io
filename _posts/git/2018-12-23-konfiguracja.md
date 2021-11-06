---
layout: post
#toc: true
description: >
    [GIT - przewodnik praktyczny] Konfiguracja - czyli co i jak ustawiać żeby praca z Git była wygodniejsza. Git posiada długą listę parametrów konfiguracyjnych pozwalających dostosować do swoich potrzeb środowisko pracy, a ten opis zawiera podstawowe parametry konfiguracyjne.
hide_description: true
title: GIT&#58; Konfiguracja
#categories: [git]
tags: [git]
languages:
- pl
---

Git posiada długą listę parametrów konfiguracyjnych pozwalających dostosować do swoich potrzeb środowisko pracy oraz zdefiniować informacje o użytkowniku (autorze) wprowadzanych zmian. Wszystkie ustawienia można ustawić ręcznie w pliku _.gitconfig_ w katalogu domowym zalogowanego użytkownika bądź poprzez wykonanie odpowiednich komend.
{:.text-justify}

<!--more-->

## Ustawienie parametrów dla użytkownika

Pierwszą rzeczą, którą powinno się ustawić w każdej nowej instalacji Git, jest nazwa użytkownika. Git rejestruje tę informacje wraz ze wszystkimi zmianami wprowadzanymi do repozytorium kodu. Dodatkowo informacja ta jest wykorzystywana przez usługi innych firm, np.: GitHub. Najczęściej jako nazwę użytkownika wprowadza się imię i nazwisko autora bądź login dzięki czemu łatwo jest identyfikować zmiany wprowadzone zmiany we współdzielonym repozytorium. Wartości parametrów warto umieszczać w cudzysłowach, szczególnie jeśli zawierają spacje.
{:.text-justify}

Dla ukrycia swojego adresu mailowego przez innymi użytkownikami współdzielonych repozytoriów github warto posłużyć się specjalnym adresem mail w postaci nazwa_użytkownka@users.noreply.github.com. Przykład został zamieszczony poniżej.
{:.text-justify}

```bash
git config --global user.name "Radosław Roszczyk"
git config --global user.email "rroszczyk@users.noreply.github.com"
```

Dodanie parametru _--global_ powoduje zapamiętanie wprowadzonych danych we wcześniej wspomnianym pliku konfiguracyjnym _.gitconfig_, dzięki czemu parametry te stają się parametrami domyślnymi dla wszystkich nowych repozytoriów. Pominięcie parametru powoduje ustawienie parametrów tylko dla lokalnego repozytorium co jest równoznaczne użyciu parametru _--local_. Lokalna konfiguracja zostaje zapisana w pliku _.git/config_ repozytorium i będzie nadrzędna w stosunku do konfiguracji globalnej.
{:.text-justify}

## Ustawianie domyślnego edytora

Domyślnym edytorem dla Git'a jest VIM. Do zmiany edytora ponownie posłużymy się przełącznikiem _config_, ale tym razem zmienimy parametr konfiguracyjny _core.editor_. Poniższy przykład zmienia domyślny edytor na nano:
{:.text-justify}

```bash
git config --global core.editor nano
```

## Modyfikacja konfiguracji

Jeżeli zajdzie potrzeba zmiany dowolnego z parametrów wystarczy dokonać jego nadpisania poprzez ponowne ustawienie parametru z nową wartością. W przypadku gdy zależy nam na usunięciu któregoś z parametrów należy posłużyć się przełącznikiem _--unset_. W poniższym przykładzie usunięta zostanie nazwa użytkownika z konfiguracji lokalnego repozytorium.
{:.text-justify}

```bash
git config --local --unset user.name
```

## Sprawdzanie konfiguracji

Poszczególne parametry konfiguracji można odczytać wykonując polecenie:
{:.text-justify}

```bash
git config user.name
git config user.email
```

Analogicznie jak przy ustawianiu pominięcie parametru _--global_ zwraca konfigurację lokalnego repozytorium. Jeśli chcemy odczytać konfigurację globalną należy posłużyć się parametrem:
{:.text-justify}

```bash
git config --global user.name
```

Oprócz pojedynczych parametrów możemy odczytać pełną konfigurację. Do tego celu służy przełącznik _--list_ i ponownie w połączeniu z _--global_ zwróci konfigurację globalną, natomiast bez parametru otrzymamy ustawienia lokalnego repozytorium:
{:.text-justify}

```bash
git config --global --list
```

## Tworzenie aliasów

Git domyślnie nie posiada utworzonych żadnych aliasów. Poniższe polecenia powodują wygenerowanie czterech aliasów do popularnych poleceń Git'a i będą szczególnie przydatne dla użytkowników którzy wcześniej posługiwali się SVN'em:
{:.text-justify}

```bash
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
```