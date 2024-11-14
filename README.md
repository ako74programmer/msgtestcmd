Aby utworzyć komendę dla naszego programu CLLE na platformie IBM i, musimy napisać definicję komendy (CMD) oraz skonfigurować ją tak, by wywoływała nasz program. Dzięki temu użytkownik będzie mógł uruchomić program za pomocą własnej komendy zamiast wpisywać nazwę programu.

### Krok 1: Tworzenie programu CLLE (MSGTESTCL)

Program CLLE, który stworzyliśmy, powinien być zapisany i skompilowany. Przyjmujemy, że nazwa programu to `MSGTESTCL`, a znajduje się on w bibliotece `MYLIB`.

### Krok 2: Tworzenie pliku CMD dla komendy (MSGTEST)

Aby utworzyć komendę, utworzymy obiekt `CMD`, który zdefiniuje parametry i sposób wywołania programu.

### Opis kodu komendy MSGTEST:
1. **CMD** - Początek definicji komendy.
2. **PARM** - Definicja parametru `MSG`, który użytkownik może podać podczas uruchamiania komendy.
   - **KWD(MSG)** - Nazwa parametru, który będzie przekazywany do programu CLLE.
   - **TYPE(*CHAR) LEN(50)** - Parametr typu znakowego o maksymalnej długości 50 znaków.
   - **DFT('Witaj w świecie IBM i!')** - Wartość domyślna parametru. Jeśli użytkownik nie poda wartości, zostanie użyty domyślny komunikat.
   - **PROMPT** - Opis parametru, który wyświetla się użytkownikowi.


### Krok 3: Kompilacja komendy i programu

1. **Skompilowanie programu CLLE** - Upewnij się, że program CLLE jest skompilowany w bibliotece `MYLIB`:
   ```cl
   CRTBNDCL PGM(MYLIB/MSGTESTCL) SRCFILE(MYLIB/QCLSRC) SRCMBR(MSGTESTCL)
   ```

2. **Skompilowanie komendy** - Utwórz plik źródłowy dla komend (`QCMDSRC`) i zapisz w nim definicję komendy `MSGTEST`. Następnie skompiluj komendę:
   ```cl
   CRTCMD CMD(MYLIB/MSGTEST) PGM(MYLIB/MSGTESTCL) SRCFILE(MYLIB/QCMDSRC) SRCMBR(MSGTEST)
   ```

### Krok 4: Uruchomienie komendy

Teraz użytkownik może użyć komendy `MSGTEST`, aby wyświetlić wiadomość. Na przykład:
```cl
MSGTEST MSG('Hello, IBM i!')
```

Lub wywołać komendę bez parametrów, aby użyć domyślnej wartości:
```cl
MSGTEST
```

Ta konfiguracja umożliwia łatwe wywołanie programu za pomocą prostej komendy, co jest wygodne dla użytkowników na platformie IBM i.