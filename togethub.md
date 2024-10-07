# 2024.9.26刷题
## 题目1：
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。
## 代码实现：
```C++
vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> mymap;  //定义一个map，用来存放遍历过的元素
        int i;
        for(i = 0;i < nums.size();i++)
        {
            //遍历元素，如果该元素在map中存在相应的元素相加之和等于目标值，则返回俩下标
            int s = target - nums[i];          //s是当前数组中元素所需要组成目标值的数
            auto iter = mymap.find(s);         //使用迭代器寻找元素
            if(iter != mymap.end())
            {
                return {iter->second,i};
            }
            else
            mymap.insert({nums[i],i});   //如果没找到，将该元素放入map
        }
        return {};
    }
```
# 积累
## 题目1：
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。  
假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：  
更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。  
返回 k。

```C++
int removeElement(vector<int>& nums, int val) {
        //双指针
        //快指针负责遍历数组，每有一个不等于val的数，则将其更新至slow指针；若等于val，则不更新slow指针；
        int fast,slow;
        slow = 0;
        for(fast = 0;fast < nums.size();fast++)
        {
            if(nums[fast] != val)
            {
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
```
## 题目2：
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。
```C++
int search(vector<int>& nums, int target) {
    //二分查找
    int left = 0;
    int right = nums.size() -1;
    int middle;
    while(left <= right)              //左闭右闭
    {
        middle = (left + right) / 2;  //找到中间值
        if(nums[middle] < target)    //如果中间值比目标值小，说明目标值在该值右边，所以将左指针调整为中间值加1
        {
            left = middle + 1;
        }
        else if(nums[middle] > target)
        {
            right = middle - 1;
        }
        else
        {
            return middle;
        }
    }
    return -1;
    }
```