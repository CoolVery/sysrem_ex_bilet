## Создание функции, аргументом которой является указатель на функцию. Создать не менее двух вспомогательных функций и передать их в качестве аргумента исходной функции. Продемонстрировать специфику работы исходной функции в зависимости от переданных параметров (отдельно для Windows и Linux)


-----


Код будет работать как на винде, так и линуксе
Для линукса надо убрать system и при компиляции добавить флаг -lm для мат формул
```C
#include <stdio.h>
#include <math.h> 

// Указатель, который вернет double (*НазваниеЛюбое)(Че передать надо)
typedef double (*MathFunction)(double);

//Далее просто создаем всякие функции
// Вспомогательная функция: возведение в квадрат
double square(double x) {
    return x * x;
}

// Вспомогательная функция: возведение в куб
double cube(double x) {
    return x * x * x;
}

//Данная функция принимает в себя указатель из самого верха и выполняет функцию
// Основная функция, принимающая указатель на математическую функцию
double calculate(MathFunction func, double x) {
    if (func == NULL) {
        return 0; // Обработка случая NULL-указателя
    }
    return func(x);
}

int main() {
    system("chcp 1251");
    double num = 5.0;

    // Вызываем calculate с разными функциями
    printf("Квадрат %.2f: %.2f\n", num, calculate(square, num));
    printf("Куб %.2f: %.2f\n", num, calculate(cube, num));

    // Пример с pow
    printf("%.2f в степени 3 (pow): %.2f\n", num, calculate(pow, num));

    // Пример с NULL указателем
    printf("Вызов с NULL указателем: %.2f\n", calculate(NULL, num));

    return 0;
}
```