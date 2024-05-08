# «Выстраивание процесса непрерывной интеграции»

## Решения
### Задание 1
* <a href="https://github.com/Nephedov/8.1.Java/blob/main/pom.xml">pom.xml</a> - c JaCoCo, генерацией отчетов и проверкой 100% покрытия строк.
* <a href="https://github.com/Nephedov/8.1.Java/blob/main/.github/workflows/maven.yml">maven.yml</a> - Github CI с verify-сборкой.
* <a href="https://github.com/Nephedov/8.1.Java/blob/main/src/test/java/ru/netology/statistic/StatisticsServiceTest.java">StatisticsServiceTest.java</a> - автотесты.

<a href="https://github.com/Nephedov/8.1.Java/tree/main">Репозиторий</a> с проектом JaCoCo.
### Задание 2
* <a href="https://github.com/Nephedov/8.2.Java/blob/main/pom.xml">pom.xml</a> - с подключенными JaCoCo, SpotBugs и SpotBugs Maven Plugin.

<a href="https://github.com/Nephedov/8.2.Java/tree/main">Репозиторий</a> с проектом JaCoCo + SpotBugs + SpotBugs Maven Plugin.

### Задание 3
* <a href="https://github.com/Nephedov/8.3.Java/blob/a9b5bddfceabf2e3ccf64ce14c4cc17e32d825a6/pom.xml">pom.xml</a> - с подключенным JaCoCo и Maven Checkstyle Plugin.

<a href="https://github.com/Nephedov/8.3.Java/tree/main">Репозиторий</a> с проектом JaCoCo + Maven Checkstyle Plugin.

## Что было сделано
### Задание1
* Создан Maven проект и настроен <a href="https://github.com/Nephedov/8.1.Java/blob/main/pom.xml">pom.xml</a> с плагинами и зависимостями:
  * JunitJupiter.
  * Maven Surefire Plugin.
  * JaCoCo.
* Настроен <a href="https://github.com/Nephedov/8.1.Java/blob/main/.github/workflows/maven.yml">maven.yml</a> для Github CI с verify-сборкой.
* Дописаны автотесты в классе <a href="https://github.com/Nephedov/8.1.Java/blob/main/src/test/java/ru/netology/statistic/StatisticsServiceTest.java">StatisticsServiceTest.java</a>

### Задание 2
* Создан Maven проект и настроен <a href="https://github.com/Nephedov/8.2.Java/blob/main/pom.xml">pom.xml</a> с плагинами и зависимостями:
  * JunitJupiter.
  * Maven Surefire Plugin.
  * JaCoCo.
  * SpotBugs.
  * SpotBugs Maven Plugin.
* Настроен <a href="https://github.com/Nephedov/8.2.Java/blob/main/.github/workflows/maven.yml">maven.yml</a> для Github CI с verify-сборкой.

### Задание 3
* Создан Maven проект и настроен <a href="https://github.com/Nephedov/8.3.Java/blob/main/pom.xml">pom.xml</a> с плагинами и зависимостями:
  * JunitJupiter.
  * Maven Surefire Plugin.
  * JaCoCo.
  * Maven Checkstyle Plugin.
* Настроен <a href="https://github.com/Nephedov/8.3.Java/blob/main/.github/workflows/maven.yml">maven.yml</a> для Github CI с verify-сборкой.


# Описание Задания 1. Синдром 100% (обязательное к выполнению)

Вы попали в команду максималистов, которые хотят, чтобы те автотесты, которые вы пишете, покрывали код на 100%.

Что вам нужно
1. Создать Мавен-проект с тестируемым кодом из листинга кода, он указан ниже по условию.
1. Внедрить эту цель во фазу `verify`.
1. Выбрать один из счётчиков и добиться 100% покрытия через добавление новых тестов.

**Важно**: использовать можно только один из следующих: 
1. `INSTRUCTION`
1. `LINE`
1. `BRANCH`

Тестируемый код, его как-либо редактировать **нельзя**:
```java
package ru.netology.statistic;

public class StatisticsService {
  /**
   * Calculate index of max income
   *
   * @param incomes - array of incomes
   * @return - index of first max value
   */
  public long findMax(long[] incomes) {
    long current_max_index = 0;
    long current_max = incomes[0];
    for (long income : incomes)
      if (current_max < income)
        current_max = income;
        return current_max;
  }
}
```

Класс с тестами, его надо будет расширить новыми тестами:
```java
package ru.netology.statistic;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

public class StatisticsServiceTest {

  @Test
  void findMax() {
    StatisticsService service = new StatisticsService();

    long[] incomesInBillions = {12, 5, 8, 4, 5, 3, 8, 6, 11, 11, 12};
    long expected = 12;

    long actual = service.findMax(incomesInBillions);

    assertEquals(expected, actual);
  }
}
```

# Описание Задания 2*. Пусть плагин ищет баги (необязательная задача)

[SpotBugs](https://spotbugs.github.io) и [Maven Plugin для него](https://spotbugs.readthedocs.io/en/latest/maven.html) предоставляют возможность производить статический анализ, то есть анализ кода без его запуска, для выявления наиболее часто встречающихся багов.

[Список багов, которые ищет SpotBugs](https://spotbugs.readthedocs.io/en/latest/bugDescriptions.html).

Ваша задача
1. Подключить плагин к вашему проекту. Возьмите проект из первой задачи или создайте новый на его базе.
1. Настроить goal `check` в фазу `verify`.
1. Удостовериться, что код проходит проверки SpotBugs, если не проходит, то пофиксить.
1. Сделать push в GitHub и удостовериться, что сборка проходит.
