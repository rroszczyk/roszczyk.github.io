---
layout: post
title: Operacje plikowe w języku C
categories: [programowanie]
accent_image: /assets/img/key-bg.jpg
image: /img/kryptografia/enigma_1600x600.jpg
img: cover/files-min.png
ximg: tmb/files-min.jpg
hide_image: true
author: rroszczyk
tags: [c,pliki]
comments: false
description: >
   Systemy informatyczne często wykorzystują pliki do przechowywania danych. Operacje plikowe w języku C pozwalają na użycie zawartości tychże plików w programie komputerowym.
copyrights: Cover Image Photo by <a href="https://unsplash.com/@qwitka?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" target="_blank">Maksym Kaharlytskyi</a> on <a href="https://unsplash.com/photos/Q9y3LRuuxmg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" target="_blank">Unsplash</a>
    
---

Dzięki temu przewodnikowi poznasz obsługę plików w&nbsp;języku&nbsp;C. Niniejszy dokument pokazuje jak obsługiwać standardowe wejście / wyjście używając bazowych instrukcji języka&nbsp;C - **fprintf()**{:.maroon}, **fscanf()**{:.maroon}, **fread()**{:.maroon}, **fwrite()**{:.maroon}, **fseek()**{:.maroon} itp. Dodatkowo znajdują się tu opisy trybów w jakich można otworzyć plik z poziomu języka C.
{:.text-justify-has-drop-cap}

<!--more-->

## Typy plików
Mając do czynienia z plikami, należy wiedzieć o dwóch ich rodzajach:
- pliki tekstowe,
- pliki binarne.

Obydwa rodzaje plików nieco różną się od siebie z punktu widzenia zawartości oraz sposobu obsługi. Każdemu z nich są dedykowane nieco inne funkcje. 
{: .text-justify}

### Pliki tekstowe

Pliki tekstowe to zwykłe pliki zawierające dane tekstowe. Najczęściej mają rozszerzenie .txt. Możesz łatwo tworzyć pliki tekstowe za pomocą dowolnego prostego edytora tekstu. Plik tekstowy jest szczególną wersją pliku binarnego.
{: .text-justify}

Kiedy otworzysz tego typu pliki, zobaczysz całą zawartość w pliku jako zwykły tekst. Pliki te można prosto zmieniać i&nbsp;edytować. Wymagają one minimalnego wysiłku w&nbsp;utrzymaniu, są łatwe do odczytania, jednakże zapewniają najmniejsze bezpieczeństwo i&nbsp;zajmują więcej miejsca na dysku.
{: .text-justify}

### Pliki binarne

Pliki binarne to najczęściej pliki zawierające dane binarne. Zwyczajowo mają różne rozszerzenia, zależnie od danych jake są w nich przechowywane oraz jaki program je utworzył. Programy zazyczaj zamiast przechowywać dane w postaci zwykłego tekstu, przechowują je w&nbsp;postaci binarnej. Pliki binarne mogą pomieścić większą ilość danych, są dużo trudniejsze do odczytania i&nbsp;mogą zapewnić dużo lepsze bezpieczeństwo niż pliki tekstowe.
{: .text-justify}

## Operacje na plikach

W języku C&nbsp;można wykonywać cztery główne operacje na plikach, zarówno tekstowych jak i&nbsp;binarnych:

- tworzenie nowego pliku,
- otwieranie istniejącego pliku,
- zamykanie pliku,
- odczyt z i zapis informacji do pliku.

### Uchwyt pliku

Podczas pracy z&nbsp;plikami należy zadeklarować wskaźnik typu **FILE**{:.blue}. Zmienna **fptr**{:.blue} zdeklarowana w&nbsp;ten sposób stanowi uchwyt pliku, który jest wykorzystywany do komunikacji między systemem operacyjnym, a&nbsp;programem. 
{: .text-justify}

```c
FILE* fptr;
```

### Otwieranie pliku do odczytu oraz zapisu

Otwieranie pliku odbywa się za pomocą funkcji *fopen()* zdefiniowanej w&nbsp;pliku nagłówkowym *stdio.h*.

Składnia otwarcia pliku dla standardowego wejścia / wyjścia to:

```c
ptr = fopen("plik_do_otwarcia", "mode");
```

przykładowo:

