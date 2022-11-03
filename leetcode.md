# leetcode刷题笔记

#### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int left=0,right=nums.size()-1;
        vector<int> ans(2);
        while(left<=right){
            int mid=left+(right-left)/2;
            if(nums[mid]<target)
            {
                left=mid+1;
            }
            else if(nums[mid]>target)
                right=mid-1;
            else if(nums[mid]==target)
                right=mid-1;
        }
        if(nums.size()==0)
        {
            ans[0]=-1;
            ans[1]=-1;
        }
        else if(left>=nums.size())
        {
            ans[0]=-1;
            ans[1]=-1;
        }
        else if(nums[left]!=target)
        {
            ans[0]=-1;
            ans[1]=-1;
        }
        else
        {
            right=left+1;
            while(right<nums.size())
            {
                if(nums[right]!=target)
                    break;
                right++;
            }     
            ans[0]=left;
            ans[1]=right-1;
        }
        return ans;
    }
};
```



#### [704. 二分查找](https://leetcode.cn/problems/binary-search/)

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left=0,right=nums.size()-1;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            if(nums[mid]<target)
                left=mid+1;
            else if(nums[mid]>target)
                right=mid-1;
            else if(nums[mid]==target)
                return mid;
        }
        if(left>=nums.size())
            return -1;
        return nums[left]==target?left:-1;
    }
};
```



#### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

```
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0,right=nums.size()-1;
        while(left<=right){
            int mid=left+(right-left)/2;
            if(nums[mid]<target)
                left=mid+1;
            else if(nums[mid]>target)
                right=mid-1;
            else
                return mid;
        }
        if(left>=nums.size())
            return nums.size();
        return left;
    }
};
```



#### [74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/)

**题目描述**

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

* 每行中的整数从左到右按升序排列。
* 每行的第一个整数大于前一行的最后一个整数。

当另一个信封的宽度和高度都比这个信封大的时候，这个信封就可以放进另一个信封里，如同俄罗斯套娃一样。

请计算 最多能有多少个 信封能组成一组“俄罗斯套娃”信封（即可以把一个信封放到另一个信封里面）。

