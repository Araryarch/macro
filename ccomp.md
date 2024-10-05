Baik, mari kita bahas setiap makro satu per satu dengan contoh input dan outputnya.

### 1. Makro `log`

**Definisi:**

```c
#define log(msg) printf("%s\n", msg)
```

**Contoh Penggunaan:**

```c
log("Hello, World!");
```

**Output:**

```
Hello, World!
```

**Penjelasan:**

- Makro ini mengambil satu argumen (`msg`) dan mencetaknya ke konsol dengan menambahkan baris baru setelahnya. Ini menggunakan fungsi `printf` dari pustaka C.

---

### 2. Makro `logError`

**Definisi:**

```c
#define logError(msg) fprintf(stderr, "%s\n", msg)
```

**Contoh Penggunaan:**

```c
logError("An error occurred!");
```

**Output:**

```
An error occurred!
```

**Penjelasan:**

- Makro ini juga mengambil satu argumen (`msg`) tetapi mencetak pesan tersebut ke saluran kesalahan standar (stderr) menggunakan `fprintf`. Ini sering digunakan untuk menampilkan pesan kesalahan.

---

### 3. Makro `assert`

**Definisi:**

```c
#define assert(condition, msg) if (!(condition)) { logError(msg); exit(1); }
```

**Contoh Penggunaan:**

```c
int x = 5;
assert(x > 10, "x must be greater than 10");
```

**Output:**

```
An error occurred!
```

**Penjelasan:**

- Makro ini memeriksa sebuah kondisi. Jika kondisi tersebut tidak benar (`false`), maka makro ini akan memanggil `logError` untuk mencetak pesan kesalahan yang diberikan (`msg`) dan menghentikan program dengan `exit(1)`. Jika kondisi benar, tidak ada yang terjadi.

---

### Contoh Gabungan

Berikut adalah contoh gabungan dari ketiga makro tersebut dalam sebuah program:

```c
#include <stdio.h>
#include <stdlib.h>

// Logging
#define log(msg) printf("%s\n", msg)
#define logError(msg) fprintf(stderr, "%s\n", msg)
#define assert(condition, msg) if (!(condition)) { logError(msg); exit(1); }

int main() {
    log("Program started");

    int x = 5;
    log("Checking value of x");

    // Assert that x is greater than 10
    assert(x > 10, "x must be greater than 10");

    log("Program finished");
    return 0;
}
```

**Output ketika dijalankan:**

```
Program started
Checking value of x
x must be greater than 10
```

- **Penjelasan Gabungan:**
  1. Program mencetak "Program started".
  2. Program mencetak "Checking value of x".
  3. Ketika `assert` dipanggil, karena `x` tidak lebih besar dari 10, makro `logError` akan dipanggil dan mencetak "x must be greater than 10", lalu program dihentikan.

### 1. Makro `forEach`

**Definisi:**

```c
#define forEach(arr, len, func) for (int i = 0; i < len; i++) { func(arr[i]); }
```

**Contoh Penggunaan:**

```c
void print(int num) {
    printf("%d ", num);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    forEach(arr, 5, print);
    return 0;
}
```

**Output:**

```
1 2 3 4 5
```

**Penjelasan:**

- Makro ini mengiterasi elemen dalam array `arr` sebanyak `len` kali, dan menerapkan fungsi `func` pada setiap elemen.

---

### 2. Makro `map`

**Definisi:**

```c
#define map(arr, len, func, result) for (int i = 0; i < len; i++) { result[i] = func(arr[i]); }
```

**Contoh Penggunaan:**

```c
int square(int num) {
    return num * num;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int result[5];
    map(arr, 5, square, result);

    for (int i = 0; i < 5; i++) {
        printf("%d ", result[i]);
    }
    return 0;
}
```

**Output:**

```
1 4 9 16 25
```

**Penjelasan:**

- Makro ini menerapkan fungsi `func` pada setiap elemen dalam array `arr` dan menyimpan hasilnya dalam array `result`.

---

### 3. Makro `filter`

**Definisi:**

```c
#define filter(arr, len, func, result, result_len) { int j = 0; for (int i = 0; i < len; i++) { if (func(arr[i])) result[j++] = arr[i]; } *result_len = j; }
```