```c
fopen("nazwa_pliku.txt", "w");

fopen("nazwa_pliku.bin", "rb");
```

Załóżmy, że plik nazwa_pliku.txt nie istnieje. Pierwsza funkcja tworzy nowy plik o&nbsp;nazwie nazwa_pliku.txt i&nbsp;otwiera go do zapisu zgodnie z&nbsp;trybem 'w'.
Tryb pisania pozwala na tworzenie i&nbsp;edycję (nadpisywanie) zawartości pliku.
{: .text-justify}

Załóżmy teraz, że drugi plik binarny nazwa_pliku.bin istnieje. Druga funkcja otwiera istniejący plik do odczytu w&nbsp;trybie binarnym&nbsp;'rb'.
Tryb czytania pozwala tylko na odczytanie pliku, nie można do niego pisać.
{: .text-justify}

| &nbsp;&nbsp;Tryb&nbsp;&nbsp; | &nbsp;&nbsp;Funkcja trybu               | &nbsp;&nbsp;Uwagi                                            |
|:-------:| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **r**   | Otwarcie do odczytu                                          | Jeśli plik nie istnieje, funkcja fopen() zwraca NULL.        |
| **rb**  | Otwarcie do odczytu w trybie binarnym                        | Jeśli plik nie istnieje, funkcja fopen() zwraca NULL.        |
| **w**   | Otwarcie do zapisu                                           | Jeśli plik istnieje to zostanie nadpisany, jeśli plik nie istnieje to zostanie utworzony. |
| **wb**  | Otwarcie do zapisu w trybie binarnym                         | Jeśli plik istnieje to zostanie nadpisany, jeśli plik nie istnieje to zostanie utworzony. |
| **a**   | Otwiera plik w trybie dodawania danych. Dane są dopisywane na końcu pliku. | Jeśli plik nie istnieje to zostanie utworzony.               |
| **ab**  | Otwiera plik w trybie dodawania danych. Dane są dopisywane na końcu pliku. | Jeśli plik nie istnieje to zostanie utworzony.               |
| **r+**  | Otwiera plik do odczytu i zapisu.                            | Jeśli plik nie istnieje, funkcja fopen() zwraca NULL.        |
| **rb+** | Otwiera plik do odczytu i zapisu w trybie binarnym.          | Jeśli plik nie istnieje, funkcja fopen() zwraca NULL.        |
| **w+**  | Otwiera plik do zapisu i odczytu.                            | Jeśli plik istnieje to zostanie nadpisany, jeśli plik nie istnieje to zostanie utworzony. |
| **wb+** | Otwiera plik do zapisu i odczytu w trybie binarnym.          | Jeśli plik istnieje to zostanie nadpisany, jeśli plik nie istnieje to zostanie utworzony. |
| **a+**  | Otwiera plik w trybie dodawania danych oraz odczytu.         | Jeśli plik nie istnieje to zostanie utworzony.               |
| **ab+** | Otwiera plik w trybie dodawania danych oraz odczytu w trybie binarnym | Jeśli plik nie istnieje to zostanie utworzony.               |

#### Odczyt i zapis plików tekstowych

Do odczytu i&nbsp;zapisu do pliku tekstowego używamy funkcji **fprintf()**{:.maroon} oraz **fscanf()**{:.maroon}.

Są one po prostu plikowymi odpowiednikami funkcji **printf()**{:.maroon} oraz **scanf()**{:.maroon}. Jedyna różnica polega na tym, że **fprintf()**{:.maroon} oraz **fscanf()**{:.maroon} wymagają podania wskaźnika do struktury **FILE**{:.blue}.
{: .text-justify}

##### Przykład 1: zapis do pliku tekstowego