注意：不允许旋转信封。

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row = matrix.size(),col = matrix[0].size();
        int len=row*col;
        int left = 0,right = len-1;
        while(left<=right){
            int mid=left+(right-left)/2;
            int i=mid/col,j=mid%col;
            if(matrix[i][j]<target)
                left=mid+1;
            else if(matrix[i][j]>target)
                right=mid-1;
            else if(matrix[i][j]==target)
                return true;
        }
        return false;
    }
};
```



#### [392. 判断子序列](https://leetcode.cn/problems/is-subsequence/)

**题目描述**

给定字符串 s 和 t ，判断 s 是否为 t 的子序列。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。

```c++
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int len1 = t.size(),len2 = s.size();
        int i,j;
        for(i=0,j=0;i<len1&&j<len2;i++)
        {
            if(s[j]==t[i])
                j++;
        }
        return j==len2;
    }
};
```



#### [852. 山脉数组的峰顶索引](https://leetcode.cn/problems/peak-index-in-a-mountain-array/)

**题目描述**

符合下列属性的数组 arr 称为 山脉数组 ：

* arr.length >= 3
* 存在 i（0 < i < arr.length - 1）使得：
  * arr[0] < arr[1] < ... arr[i-1] < arr[i]
  * arr[i] > arr[i+1] > ... > arr[arr.length - 1]

给你由整数组成的山脉数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i 。

```c++
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int len=arr.size();
        int left=0,right=len-1;
        while(left<=right){
            int mid=left+(right-left)/2;
            if(arr[mid+1]>arr[mid])
                left=mid+1;
            else if(arr[mid-1]>arr[mid])
                right=mid-1;
            else if(arr[mid-1]<arr[mid]&&arr[mid+1]<arr[mid])
                return mid;
        }
        return 0;
    }
};
```



#### [1011. 在 D 天内送达包裹的能力](https://leetcode.cn/problems/capacity-to-ship-packages-within-d-days/)

**题目描述**

传送带上的包裹必须在 days 天内从一个港口运送到另一个港口。

传送带上的第 i 个包裹的重量为 weights[i]。每一天，我们都会按给出重量（weights）的顺序往传送带上装载包裹。我们装载的重量不会超过船的最大运载重量。

返回能在 days 天内将传送带上的所有包裹送达的船的最低运载能力。

```c++
class Solution {
public:
    bool isLeft(vector<int>& weights,int days,int maxWeight){
        int count=0;
        int temp=maxWeight;
        for(int i=0;i<weights.size();)
        {
            if(temp>=weights[i])
            {
                temp-=weights[i];
                i++;
            }   
            else
            {
                temp=maxWeight;
                count++;
            }
        }
        return count>=days;
    }
    int shipWithinDays(vector<int>& weights, int days) {
        int len=weights.size();
        int left=0,right=0;
        for(int i=0;i<len;i++){
            left=max(left,weights[i]);
            right+=weights[i];
        }
        while(left<=right){
            int mid=left+(right-left)/2;
            if(isLeft(weights,days,mid))
                left=mid+1;
            else
                right=mid-1;
        } 
        return left;  
    }
};
```



####  [167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/) 

**题目描述**

给你一个下标从 1 开始的整数数组 numbers ，该数组已按 非递减顺序排列  ，请你从数组中找出满足相加之和等于目标数 target 的两个数。如果设这两个数分别是· numbers`[index1]`和 `numbers[index2]` ，则 `1 <= index1 < index2 <= numbers.length` 。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int left=0,right=numbers.size()-1;
        vector<int> ans(2);
        while(left<right)
        {
            int sum=numbers[left]+numbers[right];
            if(sum<target)
                left++;
            else if(sum>target)
                right--;
            else
            {
                ans[0]=left+1;
                ans[1]=right+1;
                return ans;
            }
        }
        return ans;
    }
};
```



####  [26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/) 

**题目描述**

 给你一个 **升序排列** 的数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。 

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int slow=0,fast=0;
        while(fast<nums.size()-1)
        {
            if(nums[fast]!=nums[slow])
            {
                slow++;
                nums[slow]=nums[fast];
            }
            fast++;
        }
        return slow+1;
    }
};
```



####  [27. 移除元素](https://leetcode.cn/problems/remove-element/) 

**题目描述**

 给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。 

**题解**

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow=0,fast=0;
        while(fast<nums.size())
        {
            if(nums[fast]!=val)
            {
                nums[slow]=nums[fast];
                slow++;
            }
            fast++;
        }
        return slow;
    }
};
```



####  [283. 移动零](https://leetcode.cn/problems/move-zeroes/) 

**题目描述**

 给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。 

**题解**

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int slow=0,fast=0;
        while(fast<nums.size())
        {
            if(nums[fast]!=0)
            {
                nums[slow]=nums[fast];
                slow++;
            }
            fast++;
        }
        while(slow<nums.size())
        {
            nums[slow]=0;
            slow++;
        }
    }
};
```



####  [344. 反转字符串](https://leetcode.cn/problems/reverse-string/) 

**题目描述**

 编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。 

**题解**

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int left=0,right=s.size()-1;
        while(left<right)
        {
            int temp=s[left];
            s[left]=s[right];
            s[right]=temp;
            left++;
            right--;
        }
    }
};
```



####   [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/) 

**题目描述**

 给你一个字符串 `s`，找到 `s` 中最长的回文子串。 