**Contoh Penggunaan:**

```c
bool isEven(int num) {
    return num % 2 == 0;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int result[5];
    int result_len;

    filter(arr, 5, isEven, result, &result_len);

    for (int i = 0; i < result_len; i++) {
        printf("%d ", result[i]);
    }
    return 0;
}
```

**Output:**

```
2 4
```

**Penjelasan:**

- Makro ini memfilter elemen dalam `arr` berdasarkan fungsi `func`, dan menyimpan elemen yang memenuhi syarat ke dalam `result`.

---

### 4. Makro `reduce`

**Definisi:**

```c
#define reduce(arr, len, func, initial) ({ int acc = initial; for (int i = 0; i < len; i++) { acc = func(acc, arr[i]); } acc; })
```

**Contoh Penggunaan:**

```c
int sum(int acc, int num) {
    return acc + num;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int result = reduce(arr, 5, sum, 0);
    printf("%d\n", result);
    return 0;
}
```

**Output:**

```
15
```

**Penjelasan:**

- Makro ini mengakumulasi nilai dalam `arr` dengan menggunakan fungsi `func`, dimulai dari nilai `initial`.

---

### 5. Makro `includes`

**Definisi:**

```c
#define includes(arr, len, value) ({ bool found = false; for (int i = 0; i < len; i++) if (arr[i] == value) { found = true; break; } found; })
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    bool found = includes(arr, 5, 3);
    printf("%s\n", found ? "Found" : "Not Found");
    return 0;
}
```

**Output:**

```
Found
```

**Penjelasan:**

- Makro ini memeriksa apakah `value` ada di dalam `arr`. Jika ada, mengembalikan `true`, jika tidak `false`.

---

### 6. Makro `reverse`

**Definisi:**

```c
#define reverse(arr, len) for (int i = 0; i < len / 2; i++) { int temp = arr[i]; arr[i] = arr[len - 1 - i]; arr[len - 1 - i] = temp; }
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    reverse(arr, 5);

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
5 4 3 2 1
```

**Penjelasan:**

- Makro ini membalik urutan elemen dalam `arr`.

---

### 7. Makro `sortAsc`

**Definisi:**

```c
#define sortAsc(arr, len) qsort(arr, len, sizeof(arr[0]), cmpAsc)
```

**Contoh Penggunaan:**

```c
int cmpAsc(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int main() {
    int arr[] = {5, 3, 1, 4, 2};
    sortAsc(arr, 5);

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
1 2 3 4 5
```

**Penjelasan:**

- Makro ini mengurutkan elemen dalam `arr` secara ascending menggunakan `qsort`.

---

### 8. Makro `sortDesc`

**Definisi:**

```c
#define sortDesc(arr, len) qsort(arr, len, sizeof(arr[0]), cmpDesc)
```

**Contoh Penggunaan:**

```c
int cmpDesc(const void *a, const void *b) {
    return (*(int*)b - *(int*)a);
}

int main() {
    int arr[] = {5, 3, 1, 4, 2};
    sortDesc(arr, 5);

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
5 4 3 2 1
```

**Penjelasan:**

- Makro ini mengurutkan elemen dalam `arr` secara descending menggunakan `qsort`.

---

### 9. Makro `unique`

**Definisi:**

```c
#define unique(arr, len, result, result_len) { int j = 0; for (int i = 0; i < len; i++) { if (!includes(result, j, arr[i])) result[j++] = arr[i]; } *result_len = j; }
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[] = {1, 2, 2, 3, 4, 4, 5};
    int result[7];
    int result_len;

    unique(arr, 7, result, &result_len);

    for (int i = 0; i < result_len; i++) {
        printf("%d ", result[i]);
    }
    return 0;
}
```

**Output:**

```
1 2 3 4 5
```

**Penjelasan:**

- Makro ini menghilangkan elemen duplikat dari `arr` dan menyimpan hasilnya dalam `result`.

---

### 10. Makro `push`

**Definisi:**

```c
#define push(arr, len, value) arr[len++] = value
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[6] = {1, 2, 3, 4, 5};
    int len = 5;

    push(arr, len, 6);

    for (int i = 0; i < len + 1; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
1 2 3 4 5 6
```

**Penjelasan:**

