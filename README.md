#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char str[1000];
    int latin_count = 0, russian_count = 0;
    
    printf("Введите строку: ");
    fgets(str, sizeof(str), stdin);
    
    // Удаляем символ новой строки
    str[strcspn(str, "\n")] = '\0';
    
    // Проходим по всем символам строки
    for (int i = 0; str[i] != '\0'; i++) {
        // Проверяем латинские строчные буквы
        if (str[i] >= 'a' && str[i] <= 'z') {
            latin_count++;
        }
        // Проверяем русские строчные буквы (Windows-1251 кодировка)
        // а-п: 224-239, р-я: 240-255
        else if ((unsigned char)str[i] >= 224 && (unsigned char)str[i] <= 255) {
            russian_count++;
        }
    }
    
    printf("\nРезультаты:\n");
    printf("Латинских строчных букв: %d\n", latin_count);
    printf("Русских строчных букв: %d\n", russian_count);
    printf("Всего строчных букв: %d\n", latin_count + russian_count);
    
    return 0;
}