Poniższy program pobiera od użytkownika liczbę i&nbsp;zapisuje w pliku *plik.txt*.
{: .text-justify}

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
   int num;
   FILE *fptr;

   // zamiast nazwy plik.txt można użyć innej wraz ze ścieżką dostępu
   fptr = fopen("plik.txt", "w");

   if(fptr == NULL)
   {
      printf("Błąd!");   
      exit(1);             
   }

   printf("Podaj liczbę: ");
   scanf("%d", &num);

   fprintf(fptr, "%d", num);
   fclose(fptr);

   return 0;
}
```

Po skompilowaniu i&nbsp;uruchomieniu powyższego programu można zobaczyć plik tekstowy o&nbsp;nazwie *plik.txt* utworzony w&nbsp;katalogu w&nbsp;którym został uruchomiony program. Po otwarciu tego pliku widać liczbę wpisaną przez użytkownika zapisaną w postaci tekstu.
{: .text-justify}

##### Przykład 2: odczyt z pliku tekstowego

Poniższy program otwiera wcześniej utworzony plik o&nbsp;nazwie *plik.txt* i&nbsp;wczytuje z&nbsp;niego zapisaną liczbę.
{: .text-justify}

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
   int num;
   FILE *fptr;

   if ((fptr = fopen("plik.txt", "r")) == NULL) {
       printf("Błąd otwarcia pliku!");

       // Koniec działania - zwracamy błąd numer 1
       exit(1);
   }

   fscanf(fptr,"%d", &num);

   printf("Liczba wczytana z pliku to: %d", num);
   fclose(fptr); 
  
   return 0;
}
```

Powyższy program odczytuje liczbę całkowitą znajdującą się w pliku *plik.txt*, a następnie wypisuje ją na ekranie.
{: .text-justify}

Jeśli udało się stworzyć plik przy użyciu programu z przykładu 1, to uruchomienie tego programu da liczbę całkowitą, wcześniej którą wprowadziłeś.
{: .text-justify}

W podobny sposób można wykorzystać inne funkcje do wczytywania danych z pliku, takie jak **fgetchar()**{:.maroon}, **fputc()**{:.maroon} itp.
{: .text-justify}

### Odczyt i zapis plików binarnych

Do zapisu oraz odczytu z dysku plików binarnych stosuje się odpowiednio instrukcję **fread()**{:.maroon} oraz **fwrite()**{:.maroon}.
{: .text-justify}

#### Zapis do pliku binarnego
Aby zapisać do pliku binarnego, należy użyć funkcji **fwrite()**{:.maroon}. Funkcje przyjmują cztery argumenty:
{: .text-justify}

```c
fwrite(addressData, sizeData, numbersData, pointerToFile);
```

- addressData - adres danych, które mają zostać zapisane na dysku,
- sizeData - rozmiar pojedynczego elementu danych, które mają być zapisane na dysku,
- numbersData - liczbę elementów, które mają zostać zapisane na dysku,
- pointerToFile - wskaźnik do pliku, w którym chcemy dokonać zapisu.

##### Przykład 3: zapis pliku binarnego

Ten program tworzy nowy plik o nazwie *plik.bin* na dysku w katalogu w którym został uruchomiony program.
{: .text-justify}

```c
#include <stdio.h>
#include <stdlib.h>

struct threeNum
{
   int n1, n2, n3;
};

int main()
{
   int i;
   struct threeNum num;
   FILE *fptr;

   if ((fptr = fopen("plik.bin", "wb")) == NULL){
       printf("Błąd otwarcia pliku!");

       // plik istnieje jeśli zwracana wartość jest różna od NULL
       exit(1);
   }

   for(i = 1; i < 5; i++)
   {
      num.n1 = i;
      num.n2 = 5 * i;
      num.n3 = 5 * i + 1;
      fwrite(&num, sizeof(struct threeNum), 1, fptr); 
   }
   fclose(fptr); 
  
   return 0;
}
```

Deklarujemy strukturę **trzyNum**{:.blue} zawierającą trzy liczby - **n1**{:.blue}, **n2**{:.blue} oraz **n3**{:.blue}, a następnie definiujemy ją w funkcji *main* jako **num**{:.blue}.
{: .text-justify}

Teraz wewnątrz pętli *for* zapisujemy wartość do pliku za pomocą funkcji **fwrite()**{:.maroon}.
{: .text-justify}

Pierwszy parametr przyjmuje adres **num**{:.blue}, a drugi rozmiar struktury **trzyNum**{:.blue}.
{: .text-justify}

Ponieważ wstawiamy tylko jedną instancję **num**{:.blue}, trzeci parametr wynosi 1. Ostatni parametr **fptr**{:.blue} wskazuje na plik, w którym przechowujemy dane.
{: .text-justify}

Na koniec zamykamy plik.
{: .text-justify}