- Makro ini menambahkan `value` ke akhir `arr` dan meningkatkan panjang array `len`.

---

### 11. Makro `pop`

**Definisi:**

```c
#define pop(arr, len) (len > 0 ? --len : 0)
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[] = {1, 2, 3, 4,

5};
    int len = 5;

    len = pop(arr, len);

    printf("New length: %d\n", len);
    return 0;
}
```

**Output:**

```
New length: 4
```

**Penjelasan:**

- Makro ini menghapus elemen terakhir dari `arr` dengan mengurangi panjang `len`.

---

### 12. Makro `shift`

**Definisi:**

```c
#define shift(arr, len) { for (int i = 1; i < len; i++) arr[i - 1] = arr[i]; len--; }
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int len = 5;

    shift(arr, len);

    for (int i = 0; i < len - 1; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
2 3 4 5
```

**Penjelasan:**

- Makro ini menggeser semua elemen ke kiri dan mengurangi panjang `len`.

---

### 13. Makro `unshift`

**Definisi:**

```c
#define unshift(arr, len, value) { for (int i = len; i > 0; i--) arr[i] = arr[i - 1]; arr[0] = value; len++; }
```

**Contoh Penggunaan:**

```c
int main() {
    int arr[6] = {2, 3, 4, 5};
    int len = 4;

    unshift(arr, len, 1);

    for (int i = 0; i < len + 1; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
1 2 3 4 5
```

**Penjelasan:**

- Makro ini menambahkan `value` ke awal `arr` dan meningkatkan panjang `len`.

---

Berikut adalah penjelasan mendetail untuk setiap makro string yang Anda berikan, termasuk contoh penggunaannya:

### 1. Makro `startsWith`

**Definisi:**

```c
#define startsWith(str, prefix) (strncmp(str, prefix, strlen(prefix)) == 0)
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    const char *str = "Hello, world!";
    if (startsWith(str, "Hello")) {
        printf("String starts with 'Hello'\n");
    }
    return 0;
}
```

**Output:**

```
String starts with 'Hello'
```

**Penjelasan:**

- Makro ini memeriksa apakah `str` dimulai dengan `prefix` menggunakan `strncmp`.

---

### 2. Makro `endsWith`

**Definisi:**

```c
#define endsWith(str, suffix) ({ int l1 = strlen(str); int l2 = strlen(suffix); (l1 >= l2 && strcmp(str + l1 - l2, suffix) == 0); })
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    const char *str = "Hello, world!";
    if (endsWith(str, "world!")) {
        printf("String ends with 'world!'\n");
    }
    return 0;
}
```

**Output:**

```
String ends with 'world!'
```

**Penjelasan:**

- Makro ini memeriksa apakah `str` diakhiri dengan `suffix` menggunakan `strcmp`.

---

### 3. Makro `toUpperCase`

**Definisi:**

```c
#define toUpperCase(str) for (int i = 0; str[i]; i++) str[i] = toupper(str[i])
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char str[] = "hello";
    toUpperCase(str);
    printf("%s\n", str);
    return 0;
}
```

**Output:**

```
HELLO
```

**Penjelasan:**

- Makro ini mengubah semua karakter dalam `str` menjadi huruf besar menggunakan `toupper`.

---

### 4. Makro `toLowerCase`

**Definisi:**

```c
#define toLowerCase(str) for (int i = 0; str[i]; i++) str[i] = tolower(str[i])
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char str[] = "HELLO";
    toLowerCase(str);
    printf("%s\n", str);
    return 0;
}
```

**Output:**

```
hello
```

**Penjelasan:**

- Makro ini mengubah semua karakter dalam `str` menjadi huruf kecil menggunakan `tolower`.

---

### 5. Makro `split`

**Definisi:**

```c
#define split(str, delimiter, result, result_len) { char *token = strtok(str, delimiter); int i = 0; while (token != NULL) { result[i++] = token; token = strtok(NULL, delimiter); } *result_len = i; }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "one,two,three";
    char *result[3];
    int result_len;

    split(str, ",", result, &result_len);

    for (int i = 0; i < result_len; i++) {
        printf("%s\n", result[i]);
    }
    return 0;
}
```

**Output:**

```
one
two
three
```

**Penjelasan:**