**题解**

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        string ans="";
        for(int i=0;i<s.size();i++)
        {
            string s1=longest(s,i,i);
            string s2=longest(s,i,i+1);
            ans=ans.size()>s1.size()?ans:s1;
            ans=ans.size()>s2.size()?ans:s2;
        }
        return ans;
    }
    string longest(string s,int l,int r)
    {
        string ans="";
        while(l>=0&&r<s.size())
        {
            if(s[l]!=s[r])
            {
                ans=s.substr(l+1,r-l-1);
                return ans;
            } 
            l--;
            r++;
        }
        ans=s.substr(l+1,r-l-1);
        return ans;
    }
};
```



####  [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/) 

**题目描述**

 给你一个链表的头节点 `head` ，判断链表中是否有环。 

**题解**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *slow = head,*fast = head;
        while(fast != NULL && fast->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
            if(slow==fast)
                return true;
        }
        return false;
    }
};
```



####  [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/) 

**题目描述**

 给定一个链表的头节点  `head` ，返回链表开始入环的第一个节点。 *如果链表无环，则返回 `null`。* 

**题解**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head,*fast = head;
        while(fast != NULL && fast->next != NULL)
        {
            slow = slow->next;
            fast = fast->next->next;
            if(fast==slow)
                break;
        }
        if(fast==NULL || fast->next==NULL)
            return NULL;
        slow=head;
        while(slow!=fast)
        {
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
};
```



#### [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/) 

**题目描述**

 给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。 

**题解**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *p=headA,*q=headB;
        while(p!=q)
        {
            if(p==NULL)
                p=headB;
            else
                p=p->next;
            if(q==NULL)
                q=headA;
            else
                q=q->next;
        }
        return p;
    }
};
```



####  [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/) 

**题目描述**

 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。 

**题解**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* findNode(ListNode* head,int n){
        ListNode *fast=head,*slow=head;
        for(int i=0;i<n;i++)
            fast=fast->next;
        while(fast!=NULL)
        {
            fast=fast->next;
            slow=slow->next;
        }
        return slow;
    }
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummy=(ListNode *)malloc(sizeof(ListNode));
        dummy->next = head;
        ListNode *x = findNode(dummy,n+1);
        x->next = x->next->next;
        return dummy->next;
    }
};
```



####  [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/) 

**题目描述**

 将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。  

**题解**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *p1=list1,*p2=list2;
        ListNode* p=new ListNode();
        ListNode* dummy=p;
        p->next=list1;
        while(p1!=NULL&&p2!=NULL)
        {
            if(p1->val<p2->val)
            {
                p->next=p1;
                p1=p1->next;
            }
            else
            {
                p->next=p2;
                p2=p2->next;
            }
            p=p->next;
        }
        if(p1==NULL)
            p->next=p2;
        else
            p->next=p1;
        return dummy->next;
    }
};
```



####   [23. 合并K个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/) 

**题目描述**

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

**题解**

```c++
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists.length==0) return null;
        ListNode dummy=new ListNode();
        ListNode p=dummy;
        
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.length,(x,y)->(x.val-y.val));
        for(ListNode head:lists)
        {
            if(head!=null)
            {
                pq.add(head);
            }
        }
        while(!pq.isEmpty())
        {
            ListNode node=pq.poll();
            if(node.next!=null)
                pq.add(node.next);
            p.next=node;
            p=p.next;
        }
        return dummy.next;
    }
}
```



## 二叉树

