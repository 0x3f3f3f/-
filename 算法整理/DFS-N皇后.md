# DFS-N皇后

![image-20220721212241404](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220721212241404.png)



![image-20220721215724881](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220721215724881.png)

+ https://www.acwing.com/solution/content/2820/
+ 二维回溯法应用,默认传入x，x从0一直到n - 1，遍历完成就是一个结果，还要进行回溯，因为答案可能不只一个。
+ 分析斜对角线和反斜对角线，\ 反斜对角线是y - x + n, / 斜对角线是x + y
+ **所有的标记数组都是从0开始的，原因就是x和y 牵扯到结果tmp，这个tmp的x，y都是从0算。**
+ 注意斜线标记数组和反斜线标记数组大小都是2 * n + 1。
+ 时间复杂度为O(n!)，直接暴力则是O(2^(N^2))

