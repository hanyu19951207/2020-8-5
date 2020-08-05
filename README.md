# 2020-8-5
1460. 通过翻转子数组使两个数组相等
      给你两个长度相同的整数数组 target 和 arr 。
      每一步中，你可以选择 arr 的任意 非空子数组 并将它翻转。你可以执行此过程任意次。
      如果你能让 arr 变得与 target 相同，返回 True；否则，返回 False 。
      示例 1：
      输入：target = [1,2,3,4], arr = [2,4,1,3]
      输出：true
      解释：你可以按照如下步骤使 arr 变成 target：
      1- 翻转子数组 [2,4,1] ，arr 变成 [1,4,2,3]
      2- 翻转子数组 [4,2] ，arr 变成 [1,2,4,3]
      3- 翻转子数组 [4,3] ，arr 变成 [1,2,3,4]
      上述方法并不是唯一的，还存在多种将 arr 变成 target 的方法。
题解：
本题思路：
    1.长度不等 false
    2.排序，每一位比较，如有不等 false
    3.否则，为true

class Solution {
    public boolean canBeEqual(int[] target, int[] arr) {
        if(arr.length != target.length)
            return false;
        Arrays.sort(target);
        Arrays.sort(arr);
        for(int i = 0;i < arr.length;i++){
            if(arr[i] != target[i])
                return false;
        }
        return true;
    }
}

1461. 检查一个字符串是否包含所有长度为 K 的二进制子串
      给你一个二进制字符串 s 和一个整数 k 。
      如果所有长度为 k 的二进制字符串都是 s 的子串，请返回 True ，否则请返回 False 。
      示例 1：
      输入：s = "00110110", k = 2
      输出：true
      解释：长度为 2 的二进制串包括 "00"，"01"，"10" 和 "11"。它们分别是 s 中下标为 0，1，3，2 开始的长度为 2 的子串。
 题解：
 思路：HashSet的特性为不能存储重复的元素，然后利用Set元素的唯一性设置定长滑动窗口，来获取字符串所有的定长子串。题目中所有0,1组成的k长度的组合一共有2的k次方个，所以最后
      Set的长度和2的K次方相等即为true。
 class Solution {
    public boolean hasAllCodes(String s, int k) {
        int left = 0,rigth = k;
        int len = s.length();
        Set<String> set = new HashSet<>();
        //获取s所有的不重复子串
        while(rigth <= len){
            set.add(s.substring(left,rigth));
            left++;
            rigth++;
        }
        //Math.pow()方法作用为返回2的k次方.
        return set.size() == Math.pow(2,k);
    }
}
      
      