### 归并排序

 [912. 排序数组](https://leetcode.cn/problems/sort-an-array/) 

**题目描述**

 给你一个整数数组 `nums`，请你将该数组升序排列。 

**题解**

```c++
class Solution {
public:
    //用于辅助合并有序数组
    vector<int> temp;
    vector<int> sortArray(vector<int>& nums) {
        int len = nums.size();
        temp = vector<int> (len);   //初始化辅助数组
        sort(nums,0,len-1);     //排序整个数组
        return nums;
    }
    void sort(vector<int>& nums,int lo,int hi){
        //单个元素不用排序
        if(lo==hi) return;  
        int mid = lo+(hi-lo)/2;
        //先对左半部分数组nums[lo..mid]排序
        sort(nums,lo,mid);  
        //再对右半部分数组nums[mid+1..hi]排序
        sort(nums,mid+1,hi);
        //将两部分有序数组合并成一个有序数组
        merge(nums,lo,mid,hi);
    }
    // 将 nums[lo..mid] 和 nums[mid+1..hi] 这两个有序数组合并成一个有序数组
    void merge(vector<int>& nums,int lo,int mid,int hi){
        //将nums数组需要排序的部分暂存进辅助数组
        for(int i=lo;i<=hi;i++){
            temp[i] = nums[i];
        }
        int i = lo,j = mid+1;
        for(int p=lo;p<=hi;p++){
            //左半边数组已全部被合并
            if(i==mid+1) nums[p] = temp[j++];
            //右半边数组已全部被合并
            else if(j==hi+1) nums[p] = temp[i++];
            //较小元素先进入数组
            else if(temp[i]<=temp[j]) nums[p] = temp[i++];
            else nums[p] = temp[j++];
        }
    }
};
```



 [493. 翻转对](https://leetcode.cn/problems/reverse-pairs/) 

**题目描述**

给定一个数组 nums ，如果 i < j 且 nums[i] > 2*nums[j] 我们就将 (i, j) 称作一个重要翻转对。

你需要返回给定数组中的重要翻转对的数量。

**题解**

```c++
class Solution {
public:
    vector<int> temp;
    int count = 0;
    int reversePairs(vector<int>& nums) {
        int len = nums.size();
        temp = vector<int>(len);
        sort(nums,0,len-1);
        return count;
    }

    void sort(vector<int>& nums,int lo,int hi){
        if(lo==hi) return;
        int mid = lo+(hi-lo)/2;
        sort(nums,lo,mid);
        sort(nums,mid+1,hi);
        merge(nums,lo,mid,hi);
    }

    void merge(vector<int>& nums,int lo,int mid,int hi){
        for(int i=lo;i<=hi;i++) temp[i] = nums[i];
        int end = mid+1;
        for(int i=lo;i<=mid;i++){
            while(end<=hi&&(long)nums[i]>(long)nums[end]*2) end++;
            count+=end-mid-1;
        }
        int i=lo,j=mid+1;
        for(int p=lo;p<=hi;p++){
            if(i==mid+1) nums[p] = temp[j++];
            else if(j==hi+1) nums[p] = temp[i++];
            else if(temp[i]<=temp[j]) nums[p] = temp[i++];
            else nums[p] = temp[j++];
        }
    }
};
```



 [315. 计算右侧小于当前元素的个数](https://leetcode.cn/problems/count-of-smaller-numbers-after-self/) 

**题目描述**

给你一个整数数组 nums ，按要求返回一个新数组 counts 。数组 counts 有该性质： counts[i] 的值是  nums[i] 右侧小于 nums[i] 的元素的数量。

**题解**

```c++
class Solution {
public:
    typedef pair<int,int> pr;
    vector<int> count;
    vector<pr> temp;
    vector<int> countSmaller(vector<int>& nums) {
        int len = nums.size();
        count = vector<int>(len,0);
        temp = vector<pr>(len);
        vector<pr> p(len);
        for(int i=0;i<len;i++) p[i] = pr(i,nums[i]);
        sort(p,0,len-1);
        return count;
    }
    
    void sort(vector<pr>& p,int lo,int hi){
        if(lo==hi) return;
        int mid = lo+(hi-lo)/2;
        sort(p,lo,mid);
        sort(p,mid+1,hi);
        merge(p,lo,mid,hi);
    }

    void merge(vector<pr>& p,int lo,int mid,int hi){
        for(int i=lo;i<=hi;i++) temp[i] = p[i];
        int i=lo,j=mid+1;
        for(int k=lo;k<=hi;k++){
            if(i==mid+1) p[k] = temp[j++];
            else if(j==hi+1){
                p[k] = temp[i++];
                //cout<<"t";
                count[p[k].first]+=j-1-mid;
                //cout<<count[p[k].first];
                //cout<<j-mid;
            } 
            else if(temp[i].second<=temp[j].second){
                p[k] = temp[i++];
                count[p[k].first]+=j-1-mid;
                //cout<<j-mid;
            } 
            else p[k] = temp[j++];
        }
    }
};
```



 [327. 区间和的个数](https://leetcode.cn/problems/count-of-range-sum/) 

**题目描述**

给你一个整数数组 nums 以及两个整数 lower 和 upper 。求数组中，值位于范围 [lower, upper] （包含 lower 和 upper）之内的 区间和的个数 。

区间和 S(i, j) 表示在 nums 中，位置从 i 到 j 的元素之和，包含 i 和 j (i ≤ j)。

**题解**

```c++
class Solution {
public:
    vector<long> presum;
    vector<long> temp;
    int count = 0;
    int lower,upper;
    int countRangeSum(vector<int>& nums, int lower, int upper) {
        int len = nums.size();
        presum = vector<long>(len+1,0);
        temp = vector<long>(len+1);
        this->lower = lower,this->upper = upper;
        for(int i=0;i<len;i++){
            presum[i+1] = presum[i] + nums[i];
        } 
        sort(presum,0,len);
        return count;
    }

    void sort(vector<long>& nums,int lo,int hi){
        if(lo==hi) return;
        int mid = lo+(hi-lo)/2;
        sort(nums,lo,mid);
        sort(nums,mid+1,hi);
        merge(nums,lo,mid,hi);
    }

    void merge(vector<long>& nums,int lo,int mid,int hi){
        for(int i=lo;i<=hi;i++) temp[i] = nums[i];
        int start = mid+1,end = mid+1;
        for(int i=lo;i<=mid;i++){
            while(start<=hi&&presum[start]-presum[i]<lower) start++;
            while(end<=hi&&presum[end]-presum[i]<=upper){
                end++;
            } 
            count+=end-start;
        }
        int i=lo,j=mid+1;
        for(int p=lo;p<=hi;p++){
            if(i==mid+1) nums[p] = temp[j++];
            else if(j==hi+1) nums[p] = temp[i++];
            else if(temp[i]<=temp[j]) nums[p] = temp[i++];
            else nums[p] = temp[j++];
        }
    }
};
```



 [1038. 从二叉搜索树到更大和树](https://leetcode.cn/problems/binary-search-tree-to-greater-sum-tree/) 

**题目描述**

 给定一个二叉搜索树 `root` (BST)，请将它的每个节点的值替换成树中大于或者等于该节点值的所有节点值之和。 

**题解**

```c++
class Solution {
public:
    int sum = 0;
    TreeNode* bstToGst(TreeNode* root) {
        Traverse(root);
        return root;
    }
    /*从大到小开始遍历*/
    void Traverse(TreeNode* root){
        if(root==NULL) return;
        Traverse(root->right);
        sum+=root->val;     //中序遍历时每次将比自己大的值累加
        root->val = sum;
        Traverse(root->left);
    }
};
```



 [230. 二叉搜索树中第K小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/) 

给定一个二叉搜索树的根节点 `root` ，和一个整数 `k` ，请你设计一个算法查找其中第 `k` 个最小元素（从 1 开始计数）。

**题解**

```c++
class Solution {
public:
    int k,ans,rank=0;
    int kthSmallest(TreeNode* root, int k) {
        this->k = k;
        Traverse(root);
        return ans;
    }
    
    void Traverse(TreeNode* root){
        if(root==NULL) return;
        Traverse(root->left);
        rank++;
        if(rank==k){
            ans=root->val;
            return;
        }
        Traverse(root->right);
    }
};
```



模板

**题目描述**



**题解**

```c++

```



模板

**题目描述**



**题解**

```c++

```



模板

**题目描述**



**题解**

```c++

```

















