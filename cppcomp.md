Berikut adalah penjelasan untuk masing-masing makro yang Anda berikan, beserta contoh input dan outputnya.

### 1. `#include <bits/stdc++.h>`

**Penjelasan**: Ini adalah header yang mengikutsertakan hampir semua library standard C++ dalam satu file. Ini sering digunakan dalam kompetisi pemrograman untuk menghemat waktu dalam menyertakan library.

**Contoh Input**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

**Contoh Output**:

```
Hello, World!
```

---

### 2. `using namespace std;`

**Penjelasan**: Mengizinkan penggunaan elemen dari namespace `std` tanpa perlu menyertakan prefix `std::` setiap kali.

**Contoh Input**:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl; // Menggunakan cout tanpa std::
    return 0;
}
```

**Contoh Output**:

```
Hello, World!
```

---

### 3. `#define int long long`

**Penjelasan**: Makro ini mengganti semua penggunaan `int` dengan `long long`, sehingga semua variabel bertipe `int` akan bertipe `long long`, yang memiliki rentang lebih besar.

**Contoh Input**:

```cpp
#include <iostream>
#define int long long
using namespace std;

int main() {
    int a = 10000000000; // a sekarang bertipe long long
    cout << a << endl;
    return 0;
}
```

**Contoh Output**:

```
10000000000
```

---

### 4. `#define log(msg)`

**Penjelasan**: Makro ini membuat fungsi logging sederhana yang mencetak pesan ke konsol dengan newline.

**Contoh Input**:

```cpp
#include <iostream>
#define log(msg) (std::cout << msg << std::endl)
using namespace std;

int main() {
    log("Hello, World!"); // Memanggil makro log
    return 0;
}
```

**Contoh Output**:

```
Hello, World!
```

---

### 5. `#define logError(msg)`

**Penjelasan**: Mirip dengan `log`, tetapi mengarahkan output ke `std::cerr`, yang sering digunakan untuk mencetak error.

**Contoh Input**:

```cpp
#include <iostream>
#define logError(msg) (std::cerr << msg << std::endl)
using namespace std;

int main() {
    logError("An error occurred!"); // Menggunakan makro logError
    return 0;
}
```

**Contoh Output**:

```
An error occurred!
```

---

### 6. `#define throwError(msg)`

**Penjelasan**: Makro ini digunakan untuk melempar exception dengan pesan tertentu menggunakan `std::runtime_error`.

**Contoh Input**:

```cpp
#include <iostream>
#include <stdexcept>
#define throwError(msg) (throw std::runtime_error(msg))
using namespace std;

int main() {
    try {
        throwError("This is an error!"); // Menggunakan makro throwError
    } catch (const std::runtime_error& e) {
        cout << e.what() << endl; // Menangkap dan mencetak error
    }
    return 0;
}
```

**Contoh Output**:

```
This is an error!
```

---

### 7. `#define assert(condition, msg)`

**Penjelasan**: Makro ini memeriksa kondisi dan jika tidak terpenuhi, akan melempar error menggunakan `throwError`.

**Contoh Input**:

```cpp
#include <iostream>
#include <stdexcept>
#define throwError(msg) (throw std::runtime_error(msg))
#define assert(condition, msg) if (!(condition)) throwError(msg)
using namespace std;

int main() {
    try {
        int x = 5;
        assert(x > 10, "Assertion failed: x must be greater than 10!"); // Menggunakan makro assert
    } catch (const std::runtime_error& e) {
        cout << e.what() << endl; // Menangkap dan mencetak error
    }
    return 0;
}
```

**Contoh Output**:

```
Assertion failed: x must be greater than 10!
```

---

### 1. `#define forEach(arr, func)`

**Penjelasan**: Makro ini menjalankan fungsi `func` untuk setiap elemen dalam array `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define forEach(arr, func) for (auto& item : arr) { func(item); }
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    forEach(numbers, [](int x) { cout << x << " "; }); // Menggunakan makro forEach
    return 0;
}
```

**Contoh Output**:

```
1 2 3 4 5
```

---

### 2. `#define map(arr, func)`

**Penjelasan**: Makro ini mengaplikasikan fungsi `func` pada setiap elemen dalam `arr` dan mengembalikan vector hasilnya.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define map(arr, func) ({ std::vector<decltype(func(arr[0]))> _result; for (auto& item : arr) { _result.push_back(func(item)); } _result; })
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    auto squared = map(numbers, [](int x) { return x * x; }); // Menggunakan makro map
    for (int x : squared) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 4 9 16 25
```

---

### 3. `#define filter(arr, func)`

**Penjelasan**: Makro ini mengembalikan elemen dari `arr` yang memenuhi kondisi dalam `func`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define filter(arr, func) ({ std::vector<decltype(arr[0])> _result; for (auto& item : arr) { if (func(item)) _result.push_back(item); } _result; })
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    auto evens = filter(numbers, [](int x) { return x % 2 == 0; }); // Menggunakan makro filter
    for (int x : evens) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
2 4
```

---

### 4. `#define reduce(arr, func, initial)`

**Penjelasan**: Makro ini mengakumulasi nilai dari `arr` menggunakan fungsi `func` dan nilai awal `initial`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define reduce(arr, func, initial) ({ auto _acc = initial; for (auto& item : arr) { _acc = func(_acc, item); } _acc; })
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    auto sum = reduce(numbers, [](int acc, int x) { return acc + x; }, 0); // Menggunakan makro reduce
    cout << sum << endl;
    return 0;
}
```

**Contoh Output**:

```
15
```

---

### 5. `#define some(arr, func)`

**Penjelasan**: Makro ini mengembalikan true jika ada setidaknya satu elemen dalam `arr` yang memenuhi `func`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define some(arr, func) (std::any_of(arr.begin(), arr.end(), func))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    bool hasEven = some(numbers, [](int x) { return x % 2 == 0; }); // Menggunakan makro some
    cout << (hasEven ? "Has even number" : "No even number") << endl;
    return 0;
}
```

**Contoh Output**:

```
Has even number
```

---

### 6. `#define every(arr, func)`

**Penjelasan**: Makro ini mengembalikan true jika semua elemen dalam `arr` memenuhi `func`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define every(arr, func) (std::all_of(arr.begin(), arr.end(), func))
using namespace std;