- Makro ini membagi `str` berdasarkan `delimiter` dan menyimpan hasilnya di `result`.

---

### 6. Makro `join`

**Definisi:**

```c
#define join(arr, len, delimiter, result) { strcpy(result, arr[0]); for (int i = 1; i < len; i++) { strcat(result, delimiter); strcat(result, arr[i]); } }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    const char *arr[] = {"one", "two", "three"};
    char result[50];

    join(arr, 3, ", ", result);
    printf("%s\n", result);
    return 0;
}
```

**Output:**

```
one, two, three
```

**Penjelasan:**

- Makro ini menggabungkan elemen dalam `arr` dengan `delimiter` dan menyimpan hasilnya di `result`.

---

### 7. Makro `repeat`

**Definisi:**

```c
#define repeat(str, n, result) { result[0] = '\\0'; for (int i = 0; i < n; i++) strcat(result, str); }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    char result[50];
    repeat("hello", 3, result);
    printf("%s\n", result);
    return 0;
}
```

**Output:**

```
hellohellohello
```

**Penjelasan:**

- Makro ini mengulangi `str` sebanyak `n` kali dan menyimpan hasilnya di `result`.

---

### 8. Makro `trim`

**Definisi:**

```c
#define trim(str) { char *end; while (isspace((unsigned char)*str)) str++; if (*str == 0) return; end = str + strlen(str) - 1; while (end > str && isspace((unsigned char)*end)) end--; end[1] = '\\0'; }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char str[] = "   hello world!   ";
    trim(str);
    printf("'%s'\n", str);
    return 0;
}
```

**Output:**

```
'hello world!'
```

**Penjelasan:**

- Makro ini menghapus spasi di awal dan akhir `str`.

---

### 9. Makro `replace`

**Definisi:**

```c
#define replace(str, from, to, result) { char *pos = strstr(str, from); if (pos != NULL) { strncpy(result, str, pos - str); result[pos - str] = '\\0'; strcat(result, to); strcat(result, pos + strlen(from)); } else strcpy(result, str); }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    char result[50];
    replace("Hello, world!", "world", "C", result);
    printf("%s\n", result);
    return 0;
}
```

**Output:**

```
Hello, C!
```

**Penjelasan:**

- Makro ini mengganti kemunculan `from` dengan `to` dalam `str` dan menyimpan hasilnya di `result`.

---

### 10. Makro `substring`

**Definisi:**

```c
#define substring(str, start, len) (strndup(str + start, len))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    const char *str = "Hello, world!";
    char *sub = substring(str, 7, 5);
    printf("%s\n", sub);
    free(sub); // Jangan lupa untuk membebaskan memori
    return 0;
}
```

**Output:**

```
world
```

**Penjelasan:**

- Makro ini mengambil substring dari `str` mulai dari `start` dengan panjang `len`.

---

### 11. Makro `length`

**Definisi:**

```c
#define length(str) (strlen(str))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <string.h>

int main() {
    const char *str = "Hello, world!";
    printf("Length: %lu\n", length(str));
    return 0;
}
```

**Output:**

```
Length: 13
```

**Penjelasan:**

- Makro ini mengembalikan panjang dari `str` menggunakan `strlen`.

---

Berikut adalah penjelasan mendetail untuk setiap makro matematis yang Anda berikan, termasuk contoh penggunaannya:

### 1. Makro `max`

**Definisi:**

```c
#define max(a, b) ((a) > (b) ? (a) : (b))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int x = 5, y = 10;
    printf("Max: %d\n", max(x, y));
    return 0;
}
```

**Output:**

```
Max: 10
```

**Penjelasan:**

- Makro ini mengembalikan nilai maksimum antara `a` dan `b`.

---

### 2. Makro `min`

**Definisi:**

```c
#define min(a, b) ((a) < (b) ? (a) : (b))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int x = 5, y = 10;
    printf("Min: %d\n", min(x, y));
    return 0;
}
```

**Output:**

```
Min: 5
```

**Penjelasan:**

- Makro ini mengembalikan nilai minimum antara `a` dan `b`.

---

### 3. Makro `pow`

**Definisi:**

```c
#define pow(base, exp) (pow(base, exp))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double result = pow(2, 3); // 2^3
    printf("Power: %.2f\n", result);
    return 0;
}
```

