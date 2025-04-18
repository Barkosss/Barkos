# Скользящее окно

## Задача
> Для массива, состоящего из n целых чисел, найдите непрерывный подмассив заданной длины k, который имеет максимальное среднее значение. Нужно вывести максимальное среднее значение.
> ```
> Аргументы: args = [1, 12, -5, -6, 50, 3], k = 4
> Ответ: 12.75
> Объяснение: Максимальное среднее — это (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
> ```

## Брутфорс
```python
import sys
def findMaxAverage(nums: list, k: int):
  maxAverage = -sys.maxint - 1

  for i in range(len(nums) - k + 1):
    sum = 0

    for j in range(i, i + k):
      sum += nums[j]

    maxAverage = max(maxAverage, sum / k)

  return maxAverage


print(findMaxAverage([1, 12, -5, -6, 50, 3], 4))
```
> Сложность - O(n * k)

Если внимательно взглянуть на текущее решение, то легко заметить, что при каждом сдвиге мы заново высчитываем сумму элементов. 
Решение этой ситуации будет, так называемое, скользящее окно.

## Скользим
Чтобы переиспользовать рассчитанную для предыдущего подмассива сумму, достаточно вычесть элемент выпадающий из окна и добавить новый, попавший в окно.

![](https://wcademy.ru/static/f1ba248cc7280856b60468bb8d195fcd/fa5c1/sliding-window.png)

```python
import sys
def findMaxAverage(nums: list, k: int):
  sum = 0
  for i in range(k):
    sum += nums[i]

  maxAverage = sum

  for i in range(k, len(nums)):
    sum += nums[i] - nums[i - k]
    maxAverage = max(maxAverage, sum)

  return maxAverage / k


print(findMaxAverage([1, 12, -5, -6, 50, 3], 4))
```
> Сложность - O(n)

## Когда стоит использовать скользящее окно?
- В задаче передаётся упорядоченная и итерируемая структура данных, вроде массива или строки
- Просят найти подпоследовательность в массиве/строке, самое длинное/короткое, среднее/большое/маленькое и т. д.
- Первым в голову приходит наивное решение со сложностью O(n^2) или даже O(2^n)

Метод скользящего окна позволяет улучшить вычислительную сложность до линейной, а по памяти — до константной.

# Задачи для тренировки:
1. [239. Sliding Window Maximum | HARD](https://leetcode.com/problems/sliding-window-maximum/description/)
2. [480. Sliding Window Median | HARD](https://leetcode.com/problems/sliding-window-median/description/)
3. [76. Minimum Window Substring | HARD](https://leetcode.com/problems/minimum-window-substring/description/)
