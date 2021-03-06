[C++ template for ALL Combination Problem Set](https://leetcode.com/problems/combination-sum-iv/discuss/85120/C++-template-for-ALL-Combination-Problem-Set)<br>

6/29 [77. Combinations]()给定n和k，返回1-n中所有k个不同数的组合。<br》
是一个类似的题目。<br>
6/29 [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/description/)<br>
从1-9中找出k个不相同的数，使得和为n。
```
List<List<Integer>> res = new  ArrayList<List<Integer>>();
int len;
List<Integer> list = new ArrayList<>();
public List<List<Integer>> combinationSum3(int k, int n) {
    dfs(1, k, n);
    return res;
}
public void dfs(int index, int cnt, int sum){//index equals element
    if(cnt==0 && sum==0) {
        List<Integer> tmp = new ArrayList<>(list);
        res.add(tmp); return;
    }
    for(int i=index; i<=9; ++i){
        list.add(i);
        if(cnt-1>=0 && sum-i>=0) dfs(i+1, cnt-1, sum-i);
        list.remove(list.size()-1);
    }
    return;
}
```

6/29 [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)<br>
给定一个包含重复元素的数组，找出能组合成指定值的相异的组合方式。不重复7=[1,1,5]=[3,4]
```
List<List<Integer>> ans = new ArrayList<>();
List<Integer> list = new ArrayList<>();
public List<List<Integer>> combinationSum2(int[] c, int t) {
    Arrays.sort(c);
    int len = c.length;
    dfs(c, t, 0);
    return ans;
}
public void dfs(int [] c, int sum, int index){
    if(sum==0){
        List<Integer> tmp = new ArrayList<>();
        for(int ele: list){
            tmp.add(ele); 
        }
        ans.add(tmp); return;
    }
    for(int i=index;i<c.length; ++i){
        if(i>index && c[i] == c[i-1]) continue;
		//关键在于这一行，可以去重。
        if(sum-c[i]>=0){
            list.add(c[i]);
            dfs(c, sum-c[i], i+1);
            list.remove(list.size()-1);
        }
    }
    return;
}
```

5/27 [39. Combination Sum](https://leetcode.com/problems/combination-sum/description/)<br>
给定一个元素互不相同的数组以及一个目标值，要求返回一个list<list<>>，存放着所有不同的组合方式。元素可重复使用多次。112和121算相同组合。
```
List<List<Integer>> ans = new ArrayList<>();
List<Integer> list = new ArrayList<>();
public List<List<Integer>> combinationSum(int[] c, int t) {
    int len = c.length;
    dfs(c, t, 0);
    return ans;
}
public void dfs(int [] c, int t, int index){
    if(t==0){
        ans.add(new ArrayList<>(list)); return;
    }
    for(int i=index;i<c.length; ++i){
        if(t-c[i]>=0){
            list.add(c[i]);
            dfs(c, t-c[i], i);
            list.remove(list.size()-1);
        }
    }
    return;
}
```

5/27 [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/)<br>
给定总的小括号数，问能生成多少个合法的括号串。典型回溯<br>
n=3,["((()))","(()())","(())()","()(())","()()()"]<br>
令left right为左右括号剩余数。每增加一个括号，就相应地减掉1.但要注意一个点，能减到多少？
```
private List<String> ans = new ArrayList<>();
public List<String> generateParenthesis(int n) {
    int left=n, right=n;
    String s="";
    dfs(s, left, right);
    return ans;
}
void dfs(String s, int l, int r){
    if(l==0&&r==0){
        ans.add(s); return;
    }
    if(l>0) dfs(s+'(', l-1, r); 
    if(l<r) dfs(s+')', l, r-1);
    return;
}
```
减到0为止。