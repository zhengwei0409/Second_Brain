# Kadane's algorithm

- use to solve "maximum subarray sum" 

- 这个方法之所以叫 Kadane's algorithm，纯粹是因为 Jay Kadane 第一个提出了这个思路，用他的名字命名是一种致敬（credit），不是这个名字本身有什么魔法含义。

- 它聪明的地方在于：用一次遍历就搞定了本来需要 n² 次尝试才能解决的问题，核心思路就是"一旦手里的和变成负数，就果断放弃重新开始"。