**Output:**

```
Power: 8.00
```

**Penjelasan:**

- Makro ini menghitung pangkat `base` dipangkatkan `exp` menggunakan fungsi `pow`.

---

### 4. Makro `sqrt`

**Definisi:**

```c
#define sqrt(n) (sqrt(n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double result = sqrt(16); // √16
    printf("Square Root: %.2f\n", result);
    return 0;
}
```

**Output:**

```
Square Root: 4.00
```

**Penjelasan:**

- Makro ini menghitung akar kuadrat dari `n` menggunakan fungsi `sqrt`.

---

### 5. Makro `abs`

**Definisi:**

```c
#define abs(n) (abs(n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int value = -5;
    printf("Absolute: %d\n", abs(value));
    return 0;
}
```

**Output:**

```
Absolute: 5
```

**Penjelasan:**

- Makro ini mengembalikan nilai absolut dari `n` menggunakan fungsi `abs`.

---

### 6. Makro `ceil`

**Definisi:**

```c
#define ceil(n) (ceil(n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double value = 2.3;
    printf("Ceiling: %.2f\n", ceil(value));
    return 0;
}
```

**Output:**

```
Ceiling: 3.00
```

**Penjelasan:**

- Makro ini membulatkan `n` ke atas menggunakan fungsi `ceil`.

---

### 7. Makro `floor`

**Definisi:**

```c
#define floor(n) (floor(n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double value = 2.7;
    printf("Floor: %.2f\n", floor(value));
    return 0;
}
```

**Output:**

```
Floor: 2.00
```

**Penjelasan:**

- Makro ini membulatkan `n` ke bawah menggunakan fungsi `floor`.

---

### 8. Makro `round`

**Definisi:**

```c
#define round(n) (round(n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double value = 2.5;
    printf("Round: %.0f\n", round(value));
    return 0;
}
```

**Output:**

```
Round: 3
```

**Penjelasan:**

- Makro ini membulatkan `n` ke angka terdekat menggunakan fungsi `round`.

---

### 9. Makro `random`

**Definisi:**

```c
#define random(min, max) ((min) + rand() % ((max) - (min) + 1))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand(time(NULL)); // Inisialisasi seed untuk random
    int randNum = random(1, 10);
    printf("Random Number: %d\n", randNum);
    return 0;
}
```

**Output:**

```
Random Number: 5
```

**Penjelasan:**

- Makro ini menghasilkan bilangan acak antara `min` dan `max` menggunakan `rand()`.

---

### 10. Makro `clamp`

**Definisi:**

```c
#define clamp(n, minVal, maxVal) (max(minVal, min(n, maxVal)))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int value = 15;
    int clampedValue = clamp(value, 10, 12);
    printf("Clamped Value: %d\n", clampedValue);
    return 0;
}
```

**Output:**

```
Clamped Value: 12
```

**Penjelasan:**

- Makro ini membatasi nilai `n` agar berada di antara `minVal` dan `maxVal`.

---

### 11. Makro `gcd`

**Definisi:**

```c
#define gcd(a, b) ({ int _a = a, _b = b; while (_b != 0) { int t = _b; _b = _a % _b; _a = t; } _a; })
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 60, b = 48;
    printf("GCD: %d\n", gcd(a, b));
    return 0;
}
```

**Output:**

```
GCD: 12
```

**Penjelasan:**

- Makro ini menghitung GCD (Greatest Common Divisor) dari `a` dan `b` menggunakan algoritma Euclidean.

---

### 12. Makro `lcm`

**Definisi:**

```c
#define lcm(a, b) ((a * b) / gcd(a, b))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 4, b = 6;
    printf("LCM: %d\n", lcm(a, b));
    return 0;
}
```

**Output:**

```
LCM: 12
```

**Penjelasan:**

- Makro ini menghitung LCM (Least Common Multiple) dari `a` dan `b` dengan menggunakan GCD.

---

Berikut adalah penjelasan mendetail untuk setiap makro bitwise yang Anda berikan, termasuk contoh penggunaannya:

### 1. Makro `andBits`

**Definisi:**

```c
#define andBits(x, y) ((x) & (y))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    int b = 3; // 0011 dalam biner
    printf("AND: %d\n", andBits(a, b));
    return 0;
}
```