int main() {
    vector<int> numbers = {2, 4, 6, 8, 10};
    bool allEven = every(numbers, [](int x) { return x % 2 == 0; }); // Menggunakan makro every
    cout << (allEven ? "All are even" : "Not all are even") << endl;
    return 0;
}
```

**Contoh Output**:

```
All are even
```

---

### 7. `#define includes(arr, value)`

**Penjelasan**: Makro ini memeriksa apakah `value` ada dalam `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define includes(arr, value) (std::find(arr.begin(), arr.end(), value) != arr.end())
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    bool found = includes(numbers, 3); // Menggunakan makro includes
    cout << (found ? "Found 3" : "3 not found") << endl;
    return 0;
}
```

**Contoh Output**:

```
Found 3
```

---

### 8. `#define concat(arr1, arr2)`

**Penjelasan**: Makro ini menggabungkan dua array `arr1` dan `arr2`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define concat(arr1, arr2) (arr1.insert(arr1.end(), arr2.begin(), arr2.end()))
using namespace std;

int main() {
    vector<int> arr1 = {1, 2, 3};
    vector<int> arr2 = {4, 5, 6};
    concat(arr1, arr2); // Menggunakan makro concat
    for (int x : arr1) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2 3 4 5 6
```

---

### 9. `#define slice(arr, start, end)`

**Penjelasan**: Makro ini mengambil irisan dari `arr` dari indeks `start` hingga `end`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define slice(arr, start, end) (std::vector<decltype(arr[0])>(arr.begin() + start, arr.begin() + end))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    auto subArray = slice(numbers, 1, 4); // Menggunakan makro slice
    for (int x : subArray) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
2 3 4
```

---

### 10. `#define indexOf(arr, value)`

**Penjelasan**: Makro ini mengembalikan indeks dari `value` dalam `arr`, atau `arr.size()` jika tidak ditemukan.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define indexOf(arr, value) (std::find(arr.begin(), arr.end(), value) - arr.begin())
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    int index = indexOf(numbers, 3); // Menggunakan makro indexOf
    cout << "Index of 3: " << (index < numbers.size() ? index : -1) << endl;
    return 0;
}


```

**Contoh Output**:

```
Index of 3: 2
```

---

### 11. `#define find(arr, func)`

**Penjelasan**: Makro ini mencari elemen dalam `arr` yang memenuhi fungsi `func`, mengembalikan elemen tersebut atau `-1` jika tidak ditemukan.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define find(arr, func) ({ auto it = std::find_if(arr.begin(), arr.end(), func); (it != arr.end() ? *it : -1); })
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    auto found = find(numbers, [](int x) { return x > 3; }); // Menggunakan makro find
    cout << "First number greater than 3: " << (found == -1 ? -1 : found) << endl;
    return 0;
}
```

**Contoh Output**:

```
First number greater than 3: 4
```

---

### 12. `#define fill(arr, value)`

**Penjelasan**: Makro ini mengisi semua elemen dalam `arr` dengan `value`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define fill(arr, value) (std::fill(arr.begin(), arr.end(), value))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    fill(numbers, 0); // Menggunakan makro fill
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
0 0 0 0 0
```

---

### 13. `#define reverse(arr)`

**Penjelasan**: Makro ini membalik urutan elemen dalam `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define reverse(arr) (std::reverse(arr.begin(), arr.end()))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    reverse(numbers); // Menggunakan makro reverse
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
5 4 3 2 1
```

---

### 14. `#define sortAsc(arr)`

**Penjelasan**: Makro ini mengurutkan elemen dalam `arr` secara ascending.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define sortAsc(arr) (std::sort(arr.begin(), arr.end()))
using namespace std;

int main() {
    vector<int> numbers = {5, 3, 1, 4, 2};
    sortAsc(numbers); // Menggunakan makro sortAsc
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2 3 4 5
```

---

### 15. `#define sortDesc(arr)`

**Penjelasan**: Makro ini mengurutkan elemen dalam `arr` secara descending.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define sortDesc(arr) (std::sort(arr.rbegin(), arr.rend()))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3, 4, 5};
    sortDesc(numbers); // Menggunakan makro sortDesc
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
5 4 3 2 1
```

---

### 16. `#define unique(arr)`

**Penjelasan**: Makro ini menghapus elemen duplikat dalam `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define unique(arr) ({ std::sort(arr.begin(), arr.end()); arr.erase(std::unique(arr.begin(), arr.end()), arr.end()); })
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 2, 3, 4, 4, 5};
    unique(numbers); // Menggunakan makro unique
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2 3 4 5
```

---

### 17. `#define push(arr, value)`

**Penjelasan**: Makro ini menambahkan `value` ke akhir `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define push(arr, value) (arr.push_back(value))
using namespace std;

int main() {
    vector<int> numbers;
    push(numbers, 1); // Menggunakan makro push
    push(numbers, 2);
    push(numbers, 3);
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2 3
```

---

### 18. `#define pop(arr)`

**Penjelasan**: Makro ini menghapus elemen terakhir dari `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define pop(arr) (arr.pop_back())
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3};
    pop(numbers); // Menggunakan makro pop
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2
```

---

### 19. `#define shift(arr)`

**Penjelasan**: Makro ini menghapus elemen pertama dari `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define shift(arr) (arr.erase(arr.begin()))
using namespace std;

int main() {
    vector<int> numbers = {1, 2, 3};
    shift(numbers); // Menggunakan makro shift
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
2 3
```

---

### 20. `#define unshift(arr, value)`

**Penjelasan**: Makro ini menambahkan `value` ke awal `arr`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define unshift(arr, value) (arr.insert(arr.begin(), value))
using namespace std;

int main() {
    vector<int> numbers = {2, 3};
    unshift(numbers, 1); // Menggunakan makro unshift
    for (int x : numbers) cout << x << " ";
    return 0;
}
```

**Contoh Output**:

```
1 2 3
```

---

Berikut adalah penjelasan dan contoh penggunaan untuk setiap makro string yang Anda sebutkan:

### 1. `#define startsWith(str, prefix)`

**Penjelasan**: Makro ini memeriksa apakah string `str` dimulai dengan `prefix`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define startsWith(str, prefix) (str.rfind(prefix, 0) == 0)
using namespace std;

