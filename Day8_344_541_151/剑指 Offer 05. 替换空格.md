# Day8 剑指 Offer 05. 替换空格

[题目链接](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

转成字符数组再配合StringBuilder一个一个往里添加，简单又快速。

```java
class Solution {
    public String replaceSpace(String s) {
        char[] ch = s.toCharArray();
        StringBuilder ans = new StringBuilder();

        for(int i = 0; i < ch.length; i++){
            if(ch[i] != ' '){
                ans.append(ch[i]);
            } else {
                ans.append("%20");
            }
        }

        return ans.toString();
    }
}
```

其实，真的需要转成字符数组吗？恐怕是因为恰巧刚刚学会这个东西才这么想用toCharArray()，并不需要转。

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder ans = new StringBuilder();

        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) != ' '){
                ans.append(s.charAt(i));
            } else {
                ans.append("%20");
            }
        }

        return ans.toString();
    }
}
```

但这道题其实希望我们用双指针，暂时没看，先留着吧( ╯□╰ ) 

看完了，思路是先通过在字符串尾部填补空格的方式把字符串的长度扩展为最终的长度，然后左指针指向原始字符串的结尾，右指针指向扩展后字符串的结尾。当左指针指向的是空格时，移动右指针填上%20；不是空格时，把左指针指向的字符拷贝给右指针。其实思路和27移除元素是一样的，一个指针指向要放的元素，一个指针指向它应该在的最终位置。不过，这道题体现出了对于填充数组的题目，从后往前处理可以降低时间复杂度，需要好好体会。

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder r = new StringBuilder();
        StringBuilder temp = new StringBuilder();
        int left, right;

        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) == ' '){
                r.append("  ");
            }
        }

        left = s.length() - 1;
        s += r.toString();
        right = s.length() - 1;
        temp.append(s);

        while(left >= 0){
            if(temp.charAt(left) == ' '){
                temp.setCharAt(right--, '0');
                temp.setCharAt(right--, '2');
                temp.setCharAt(right, '%');
            } else {
                temp.setCharAt(right, temp.charAt(left));
            }
            left--;
            right--;
        }

        return temp.toString();
    }
}
```