**Output:**

```
AND: 1
```

**Penjelasan:**

- Makro ini mengembalikan hasil operasi AND bitwise antara `x` dan `y`. Dalam contoh, `0101 & 0011` menghasilkan `0001`, yang merupakan `1` dalam desimal.

---

### 2. Makro `orBits`

**Definisi:**

```c
#define orBits(x, y) ((x) | (y))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    int b = 3; // 0011 dalam biner
    printf("OR: %d\n", orBits(a, b));
    return 0;
}
```

**Output:**

```
OR: 7
```

**Penjelasan:**

- Makro ini mengembalikan hasil operasi OR bitwise antara `x` dan `y`. Dalam contoh, `0101 | 0011` menghasilkan `0111`, yang merupakan `7` dalam desimal.

---

### 3. Makro `xorBits`

**Definisi:**

```c
#define xorBits(x, y) ((x) ^ (y))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    int b = 3; // 0011 dalam biner
    printf("XOR: %d\n", xorBits(a, b));
    return 0;
}
```

**Output:**

```
XOR: 6
```

**Penjelasan:**

- Makro ini mengembalikan hasil operasi XOR bitwise antara `x` dan `y`. Dalam contoh, `0101 ^ 0011` menghasilkan `0110`, yang merupakan `6` dalam desimal.

---

### 4. Makro `notBits`

**Definisi:**

```c
#define notBits(x) (~(x))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    printf("NOT: %d\n", notBits(a));
    return 0;
}
```

**Output:**

```
NOT: -6
```

**Penjelasan:**

- Makro ini mengembalikan hasil operasi NOT bitwise pada `x`. Dalam contoh, `~0101` menghasilkan `-6`, karena NOT membalikkan semua bit, termasuk bit tanda.

---

### 5. Makro `shiftLeft`

**Definisi:**

```c
#define shiftLeft(x, n) ((x) << (n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    printf("Shift Left: %d\n", shiftLeft(a, 1));
    return 0;
}
```

**Output:**

```
Shift Left: 10
```

**Penjelasan:**

- Makro ini menggeser bit `x` ke kiri sebanyak `n` posisi. Dalam contoh, `0101 << 1` menghasilkan `1010`, yang merupakan `10` dalam desimal.

---

### 6. Makro `shiftRight`

**Definisi:**

```c
#define shiftRight(x, n) ((x) >> (n))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int a = 5; // 0101 dalam biner
    printf("Shift Right: %d\n", shiftRight(a, 1));
    return 0;
}
```

**Output:**

```
Shift Right: 2
```

**Penjelasan:**

- Makro ini menggeser bit `x` ke kanan sebanyak `n` posisi. Dalam contoh, `0101 >> 1` menghasilkan `0010`, yang merupakan `2` dalam desimal.

---

Berikut adalah penjelasan mendetail untuk setiap makro terkait pencarian dan permutasi dalam kode Anda, lengkap dengan contoh penggunaan:

### 1. Makro `binarySearch`

**Definisi:**

```c
#define binarySearch(arr, len, value) (bsearch(&value, arr, len, sizeof(arr[0]), cmp))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <stdlib.h>

// Fungsi komparator untuk bsearch
int cmp(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int len = sizeof(arr) / sizeof(arr[0]);
    int value = 3;

    int *result = binarySearch(arr, len, value);
    if (result) {
        printf("Found: %d\n", *result);
    } else {
        printf("Not found\n");
    }

    return 0;
}
```

**Output:**

```
Found: 3
```

**Penjelasan:**

- Makro ini menggunakan fungsi `bsearch` untuk mencari `value` dalam array `arr`. Fungsi `cmp` digunakan untuk membandingkan elemen. Jika ditemukan, ia mengembalikan pointer ke elemen tersebut; jika tidak, mengembalikan `NULL`.

---

### 2. Makro `lowerBound`

**Definisi:**

```c
#define lowerBound(arr, len, value) ({ int l = 0, r = len, m; while (l < r) { m = (l + r) / 2; if (arr[m] < value) l = m + 1; else r = m; } l; })
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 4, 4, 5};
    int len = sizeof(arr) / sizeof(arr[0]);
    int value = 4;

    int index = lowerBound(arr, len, value);
    printf("Lower Bound Index: %d\n", index);

    return 0;
}
```