int main() {
    string text = "Hello, world!";
    cout << (startsWith(text, "Hello") ? "Yes" : "No") << endl; // Menggunakan makro startsWith
    return 0;
}
```

**Contoh Output**:

```
Yes
```

---

### 2. `#define endsWith(str, suffix)`

**Penjelasan**: Makro ini memeriksa apakah string `str` diakhiri dengan `suffix`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define endsWith(str, suffix) (str.size() >= suffix.size() && 0 == str.compare(str.size()-suffix.size(), suffix.size(), suffix))
using namespace std;

int main() {
    string text = "Hello, world!";
    cout << (endsWith(text, "world!") ? "Yes" : "No") << endl; // Menggunakan makro endsWith
    return 0;
}
```

**Contoh Output**:

```
Yes
```

---

### 3. `#define toUpperCase(str)`

**Penjelasan**: Makro ini mengubah semua karakter dalam `str` menjadi huruf besar.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#define toUpperCase(str) (std::transform(str.begin(), str.end(), str.begin(), ::toupper))
using namespace std;

int main() {
    string text = "Hello, world!";
    toUpperCase(text); // Menggunakan makro toUpperCase
    cout << text << endl;
    return 0;
}
```

**Contoh Output**:

```
HELLO, WORLD!
```

---

### 4. `#define toLowerCase(str)`

**Penjelasan**: Makro ini mengubah semua karakter dalam `str` menjadi huruf kecil.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#define toLowerCase(str) (std::transform(str.begin(), str.end(), str.begin(), ::tolower))
using namespace std;

int main() {
    string text = "Hello, WORLD!";
    toLowerCase(text); // Menggunakan makro toLowerCase
    cout << text << endl;
    return 0;
}
```

**Contoh Output**:

```
hello, world!
```

---

### 5. `#define split(str, delimiter)`

**Penjelasan**: Makro ini membagi string `str` menjadi vektor berdasarkan `delimiter`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>
#define split(str, delimiter) ({ std::vector<std::string> _result; std::string token; std::istringstream tokenStream(str); while (std::getline(tokenStream, token, delimiter)) { _result.push_back(token); } _result; })
using namespace std;

int main() {
    string text = "Hello, world!";
    vector<string> words = split(text, ' '); // Menggunakan makro split
    for (const string& word : words) {
        cout << word << endl;
    }
    return 0;
}
```

**Contoh Output**:

```
Hello,
world!
```

---

### 6. `#define join(arr, delimiter)`

**Penjelasan**: Makro ini menggabungkan elemen dari vektor `arr` menjadi satu string yang dipisahkan oleh `delimiter`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <sstream>
#define join(arr, delimiter) ({ std::ostringstream os; for (int i = 0; i < arr.size(); ++i) { if (i) os << delimiter; os << arr[i]; } os.str(); })
using namespace std;

int main() {
    vector<string> words = {"Hello", "world!"};
    string result = join(words, " "); // Menggunakan makro join
    cout << result << endl;
    return 0;
}
```

**Contoh Output**:

```
Hello world!
```

---

### 7. `#define repeat(str, n)`

**Penjelasan**: Makro ini mengulang string `str` sebanyak `n` kali.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define repeat(str, n) ({ std::string _result; for (int i = 0; i < n; ++i) _result += str; _result; })
using namespace std;

int main() {
    string text = repeat("Hello! ", 3); // Menggunakan makro repeat
    cout << text << endl;
    return 0;
}
```

**Contoh Output**:

```
Hello! Hello! Hello!
```

---

### 8. `#define trim(str)`

**Penjelasan**: Makro ini menghapus spasi di awal dan akhir string `str`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define trim(str) ({ auto start = str.find_first_not_of(' '); auto end = str.find_last_not_of(' '); str.substr(start, end - start + 1); })
using namespace std;

int main() {
    string text = "   Hello, world!   ";
    string trimmedText = trim(text); // Menggunakan makro trim
    cout << trimmedText << endl;
    return 0;
}
```

**Contoh Output**:

```
Hello, world!
```

---

### 9. `#define replace(str, from, to)`

**Penjelasan**: Makro ini mengganti substring `from` dengan `to` dalam string `str`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define replace(str, from, to) ({ size_t start_pos = str.find(from); if(start_pos != std::string::npos) str.replace(start_pos, from.length(), to); str; })
using namespace std;

int main() {
    string text = "Hello, world!";
    string replacedText = replace(text, "world", "C++"); // Menggunakan makro replace
    cout << replacedText << endl;
    return 0;
}
```

**Contoh Output**:

```
Hello, C++!
```

---

### 10. `#define substring(str, start, len)`

**Penjelasan**: Makro ini mengembalikan substring dari `str` mulai dari `start` dengan panjang `len`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define substring(str, start, len) (str.substr(start, len))
using namespace std;

int main() {
    string text = "Hello, world!";
    string sub = substring(text, 7, 5); // Menggunakan makro substring
    cout << sub << endl;
    return 0;
}
```

**Contoh Output**:

```
world
```

---

### 11. `#define length(str)`

**Penjelasan**: Makro ini mengembalikan panjang string `str`.

**Contoh Input**:

```cpp
#include <iostream>
#include <string>
#define length(str) (str.length())
using namespace std;

int main() {
    string text = "Hello, world!";
    cout << "Length: " << length(text) << endl; // Menggunakan makro length
    return 0;
}
```

**Contoh Output**:

```
Length: 13
```

---

Berikut adalah penjelasan dan contoh penggunaan untuk setiap makro yang Anda sebutkan:

### 1. `#define max(a, b)`

**Penjelasan**: Makro ini mengembalikan nilai maksimum antara `a` dan `b`.

**Contoh Input**:

```cpp
#include <iostream>
#define max(a, b) (a > b ? a : b)
using namespace std;

int main() {
    int x = 5, y = 10;
    cout << "Max: " << max(x, y) << endl; // Menggunakan makro max
    return 0;
}
```

**Contoh Output**:

```
Max: 10
```

---

### 2. `#define min(a, b)`

**Penjelasan**: Makro ini mengembalikan nilai minimum antara `a` dan `b`.

**Contoh Input**:

