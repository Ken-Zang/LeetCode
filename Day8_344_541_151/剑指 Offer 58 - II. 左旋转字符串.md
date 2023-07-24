# Day8 剑指 Offer 58 - II. 左旋转字符串

[题目链接](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

可以用字符串反转实现，先将字符串整个反转，再将末尾k个反转，再将剩余的部分反转。

```java
class Solution {
    private void reverseWords(StringBuilder s, int left, int right){ // 左闭右开区间
    right--;
        char temp;
        while(left < right){
            temp = s.charAt(left);
            s.setCharAt(left, s.charAt(right));
            s.setCharAt(right, temp);
            left++;
            right--;
        }
    }

    public String reverseLeftWords(String s, int n) {
        StringBuilder r = new StringBuilder();
        r.append(s);

        reverseWords(r, 0, r.length());
        reverseWords(r, 0, r.length() - n);
        reverseWords(r, r.length() - n, r.length());

        return r.toString();
    }
}
```