**Output:**

```
Lower Bound Index: 2
```

**Penjelasan:**

- Makro ini mengimplementasikan algoritma binary search untuk menemukan indeks terkecil di mana `value` dapat ditempatkan tanpa mengubah urutan array. Dalam contoh, indeks terkecil untuk `4` adalah `2`.

---

### 3. Makro `upperBound`

**Definisi:**

```c
#define upperBound(arr, len, value) ({ int l = 0, r = len, m; while (l < r) { m = (l + r) / 2; if (arr[m] <= value) l = m + 1; else r = m; } l; })
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 4, 4, 5};
    int len = sizeof(arr) / sizeof(arr[0]);
    int value = 4;

    int index = upperBound(arr, len, value);
    printf("Upper Bound Index: %d\n", index);

    return 0;
}
```

**Output:**

```
Upper Bound Index: 4
```

**Penjelasan:**

- Makro ini menggunakan algoritma binary search untuk menemukan indeks terkecil di mana `value` tidak dapat ditempatkan tanpa mengubah urutan array. Dalam contoh, indeks untuk `4` adalah `4`, karena elemen `5` berada di indeks itu.

---

### 4. Makro `nextPermutation`

**Definisi:**

```c
#define nextPermutation(arr, len) (next_permutation(arr, arr + len))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <algorithm>

int main() {
    int arr[] = {1, 2, 3};
    int len = sizeof(arr) / sizeof(arr[0]);

    std::next_permutation(arr, arr + len);

    printf("Next Permutation: ");
    for (int i = 0; i < len; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```

**Output:**

```
Next Permutation: 1 3 2
```

**Penjelasan:**

- Makro ini memanggil fungsi `next_permutation` untuk menghasilkan permutasi berikutnya dari array. Dalam contoh, permutasi berikutnya dari `{1, 2, 3}` adalah `{1, 3, 2}`.

---

### 5. Makro `prevPermutation`

**Definisi:**

```c
#define prevPermutation(arr, len) (prev_permutation(arr, arr + len))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <algorithm>

int main() {
    int arr[] = {1, 3, 2};
    int len = sizeof(arr) / sizeof(arr[0]);

    std::prev_permutation(arr, arr + len);

    printf("Previous Permutation: ");
    for (int i = 0; i < len; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```

**Output:**

```
Previous Permutation: 1 2 3
```

**Penjelasan:**

- Makro ini memanggil fungsi `prev_permutation` untuk menghasilkan permutasi sebelumnya dari array. Dalam contoh, permutasi sebelumnya dari `{1, 3, 2}` adalah `{1, 2, 3}`.

---

Berikut adalah penjelasan untuk makro yang berkaitan dengan waktu, operasi dasar, dan fungsi perbandingan dalam kode Anda, lengkap dengan contoh penggunaan:

### 1. Makro `now`

**Definisi:**

```c
#define now() (clock())
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <time.h>

int main() {
    clock_t start = now();
    // Simulasi pekerjaan
    for (volatile int i = 0; i < 1e7; i++);
    clock_t end = now();

    printf("Elapsed time: %lf seconds\n", duration(start, end));
    return 0;
}
```

**Output:**

```
Elapsed time: x.xx seconds
```

(Angka `x.xx` akan tergantung pada waktu eksekusi.)

**Penjelasan:**

- Makro ini mengembalikan waktu saat ini dalam hitungan detik dari program yang berjalan, menggunakan fungsi `clock()` dari `<time.h>`. Ini berguna untuk mengukur durasi eksekusi suatu bagian dari kode.

---

### 2. Makro `sleep`

**Definisi:**

```c
#define sleep(ms) (usleep((ms) * 1000))
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    printf("Sleeping for 2 seconds...\n");
    sleep(2000); // Tidur selama 2000 ms atau 2 detik
    printf("Awake!\n");
    return 0;
}
```

**Output:**

```
Sleeping for 2 seconds...
Awake!
```

**Penjelasan:**

- Makro ini mengubah waktu dalam milidetik menjadi mikrodetik (1 ms = 1000 µs) dan menggunakan `usleep()` untuk menghentikan eksekusi program selama waktu yang ditentukan.