```cpp
#include <iostream>
#define min(a, b) (a < b ? a : b)
using namespace std;

int main() {
    int x = 5, y = 10;
    cout << "Min: " << min(x, y) << endl; // Menggunakan makro min
    return 0;
}
```

**Contoh Output**:

```
Min: 5
```

---

### 3. `#define pow(base, exp)`

**Penjelasan**: Makro ini menghitung pangkat dari `base` yang dipangkatkan dengan `exp`.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define pow(base, exp) (std::pow(base, exp))
using namespace std;

int main() {
    double base = 2.0, exp = 3.0;
    cout << "Power: " << pow(base, exp) << endl; // Menggunakan makro pow
    return 0;
}
```

**Contoh Output**:

```
Power: 8
```

---

### 4. `#define sqrt(n)`

**Penjelasan**: Makro ini menghitung akar kuadrat dari `n`.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define sqrt(n) (std::sqrt(n))
using namespace std;

int main() {
    double num = 16.0;
    cout << "Square Root: " << sqrt(num) << endl; // Menggunakan makro sqrt
    return 0;
}
```

**Contoh Output**:

```
Square Root: 4
```

---

### 5. `#define abs(n)`

**Penjelasan**: Makro ini mengembalikan nilai absolut dari `n`.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define abs(n) (std::abs(n))
using namespace std;

int main() {
    int num = -10;
    cout << "Absolute: " << abs(num) << endl; // Menggunakan makro abs
    return 0;
}
```

**Contoh Output**:

```
Absolute: 10
```

---

### 6. `#define ceil(n)`

**Penjelasan**: Makro ini membulatkan `n` ke atas ke bilangan bulat terdekat.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define ceil(n) (std::ceil(n))
using namespace std;

int main() {
    double num = 4.3;
    cout << "Ceiling: " << ceil(num) << endl; // Menggunakan makro ceil
    return 0;
}
```

**Contoh Output**:

```
Ceiling: 5
```

---

### 7. `#define floor(n)`

**Penjelasan**: Makro ini membulatkan `n` ke bawah ke bilangan bulat terdekat.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define floor(n) (std::floor(n))
using namespace std;

int main() {
    double num = 4.7;
    cout << "Floor: " << floor(num) << endl; // Menggunakan makro floor
    return 0;
}
```

**Contoh Output**:

```
Floor: 4
```

---

### 8. `#define round(n)`

**Penjelasan**: Makro ini membulatkan `n` ke bilangan bulat terdekat.

**Contoh Input**:

```cpp
#include <iostream>
#include <cmath>
#define round(n) (std::round(n))
using namespace std;

int main() {
    double num = 4.5;
    cout << "Rounded: " << round(num) << endl; // Menggunakan makro round
    return 0;
}
```

**Contoh Output**:

```
Rounded: 5
```

---

### 9. `#define random(min, max)`

**Penjelasan**: Makro ini menghasilkan bilangan acak antara `min` dan `max`.

**Contoh Input**:

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#define random(min, max) (min + rand() % (max - min + 1))
using namespace std;

int main() {
    srand(static_cast<unsigned int>(time(0))); // Inisialisasi seed untuk rand()
    cout << "Random: " << random(1, 100) << endl; // Menggunakan makro random
    return 0;
}
```

**Contoh Output**:

```
Random: 42
```

_(Output akan berbeda setiap kali dijalankan.)_

---

### 10. `#define clamp(n, minVal, maxVal)`

**Penjelasan**: Makro ini membatasi nilai `n` agar tidak kurang dari `minVal` dan tidak lebih dari `maxVal`.

**Contoh Input**:

```cpp
#include <iostream>
#include <algorithm>
#define clamp(n, minVal, maxVal) (std::max(minVal, std::min(n, maxVal)))
using namespace std;

int main() {
    int num = 10;
    cout << "Clamped: " << clamp(num, 1, 5) << endl; // Menggunakan makro clamp
    return 0;
}
```

**Contoh Output**:

```
Clamped: 5
```

---

### 11. `#define gcd(a, b)`

**Penjelasan**: Makro ini menghitung pembagi terbesar (GCD) dari dua bilangan `a` dan `b`.

**Contoh Input**:

```cpp
#include <iostream>
#include <numeric>
#define gcd(a, b) (std::gcd(a, b))
using namespace std;

int main() {
    int a = 24, b = 36;
    cout << "GCD: " << gcd(a, b) << endl; // Menggunakan makro gcd
    return 0;
}
```

**Contoh Output**:

```
GCD: 12
```

---

### 12. `#define lcm(a, b)`

**Penjelasan**: Makro ini menghitung kelipatan persekutuan terkecil (LCM) dari dua bilangan `a` dan `b` menggunakan GCD.

**Contoh Input**:

```cpp
#include <iostream>
#include <numeric>
#define gcd(a, b) (std::gcd(a, b))
#define lcm(a, b) ((a * b) / gcd(a, b))
using namespace std;

int main() {
    int a = 4, b = 6;
    cout << "LCM: " << lcm(a, b) << endl; // Menggunakan makro lcm
    return 0;
}
```

**Contoh Output**:

```
LCM: 12
```

---

Berikut adalah penjelasan dan contoh penggunaan untuk makro bitwise dan makro utilitas set dan map yang Anda sebutkan:

### Makro Bitwise

#### 1. `#define andBits(x, y)`

**Penjelasan**: Mengembalikan hasil operasi AND bitwise antara `x` dan `y`.

**Contoh Input**:

```cpp
#include <iostream>
#define andBits(x, y) (x & y)
using namespace std;

int main() {
    int a = 5;  // 0101
    int b = 3;  // 0011
    cout << "AND: " << andBits(a, b) << endl; // Menggunakan makro andBits
    return 0;
}
```

**Contoh Output**:

```
AND: 1
```

---

#### 2. `#define orBits(x, y)`

**Penjelasan**: Mengembalikan hasil operasi OR bitwise antara `x` dan `y`.

**Contoh Input**:

```cpp
#include <iostream>
#define orBits(x, y) (x | y)
using namespace std;

int main() {
    int a = 5;  // 0101
    int b = 3;  // 0011
    cout << "OR: " << orBits(a, b) << endl; // Menggunakan makro orBits
    return 0;
}
```