#### Odczyt pliku binarnego

Do odczytu zawartości pliku binarnego należy użyć funkcji **fread()**{:.blue}. Funkcja ta przyjmuje analogiczne parametry jak wcześniej opisywana funkcja **fwrite()**{:.blue}:
{: .text-justify}

- addressData - adres danych, które mają zostać zapisane na dysku,
- sizeData - rozmiar pojedynczego elementu danych, które mają być zapisane na dysku,
- numbersData - liczbę elementów, które mają zostać zapisane na dysku,
- pointerToFile - wskaźnik do pliku, w którym chcemy dokonać zapisu.

##### Przykład 4: odczyt dany z pliku binarnego

Poniższy program wczytuje dane z pliku plik.bin i wyświetla je na ekranie.
{: .text-justify}

```c
#include <stdlib.h>

struct threeNum
{
   int n1, n2, n3;
};

int main()
{
   int i;
   struct threeNum num;
   FILE *fptr;

   if ((fptr = fopen("plik.bin","rb")) == NULL){
       printf("Błąd otwarcia pliku!");

       // plik istnieje jeśli zwracana wartość jest różna od NULL
       exit(1);
   }

   for(i = 1; i < 5; i++)
   {
      fread(&num, sizeof(struct threeNum), 1, fptr); 
      printf("n1: %d\tn2: %d\tn3: %d\n", num.n1, num.n2, num.n3);
   }
   fclose(fptr); 
  
   return 0;
}
```

W uproszczeniu, czytasz jeden rekord o rozmiarze **threeNum**{:.blue} z pliku wskazywanego przez **fptr**{:.blue} do struktury **num**{:.blue}.
{: .text-justify}

Po uruchomieniu tego programu otrzymasz te same rekordy, które zostały wstawione w przykładzie 3.
{: .text-justify}

### Pobieranie danych z wybranego miejsca pliku

Jeśli masz wiele rekordów wewnątrz pliku i potrzebujesz dostępu do rekordu w określonej pozycji, należy pominąć wszystkie rekordy przed nim, aby znaleźć się w tej określonej pozycji.
{: .text-justify}

Do pominięcia określonej porcji danych można użyć funkcji **fseek()**{:.maroon}.
{: .text-justify}

#### Składnia fseek

```c
fseek(FILE *fptr, long int offset, int whence);
```

Pierwszy parametr **fptr**{:.blue} jest wskaźnikiem do pliku. Drugi parametr to pozycja rekordu, który ma zostać odnaleziony, a&nbsp;trzeci parametr określa miejsce, w&nbsp;którym rozpoczyna się offset. Parametr whence może przyjąć jedną z trzech wartości:
{: .text-justify}

- SEEK_SET - rozpoczyna przesunięcie od początku pliku,
- SEEK_END - rozpoczyna przesunięcie od końca pliku,
- SEEK_CUR - rozpoczyna przesunięcie od aktualnego położenia kursora w pliku.

#### Użycie fseek

Ten program zacznie czytać rekordy z&nbsp;pliku plik.bin w&nbsp;odwrotnej kolejności (od ostatniego do pierwszego), a&nbsp;następnie wypisze je na ekranie.
{: .text-justify}

```c
#include <stdio.h>
#include <stdlib.h>

struct threeNum
{
   int n1, n2, n3;
};

int main()
{
   int i;
   struct threeNum num;
   FILE *fptr;

   if ((fptr = fopen("plik.bin","rb")) == NULL){
       printf("Błąd otwarcia pliku!");

       // plik istnieje jeśli zwracana wartość jest różna od NULL
       exit(1);
   }
   
   // przesuń kursor na koniec pliku
   fseek(fptr, -sizeof(struct threeNum), SEEK_END);

   for(i = 1; i < 5; i++)
   {
      fread(&num, sizeof(struct threeNum), 1, fptr); 
      printf("n1: %d\tn2: %d\tn3: %d\n", num.n1, num.n2, num.n3);
      fseek(fptr, -2 * sizeof(struct threeNum), SEEK_CUR);
   }
   fclose(fptr); 
  
   return 0;
}
```

Funkcja **fseek()**{:.maroon} może być używana zarówno podczas odczytu jak i zapisu danych w pliku.
{: .text-justify}