# Домашнее задание №2
🏫 Курс: "Архитектуры вычислительных систем", БПИ216 Багаев Марат, тема: ассемблер, работа со строками

# Задание на 4 балла
1. Написал код на C - [program.c](program.c)
2. С помощью команды ```gcc program.c -S -o program.s``` получил код на ассемблере - [program.s](program.s)
3. Добавил в код на ассемблере комментарии, поясняющие эквивалентное представление переменных в программе на C - [program.s](program.s)
4. С помощью команды ```gcc -masm=intel -fno-asynchronous-unwind-tables -fno-jump-tables -fno-stack-protector -fno-exceptions program.c -S -o program_nice.s``` убрал из ассемблерного кода лишние макросы - [program_nice.s](program_nice.s)
5. Скомпилировал программу из ассемблера в исполняемый файл с помощью команды ```gcc program_nice.s -o program_nice.exe``` - [program_nice.exe](program_nice.exe) 
6. Написал на питоне тестирующий скрипт - [script.py](script.py). Тестирование ошибок не выявило

# Задание на 5 баллов
1. Функции с передачей данных через парамерты я уже использовал
2. Локальные переменные я тоже использовал
3. Добавил в [program.s](program.s) комментарии, описывающие передачу фактических параметров и перенос возвращаемого результата
4. Комментарии о связи между парамертами функции и регистрами уже были([program.s](program.s))

# Задание на 6 баллов
1. Я заменил следующие переменные со стека на регистры([program_without_vars.s](program_without_vars.s)):
- В функции main заменил int i = -10068[rbp] на r15d
- В функции read заменил int ch = -4[rbp] на r15d
- В функции read заменил int *size = -32[rbp] на r14
- В функции read заменил FILE *stream = -40[rbp] на r13
- В функции read заменил char str[] = -24[rbp] на r12
- В функции countNumbers заменил int i = -4[rbp] на r15d
- В функции countNumbers заменил int size = -28[rbp] на r14d
- В функции countNumbers заменил int numbers_count[] = -40[rbp] на r13
- В функции countNumbers заменил char str[] = -24[rbp] на r12
2. Я надеюсь, что пункта 1 хватит для пояснения эквивалентного использование регистров вместо переменных исходной программы на C
3. Я скомпилировал все программы, которые у меня были и составил таблицу со скоростями их выполнения и памятью, которую они занимают

| Программа                 | Время в секундах   | Память в байтах    |
| --------------------------|:------------------:|:------------------:|
| [program_without_vars.exe](program_without_vars.s)  | 0.0014813077       | 16160              |
| [program_s.exe](program.s)             | 0.0013823280       | 16160              |
| [program_c.exe](program.c)             | 0.0012766633       | 16160              |
| [program_nice.exe](program_nice.s)          | 0.0013167038       | 16104              |

Как и в прошлый раз, почему-то замена переменных на регистры не ускоряет код(возможно из-за того, что тесты на питоне). В этот раз мы узнали, что он и не уменьшает память, требуемую для программы. 

п. с. Я убрал из функции read строчку sub rsp, 48(потому что в функции используются только регистры), но это не помогло(ни по скорости, ни по памяти)

Я только сейчас понял, что возможно под размерами программы подразумевалась длина кода. Я взял первую программу, потом взял вторую программу ~~, перемножил~~ - одно и то же(по длине кода)

# Задание на 7 баллов
1. Создал папку "multi-module project". Разделил исходную программу на три части. Код main функции в файле [main.c](multi-module_project/main.c) на языке C, код функции read в файле [read.s](multi-module_project/read.s) на ассемблере и код функции countNumbers в файле [countNumbers.s](multi-module_project/countNumbers.s), тоже на ассемблере. С помощью команды ```gcc -c main.c read.s countNumbers.s``` превратил их в объектные файлы и далее командой ```gcc *.o -o "multi-module program.exe"``` получил исполняемый файл

Не успел