**Contoh Output**:

```
OR: 7
```

---

#### 3. `#define xorBits(x, y)`

**Penjelasan**: Mengembalikan hasil operasi XOR bitwise antara `x` dan `y`.

**Contoh Input**:

```cpp
#include <iostream>
#define xorBits(x, y) (x ^ y)
using namespace std;

int main() {
    int a = 5;  // 0101
    int b = 3;  // 0011
    cout << "XOR: " << xorBits(a, b) << endl; // Menggunakan makro xorBits
    return 0;
}
```

**Contoh Output**:

```
XOR: 6
```

---

#### 4. `#define notBits(x)`

**Penjelasan**: Mengembalikan hasil operasi NOT bitwise dari `x`.

**Contoh Input**:

```cpp
#include <iostream>
#define notBits(x) (~x)
using namespace std;

int main() {
    int a = 5;  // 0101
    cout << "NOT: " << notBits(a) << endl; // Menggunakan makro notBits
    return 0;
}
```

**Contoh Output**:

```
NOT: -6
```

---

#### 5. `#define shiftLeft(x, n)`

**Penjelasan**: Menggeser bit dari `x` ke kiri sebanyak `n` posisi.

**Contoh Input**:

```cpp
#include <iostream>
#define shiftLeft(x, n) (x << n)
using namespace std;

int main() {
    int a = 5;  // 0101
    cout << "Shift Left: " << shiftLeft(a, 1) << endl; // Menggunakan makro shiftLeft
    return 0;
}
```

**Contoh Output**:

```
Shift Left: 10
```

---

#### 6. `#define shiftRight(x, n)`

**Penjelasan**: Menggeser bit dari `x` ke kanan sebanyak `n` posisi.

**Contoh Input**:

```cpp
#include <iostream>
#define shiftRight(x, n) (x >> n)
using namespace std;

int main() {
    int a = 5;  // 0101
    cout << "Shift Right: " << shiftRight(a, 1) << endl; // Menggunakan makro shiftRight
    return 0;
}
```

**Contoh Output**:

```
Shift Right: 2
```

---

### Utilitas Set dan Map

#### 7. `#define setAdd(s, val)`

**Penjelasan**: Menambahkan `val` ke dalam set `s`.

**Contoh Input**:

```cpp
#include <iostream>
#include <set>
#define setAdd(s, val) (s.insert(val))
using namespace std;

int main() {
    set<int> mySet;
    setAdd(mySet, 10); // Menggunakan makro setAdd
    cout << "Set Size: " << mySet.size() << endl; // Ukuran set
    return 0;
}
```

**Contoh Output**:

```
Set Size: 1
```

---

#### 8. `#define setDelete(s, val)`

**Penjelasan**: Menghapus `val` dari set `s`.

**Contoh Input**:

```cpp
#include <iostream>
#include <set>
#define setDelete(s, val) (s.erase(val))
using namespace std;

int main() {
    set<int> mySet = {1, 2, 3};
    setDelete(mySet, 2); // Menggunakan makro setDelete
    cout << "Set Size: " << mySet.size() << endl; // Ukuran set
    return 0;
}
```

**Contoh Output**:

```
Set Size: 2
```

---

#### 9. `#define setHas(s, val)`

**Penjelasan**: Memeriksa apakah `val` ada di dalam set `s`.

**Contoh Input**:

```cpp
#include <iostream>
#include <set>
#define setHas(s, val) (s.find(val) != s.end())
using namespace std;

int main() {
    set<int> mySet = {1, 2, 3};
    cout << "Has 2: " << (setHas(mySet, 2) ? "Yes" : "No") << endl; // Menggunakan makro setHas
    return 0;
}
```

**Contoh Output**:

```
Has 2: Yes
```

---

#### 10. `#define setSize(s)`

**Penjelasan**: Mengembalikan ukuran dari set `s`.

**Contoh Input**:

```cpp
#include <iostream>
#include <set>
#define setSize(s) (s.size())
using namespace std;

int main() {
    set<int> mySet = {1, 2, 3};
    cout << "Set Size: " << setSize(mySet) << endl; // Menggunakan makro setSize
    return 0;
}
```

**Contoh Output**:

```
Set Size: 3
```

---

#### 11. `#define mapSet(m, key, value)`

**Penjelasan**: Menetapkan `value` ke `key` dalam map `m`.

**Contoh Input**:

```cpp
#include <iostream>
#include <map>
#define mapSet(m, key, value) (m[key] = value)
using namespace std;

int main() {
    map<int, string> myMap;
    mapSet(myMap, 1, "One"); // Menggunakan makro mapSet
    cout << "Map[1]: " << myMap[1] << endl;
    return 0;
}
```

**Contoh Output**:

```
Map[1]: One
```

---

#### 12. `#define mapGet(m, key)`

**Penjelasan**: Mengembalikan nilai yang terkait dengan `key` dalam map `m`.

**Contoh Input**:

```cpp
#include <iostream>
#include <map>
#define mapGet(m, key) (m[key])
using namespace std;

int main() {
    map<int, string> myMap = {{1, "One"}, {2, "Two"}};
    cout << "Map[1]: " << mapGet(myMap, 1) << endl; // Menggunakan makro mapGet
    return 0;
}
```

**Contoh Output**:

```
Map[1]: One
```

---

#### 13. `#define mapHas(m, key)`

**Penjelasan**: Memeriksa apakah `key` ada dalam map `m`.

**Contoh Input**:

```cpp
#include <iostream>
#include <map>
#define mapHas(m, key) (m.find(key) != m.end())
using namespace std;

int main() {
    map<int, string> myMap = {{1, "One"}, {2, "Two"}};
    cout << "Has Key 1: " << (mapHas(myMap, 1) ? "Yes" : "No") << endl; // Menggunakan makro mapHas
    return 0;
}
```

**Contoh Output**:

```
Has Key 1: Yes
```

---

#### 14. `#define mapDelete(m, key)`

**Penjelasan**: Menghapus `key` dari map `m`.

**Contoh Input**:

