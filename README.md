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
      
1464. 数组中两元素的最大乘积
      给你一个整数数组 nums，请你选择数组的两个不同下标 i 和 j，使 (nums[i]-1)*(nums[j]-1) 取得最大值。
      请你计算并返回该式的最大值。
      示例 1：
      输入：nums = [3,4,5,2]
      输出：12 
      解释：如果选择下标 i=1 和 j=2（下标从 0 开始），则可以获得最大值，(nums[1]-1)*(nums[2]-1) = (4-1)*(5-1) = 3*4 = 12 。 
题解：
class Solution {
    public int maxProduct(int[] nums) {
        int max = 0;
        for(int i = 0;i < nums.length - 1;i++){
            for(int j = i + 1;j < nums.length;j++){
                int ans = (nums[i] - 1) * (nums[j] - 1);
                if(ans > max)   max = ans;
            }
        }
        return max;
    }
}

1038. 从二叉搜索树到更大和树
      给出二叉 搜索 树的根节点，该二叉树的节点值各不相同，修改二叉树，使每个节点 node 的新值等于原树中大于或等于 node.val 的值之和。
      提醒一下，二叉搜索树满足下列约束条件：
          节点的左子树仅包含键 小于 节点键的节点。
          节点的右子树仅包含键 大于 节点键的节点。
          左右子树也必须是二叉搜索树。
      示例：
      输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
      输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
题解：
思路：二叉搜索树的中序遍历是一个递增序列，题意原树中序遍历为0,1,2,3,4,5,6,7,8题意为修改后的新值为每个节点的值是原来的节点值加上所有大于它的节点值之和即累加树36,36,35,33,30,26,21,15,8
      观察累加前中序遍历与累加后中序遍历，我们会发现，其实后者就是前者的一个从后的累加结果。那问题就迎刃而解了，我们只需反向中序遍历即可,并把每次的节点值进行累加，就能得到最终的累加树。
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int sum = 0;
    public TreeNode bstToGst(TreeNode root) {
        if(root != null){
        //递归遍历树到达最右叶子节点即为值最大的节点
            bstToGst(root.right);
            sum += root.val;
            root.val = sum;
            bstToGst(root.left);
        }
        return root;
    }
}
