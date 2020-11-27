# Задачи с leetcode

Тут будут содержаться всякие пояснения к задачам литкода, а также теория про алгоритмы, которые я использовал/подсмотрел в решениях задач. Каждый день я хочу решать хотя бы по одной задаче, чтобы поднимать свой скилл. 

## Задача 2. Сложить два числа 

Условие: https://leetcode.com/problems/add-two-numbers/

Решение

```java
 public class ListNode {
  int val;
  ListNode next;
  ListNode() {}
  ListNode(int val) { this.val = val; }
  ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode t1 = l1, t2 = l2, curr = result;
        int car = 0;
        while (t1 != null || t2 != null){
            int x = (t1 != null) ? t1.val : 0;
            int y = (t2 != null) ? t2.val : 0;
            int sum = car + x + y;
            car = sum / 10; 
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
            if (t1 != null) t1 = t1.next;
            if (t2 != null) t2 = t2.next;
        }
        if (car > 0){
            curr.next = new ListNode(car);
        }
        return result.next;
    }
}
```



Для решения создаем временные ноды: нод с результатом, а также 2 нода с исходными данными. 

Алгоритм состоит в том, чтобы просто проходить пока оба списка не пустые и складывать по порядку. Переменная car нужна для переноса разряда. Перед присваиванием значений аргументов необходимо проверить не пусты ли они, потому что может оказаться ситуация, когда, например, t1 уже пустой, а t2 еще нет. В этом случае мы попытаемся обратиться к null полю, что в последствии вызовет ошибку. 

## Задача 3. Самая длинная последовательность символов без повтора в строке 

Условие: https://leetcode.com/problems/longest-substring-without-repeating-characters/

Конечно же, для решения задачи можно использовать брутфорс, но это совсем печально и некрасиво, мы же будем использовать более красивый алгоритм -- алгоритм скользящего окна. 

### Алгоритм скользящего окна

Проблема брутфорса -- его скорость, данный алгоритм очень медленный и некрасивый. 

Алгоритм скользящего окна -- абстракная модель, используемая для решения задач с массивами и строками. Основная суть алгоритма состоит в том, что мы создаем определенное "окно" и перемещаемся с определенной частотой 

Для лучшего понимания представим строку "приветкакдела". Нам нужно окно размером 3 с шагом 1. Посмотрим как это будет выглядеть. 

1. **при**веткакдела

2. п**рив**еткакдела

3. пр**иве**ткакдела

   И так далее 

Реализация скользящего окна у нас будет с помощью множества, а реализовывать будет HashSet.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        while (i < n && j < n) {
            if (!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            }
            else {
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
}
```

1. Сначала мы узнаем длину строки и инициализируем наш HashSet
2. Подготавливаем переменные ans -- ответ
3. а дальше я сам не понимаю если честно



### **Задача 7 Развернуть число**

Вроде простейшая задача, но тут литкод выдал, что решение эффективнее 100 процентов решений. 

Решение даже стыдно объяснять, пожтому просто пусть будет здесь 

```java
class Solution {
    public int reverse(int x) {
        long result = 0;
        
        while (x != 0){
            result = result*10 + (x % 10);
            x = x/10;
        }
        
        if (result > Integer.MAX_VALUE || result < Integer.MIN_VALUE){
            return 0;
        }
        return (int)result;
    }
}
```