```cpp
#include <iostream>
#include <map>
#define mapDelete(m, key) (m.erase(key))
using namespace std;

int main() {
    map<int, string> myMap = {{1, "One"}, {2, "Two

"}};
    mapDelete(myMap, 1); // Menggunakan makro mapDelete
    cout << "Has Key 1: " << (mapHas(myMap, 1) ? "Yes" : "No") << endl; // Memeriksa kembali
    return 0;
}
```

**Contoh Output**:

```
Has Key 1: No
```

---

#### 15. `#define mapSize(m)`

**Penjelasan**: Mengembalikan ukuran dari map `m`.

**Contoh Input**:

```cpp
#include <iostream>
#include <map>
#define mapSize(m) (m.size())
using namespace std;

int main() {
    map<int, string> myMap = {{1, "One"}, {2, "Two"}};
    cout << "Map Size: " << mapSize(myMap) << endl; // Menggunakan makro mapSize
    return 0;
}
```

**Contoh Output**:

```
Map Size: 2
```

---

Berikut adalah penjelasan dan contoh penggunaan untuk makro yang berkaitan dengan waktu, tidur, durasi, serta algoritma pengurutan dan pencarian yang Anda sebutkan:

### Makro Waktu dan Tidur

#### 1. `#define now()`

**Penjelasan**: Mengembalikan waktu saat ini dalam bentuk `std::chrono::time_point`.

**Contoh Input**:

```cpp
#include <iostream>
#include <chrono>
#define now() (std::chrono::system_clock::now())
using namespace std;

int main() {
    auto currentTime = now(); // Menggunakan makro now
    cout << "Current Time: " << std::chrono::duration_cast<std::chrono::seconds>(currentTime.time_since_epoch()).count() << " seconds since epoch." << endl;
    return 0;
}
```

**Contoh Output**:

```
Current Time: X seconds since epoch.
```

(_X akan bervariasi tergantung waktu saat dijalankan_)

---

#### 2. `#define sleep(ms)`

**Penjelasan**: Menangguhkan eksekusi thread saat ini selama `ms` milidetik.

**Contoh Input**:

```cpp
#include <iostream>
#include <thread>
#define sleep(ms) (std::this_thread::sleep_for(std::chrono::milliseconds(ms)))
using namespace std;

int main() {
    cout << "Sleeping for 2 seconds..." << endl;
    sleep(2000); // Menggunakan makro sleep
    cout << "Awake!" << endl;
    return 0;
}
```

**Contoh Output**:

```
Sleeping for 2 seconds...
Awake!
```

---

#### 3. `#define duration(start, end)`

**Penjelasan**: Menghitung durasi dalam milidetik antara dua titik waktu `start` dan `end`.

**Contoh Input**:

```cpp
#include <iostream>
#include <chrono>
#define duration(start, end) (std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count())
using namespace std;

int main() {
    auto start = now(); // Menggunakan makro now
    sleep(1000); // Tidur selama 1 detik
    auto end = now(); // Menggunakan makro now
    cout << "Duration: " << duration(start, end) << " ms" << endl; // Menggunakan makro duration
    return 0;
}
```

**Contoh Output**:

```
Duration: 1000 ms
```

(_Durasi akan bervariasi tergantung waktu tidur dan eksekusi_)

---

### Algoritma Pengurutan dan Pencarian

#### 4. `#define binarySearch(arr, value)`

**Penjelasan**: Mengembalikan `true` jika `value` ditemukan dalam `arr` menggunakan pencarian biner.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define binarySearch(arr, value) (std::binary_search(arr.begin(), arr.end(), value))
using namespace std;

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    cout << "Value 3 found: " << (binarySearch(arr, 3) ? "Yes" : "No") << endl; // Menggunakan makro binarySearch
    return 0;
}
```

**Contoh Output**:

```
Value 3 found: Yes
```

---

#### 5. `#define lowerBound(arr, value)`

**Penjelasan**: Mengembalikan indeks pertama dari elemen yang tidak kurang dari `value`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define lowerBound(arr, value) (std::lower_bound(arr.begin(), arr.end(), value) - arr.begin())
using namespace std;

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    cout << "Lower bound of 3: " << lowerBound(arr, 3) << endl; // Menggunakan makro lowerBound
    return 0;
}
```

**Contoh Output**:

```
Lower bound of 3: 2
```

---

#### 6. `#define upperBound(arr, value)`

**Penjelasan**: Mengembalikan indeks pertama dari elemen yang lebih besar dari `value`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define upperBound(arr, value) (std::upper_bound(arr.begin(), arr.end(), value) - arr.begin())
using namespace std;

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    cout << "Upper bound of 3: " << upperBound(arr, 3) << endl; // Menggunakan makro upperBound
    return 0;
}
```

**Contoh Output**:

```
Upper bound of 3: 3
```

---

#### 7. `#define nextPermutation(arr)`

**Penjelasan**: Menghasilkan urutan berikutnya dari `arr` dalam urutan leksikografis.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define nextPermutation(arr) (std::next_permutation(arr.begin(), arr.end()))
using namespace std;

int main() {
    vector<int> arr = {1, 2, 3};
    nextPermutation(arr); // Menggunakan makro nextPermutation
    cout << "Next permutation: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
    return 0;
}
```

**Contoh Output**:

```
Next permutation: 1 3 2
```

---

#### 8. `#define prevPermutation(arr)`

**Penjelasan**: Menghasilkan urutan sebelumnya dari `arr` dalam urutan leksikografis.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define prevPermutation(arr) (std::prev_permutation(arr.begin(), arr.end()))
using namespace std;

int main() {
    vector<int> arr = {3, 2, 1};
    prevPermutation(arr); // Menggunakan makro prevPermutation
    cout << "Previous permutation: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
    return 0;
}
```

**Contoh Output**:

```
Previous permutation: 2 3 1
```

---

Berikut adalah penjelasan yang lebih mendetail untuk setiap makro yang diberikan, termasuk contoh kode dan bagaimana pengguna dapat menginput data untuk menggunakan makro tersebut.

### 1. **Graph Operations**

#### 1.1. `#define addEdge(adj, u, v)`

**Penjelasan**: Makro ini menambahkan tepi (edge) dari simpul `u` ke simpul `v` dalam graf yang direpresentasikan sebagai daftar ketetanggaan.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define addEdge(adj, u, v) (adj[u].push_back(v))
using namespace std;

