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

### Алгоритм скользящего окна