---

### 3. Makro `duration`

**Definisi:**

```c
#define duration(start, end) (((double)(end - start)) / CLOCKS_PER_SEC)
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <time.h>

int main() {
    clock_t start = now();
    // Simulasi pekerjaan
    for (volatile int i = 0; i < 1e7; i++);
    clock_t end = now();

    printf("Elapsed time: %lf seconds\n", duration(start, end));
    return 0;
}
```

**Output:**

```
Elapsed time: x.xx seconds
```

(Angka `x.xx` akan tergantung pada waktu eksekusi.)

**Penjelasan:**

- Makro ini menghitung durasi antara dua waktu `start` dan `end`, mengubah hasil ke detik dengan membagi dengan `CLOCKS_PER_SEC`.

---

### 4. Makro `isEven`

**Definisi:**

```c
#define isEven(n) ((n) % 2 == 0)
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int number = 4;

    if (isEven(number)) {
        printf("%d is even.\n", number);
    } else {
        printf("%d is odd.\n", number);
    }

    return 0;
}
```

**Output:**

```
4 is even.
```

**Penjelasan:**

- Makro ini memeriksa apakah `n` genap dengan menggunakan operator modulus. Jika sisa pembagian `n` dengan `2` adalah `0`, maka `n` adalah genap.

---

### 5. Makro `isOdd`

**Definisi:**

```c
#define isOdd(n) ((n) % 2 != 0)
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int number = 5;

    if (isOdd(number)) {
        printf("%d is odd.\n", number);
    } else {
        printf("%d is even.\n", number);
    }

    return 0;
}
```

**Output:**

```
5 is odd.
```

**Penjelasan:**

- Makro ini memeriksa apakah `n` ganjil dengan menggunakan operator modulus. Jika sisa pembagian `n` dengan `2` bukan `0`, maka `n` adalah ganjil.

---

### 6. Makro `swap`

**Definisi:**

```c
#define swap(a, b) { int temp = a; a = b; b = temp; }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

int main() {
    int x = 10, y = 20;

    printf("Before swap: x = %d, y = %d\n", x, y);
    swap(x, y);
    printf("After swap: x = %d, y = %d\n", x, y);

    return 0;
}
```

**Output:**

```
Before swap: x = 10, y = 20
After swap: x = 20, y = 10
```

**Penjelasan:**

- Makro ini bertukar nilai dua variabel `a` dan `b` dengan menggunakan variabel sementara `temp`.

---

### 7. Makro `repeat`

**Definisi:**

```c
#define repeat(n, func) for (int i = 0; i < n; i++) func()
```

**Contoh Penggunaan:**

```c
#include <stdio.h>

void sayHello() {
    printf("Hello!\n");
}

int main() {
    repeat(3, sayHello); // Panggil sayHello 3 kali
    return 0;
}
```

**Output:**

```
Hello!
Hello!
Hello!
```

**Penjelasan:**

- Makro ini menjalankan fungsi `func` sebanyak `n` kali, menggunakan loop `for`.

---

### 8. Fungsi `cmpAsc`, `cmpDesc`, dan `cmp`

**Definisi:**

```c
int cmpAsc(const void *a, const void *b) { return (*(int*)a - *(int*)b); }
int cmpDesc(const void *a, const void *b) { return (*(int*)b - *(int*)a); }
int cmp(const void *a, const void *b) { return (*(int*)a - *(int*)b); }
```

**Contoh Penggunaan:**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int arr[] = {3, 1, 4, 1, 5};
    int len = sizeof(arr) / sizeof(arr[0]);

    qsort(arr, len, sizeof(int), cmpAsc);
    printf("Sorted Ascending: ");
    for (int i = 0; i < len; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    qsort(arr, len, sizeof(int), cmpDesc);
    printf("Sorted Descending: ");
    for (int i = 0; i < len; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```

**Output:**

```
Sorted Ascending: 1 1 3 4 5
Sorted Descending: 5 4 3 1 1
```

**Penjelasan:**

- Fungsi ini digunakan untuk membandingkan dua elemen, berguna dalam fungsi `qsort`. `cmpAsc` mengurutkan secara ascending, sedangkan `cmpDesc` mengurutkan secara descending.

---