int main() {
    int n; // Jumlah simpul
    cout << "Masukkan jumlah simpul: ";
    cin >> n;

    vector<vector<int>> adj(n); // Daftar ketetanggaan
    int edges; // Jumlah tepi
    cout << "Masukkan jumlah tepi: ";
    cin >> edges;

    for (int i = 0; i < edges; i++) {
        int u, v; // Simpul awal dan akhir
        cout << "Masukkan tepi (u v): ";
        cin >> u >> v;
        addEdge(adj, u, v); // Menambahkan tepi
    }

    cout << "Graf berhasil dibangun." << endl;
    return 0;
}
```

---

#### 1.2. `#define addEdgeWeighted(adj, u, v, w)`

**Penjelasan**: Makro ini menambahkan tepi berbobot dari simpul `u` ke simpul `v` dengan bobot `w`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define addEdgeWeighted(adj, u, v, w) (adj[u].push_back({v, w}))

int main() {
    int n; // Jumlah simpul
    cout << "Masukkan jumlah simpul: ";
    cin >> n;

    vector<vector<pair<int, int>>> adj(n); // Daftar ketetanggaan berbobot
    int edges; // Jumlah tepi
    cout << "Masukkan jumlah tepi: ";
    cin >> edges;

    for (int i = 0; i < edges; i++) {
        int u, v, w; // Simpul awal, akhir, dan bobot
        cout << "Masukkan tepi berbobot (u v w): ";
        cin >> u >> v >> w;
        addEdgeWeighted(adj, u, v, w); // Menambahkan tepi berbobot
    }

    cout << "Graf berbobot berhasil dibangun." << endl;
    return 0;
}
```

---

### 2. **Graph Traversal**

#### 2.1. `#define dfs(adj, v, visited, func)`

**Penjelasan**: Makro ini melakukan traversing graf menggunakan DFS (Depth-First Search) mulai dari simpul `v`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define dfs(adj, v, visited, func) ({ visited[v] = true; func(v); for (auto& u : adj[v]) if (!visited[u]) dfs(adj, u, visited, func); })
using namespace std;

void visit(int v) {
    cout << "Mengunjungi: " << v << endl; // Fungsi yang dipanggil saat mengunjungi simpul
}

int main() {
    int n; // Jumlah simpul
    cout << "Masukkan jumlah simpul: ";
    cin >> n;

    vector<vector<int>> adj(n); // Daftar ketetanggaan
    int edges; // Jumlah tepi
    cout << "Masukkan jumlah tepi: ";
    cin >> edges;

    for (int i = 0; i < edges; i++) {
        int u, v; // Simpul awal dan akhir
        cout << "Masukkan tepi (u v): ";
        cin >> u >> v;
        addEdge(adj, u, v); // Menambahkan tepi
    }

    vector<bool> visited(n, false); // Array untuk melacak simpul yang sudah dikunjungi
    int start; // Simpul awal untuk DFS
    cout << "Masukkan simpul awal untuk DFS: ";
    cin >> start;

    cout << "Hasil DFS: " << endl;
    dfs(adj, start, visited, visit); // Melakukan DFS
    return 0;
}
```

---

#### 2.2. `#define bfs(adj, v, func)`

**Penjelasan**: Makro ini melakukan traversing graf menggunakan BFS (Breadth-First Search) mulai dari simpul `v`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#define bfs(adj, v, func) ({ std::queue<int> q; std::vector<bool> visited(adj.size(), false); q.push(v); visited[v] = true; while (!q.empty()) { int u = q.front(); q.pop(); func(u); for (auto& w : adj[u]) if (!visited[w]) { q.push(w); visited[w] = true; } } })
using namespace std;

void visit(int v) {
    cout << "Mengunjungi: " << v << endl; // Fungsi yang dipanggil saat mengunjungi simpul
}

int main() {
    int n; // Jumlah simpul
    cout << "Masukkan jumlah simpul: ";
    cin >> n;

    vector<vector<int>> adj(n); // Daftar ketetanggaan
    int edges; // Jumlah tepi
    cout << "Masukkan jumlah tepi: ";
    cin >> edges;

    for (int i = 0; i < edges; i++) {
        int u, v; // Simpul awal dan akhir
        cout << "Masukkan tepi (u v): ";
        cin >> u >> v;
        addEdge(adj, u, v); // Menambahkan tepi
    }

    int start; // Simpul awal untuk BFS
    cout << "Masukkan simpul awal untuk BFS: ";
    cin >> start;

    cout << "Hasil BFS: " << endl;
    bfs(adj, start, visit); // Melakukan BFS
    return 0;
}
```

---

### 3. **Shortest Path Algorithm**

#### 3.1. `#define dijkstra(adj, src, dist)`

**Penjelasan**: Makro ini mengimplementasikan algoritma Dijkstra untuk menemukan jarak terpendek dari sumber `src` ke semua simpul dalam graf berbobot.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
#define dijkstra(adj, src, dist) ({ std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<std::pair<int, int>>> pq; pq.push({0, src}); dist[src] = 0; while (!pq.empty()) { int u = pq.top().second; pq.pop(); for (auto& [v, weight] : adj[u]) { if (dist[u] + weight < dist[v]) { dist[v] = dist[u] + weight; pq.push({dist[v], v}); } } } })
using namespace std;

int main() {
    int n; // Jumlah simpul
    cout << "Masukkan jumlah simpul: ";
    cin >> n;

    vector<vector<pair<int, int>>> adj(n); // Daftar ketetanggaan berbobot
    int edges; // Jumlah tepi
    cout << "Masukkan jumlah tepi: ";
    cin >> edges;

    for (int i = 0; i < edges; i++) {
        int u, v, w; // Simpul awal, akhir, dan bobot
        cout << "Masukkan tepi berbobot (u v w): ";
        cin >> u >> v >> w;
        addEdgeWeighted(adj, u, v, w); // Menambahkan tepi berbobot
    }

    vector<int> dist(n, numeric_limits<int>::max()); // Jarak dari sumber
    int src; // Simpul sumber
    cout << "Masukkan simpul sumber untuk Dijkstra: ";
    cin >> src;

    dijkstra(adj, src, dist); // Menjalankan Dijkstra

    cout << "Jarak terpendek dari sumber " << src << " adalah

:" << endl;
    for (int i = 0; i < n; i++) {
        cout << "Simpul " << i << ": " << (dist[i] == numeric_limits<int>::max() ? -1 : dist[i]) << endl;
    }

    return 0;
}
```

Tentu! Mari kita bahas lebih dalam mengenai istilah-istilah yang muncul dalam algoritma Dijkstra, khususnya mengenai `adj`, `src`, dan `dist`.

### 1. **`adj` (Adjacency List)**

- **Definisi**: `adj` adalah struktur data yang digunakan untuk merepresentasikan graf. Dalam konteks algoritma Dijkstra, `adj` biasanya adalah array atau vector dari list yang berisi pasangan node dan bobot dari sisi yang menghubungkan node tersebut.
- **Contoh**: Jika kita memiliki graf yang terdiri dari beberapa node, `adj` bisa diisi sebagai berikut:

  ```cpp
  // Misalkan kita memiliki graf dengan 3 node
  vector<vector<pair<int, int>>> adj(3);
  // Node 0 terhubung ke node 1 dengan bobot 2
  adj[0].push_back(make_pair(1, 2));
  // Node 0 terhubung ke node 2 dengan bobot 4
  adj[0].push_back(make_pair(2, 4));
  // Node 1 terhubung ke node 2 dengan bobot 1
  adj[1].push_back(make_pair(2, 1));
  ```

  Di sini, `adj[0]` menunjukkan bahwa dari node 0, kita dapat mencapai node 1 dengan bobot 2 dan node 2 dengan bobot 4.

### 2. **`src` (Source Node)**

- **Definisi**: `src` adalah node awal dari mana kita mulai menghitung jarak terpendek ke semua node lain di dalam graf. Biasanya, kita akan menentukan `src` sebagai input dari pengguna atau dalam kode kita.

- **Contoh**: Jika kita ingin menghitung jarak terpendek dari node 0, maka kita akan mengatur `src` menjadi 0.

### 3. **`dist` (Distance Array)**

- **Definisi**: `dist` adalah array yang menyimpan jarak terpendek dari node sumber (`src`) ke setiap node lainnya. Jarak akan diupdate selama algoritma Dijkstra berjalan.

- **Contoh**: Setelah menjalankan algoritma Dijkstra, jika kita memiliki 3 node, `dist` bisa jadi seperti ini:

  ```cpp
  dist[0] = 0; // Jarak dari src (node 0) ke dirinya sendiri
  dist[1] = 2; // Jarak terpendek dari node 0 ke node 1
  dist[2] = 3; // Jarak terpendek dari node 0 ke node 2
  ```

### Kesimpulan

- **`adj`**: Menyimpan informasi tentang graf (hubungan antar node dan bobot sisi).
- **`src`**: Menunjukkan node awal dari mana pencarian jarak terpendek dimulai.
- **`dist`**: Menyimpan jarak terpendek dari `src` ke setiap node di graf.

---

### 4. **Miscellaneous Functions**

#### 4.1. `#define isEven(n)`

**Penjelasan**: Makro ini memeriksa apakah angka `n` adalah genap.

**Contoh Input**:

```cpp
#include <iostream>
#define isEven(n) (n % 2 == 0)
using namespace std;

int main() {
    int n; // Angka yang akan diperiksa
    cout << "Masukkan angka: ";
    cin >> n;

    if (isEven(n)) {
        cout << n << " adalah genap." << endl;
    } else {
        cout << n << " adalah ganjil." << endl;
    }

    return 0;
}
```

---

#### 4.2. `#define isOdd(n)`

**Penjelasan**: Makro ini memeriksa apakah angka `n` adalah ganjil.

**Contoh Input**:

```cpp
#include <iostream>
#define isOdd(n) (n % 2 != 0)
using namespace std;

int main() {
    int n; // Angka yang akan diperiksa
    cout << "Masukkan angka: ";
    cin >> n;

    if (isOdd(n)) {
        cout << n << " adalah ganjil." << endl;
    } else {
        cout << n << " adalah genap." << endl;
    }

    return 0;
}
```

---

#### 4.3. `#define swap(a, b)`

**Penjelasan**: Makro ini menukar nilai dua variabel `a` dan `b`.

**Contoh Input**:

```cpp
#include <iostream>
#include <utility>
#define swap(a, b) (std::swap(a, b))
using namespace std;

int main() {
    int a, b; // Dua angka untuk ditukar
    cout << "Masukkan dua angka (a b): ";
    cin >> a >> b;

    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    swap(a, b); // Menukar nilai
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;

    return 0;
}
```

---

#### 4.4. `#define repeat(n, func)`

**Penjelasan**: Makro ini mengulangi pemanggilan fungsi `func` sebanyak `n` kali.

**Contoh Input**:

```cpp
#include <iostream>
#define repeat(n, func) for (int i = 0; i < n; i++) func()
using namespace std;

void hello() {
    cout << "Hello, World!" << endl;
}

int main() {
    int n; // Jumlah pengulangan
    cout << "Masukkan jumlah pengulangan: ";
    cin >> n;

    repeat(n, hello); // Mengulangi pemanggilan fungsi
    return 0;
}
```

---

#### 4.5. `#define range(start, end)`

**Penjelasan**: Makro ini menghasilkan vektor yang berisi bilangan bulat dari `start` hingga `end`.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#include <numeric>
#define range(start, end) (std::vector<int>(std::iota(start, end)))
using namespace std;

int main() {
    int start, end; // Batas rentang
    cout << "Masukkan batas awal dan akhir (start end): ";
    cin >> start >> end;

    vector<int> numbers = range(start, end); // Menghasilkan rentang

    cout << "Rentang: ";
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

---

#### 4.6. `#define print(arr)`

**Penjelasan**: Makro ini mencetak elemen dalam array atau vector.

**Contoh Input**:

```cpp
#include <iostream>
#include <vector>
#define print(arr) (for (auto& item : arr) std::cout << item << ' '; std::cout << std::endl)
using namespace std;

int main() {
    vector<int> arr = {1, 2, 3, 4, 5}; // Array contoh
    cout << "Isi array: ";
    print(arr); // Mencetak isi array
    return 0;
}
```

---
