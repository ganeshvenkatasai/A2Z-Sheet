
# Array

Left rotate an array by D places

```
void rotate(vector<int>& nums, int k) {
    k=k%nums.size();
    reverse(nums.begin(),nums.end());
    reverse(nums.begin(),nums.begin()+k);
    reverse(nums.begin()+k,nums.end());
}
```

Find missing number in an array

```
int missingNumber(vector<int>& nums) {
    int sum=0,n=nums.size();
    for(int i=0;i<n;i++){
        sum+=nums[i];
    }
    return ((n*(n+1))/2)-sum;
}
```
```
int missingNumber(vector<int>& a) {
    int n=a.size(),x=n;
    for(int i=0;i<n;i++) x^=i^a[i];
    return x;
}
```
Maximum Consecutive Ones

```
int findMaxConsecutiveOnes(vector<int>& a) {
    int c=0,r=0;
    for(auto it:a){
        if(it==0) r=max(r,c),c=0;
        else c++;
    }
    r=max(r,c);
    return r;
}
```
Element appears twice except one
```
int singleNumber(vector<int>& a) {
    int r=0;
    for(auto it:a) r=r^it;
    return r;
}
```
Longest Subarray with given Sum K (Positives)

```
int longestSubarrayWithSumK(vector<int> a, long long k) {
    int ma=0,l=0,r=0,n=a.size();
    long long s=a[0];
    while(r<n){
        while(l<=r && s>k){
            s-=a[l++];
        }
        if(s==k) ma=max(ma,r-l+1);
        r++;
        if(r<n){
           s+=a[r];
        }
    }
    return ma;
}
```
Longest Subarray with sum K (Postives and Negatives)
```
int getLongestSubarray(vector<int>& a, int k){
    unordered_map<int,int> mp;
    int s=0,ma=0;
    mp[0]=-1;
    for(int i=0;i<a.size();i++){
        s+=a[i];
        if(mp.find(s-k)!=mp.end()) ma=max(ma,i-mp[s-k]);
        if(mp.find(s)==mp.end()) mp[s]=i;
    }
    return ma;
}
```
Two Sum
```
vector<int> twoSum(vector<int>& a, int t) {
        vector<int> res;
    unordered_map<int,int> mp; 
    for(int i=0;i<a.size();i++){
        if(mp.find(t-a[i])!=mp.end()){
            res.push_back(i);
            res.push_back(mp[t-a[i]]);
        }
        mp[a[i]]=i;
    }
    return res;
}
```
Sort an array of 0s, 1s and 2s
```
void sortColors(vector<int>& a) {
    int n=a.size();
    int z=0,o=0,t=n-1;
    while(o<=t){
        if(a[o]==0) swap(a[z++],a[o++]);
        else if(a[o]==2) swap(a[t--],a[o]);
        else o++;
    }
}
```
Majority Element (>n/2 times)
```
int majorityElement(vector<int>& a) {
    int v=INT_MAX,c=0;
    for(auto it:a){
        if(it==v) c++;
        else{
            if(!c) v=it;
            else c--;
        }
    }
    return v;
}
```
Majority Element (n/3 times)
```
vector<int> majorityElement(vector<int>& nums) {
    int num1=-1,num2=-1,count1=0,count2=0;
    for(auto it:nums){
        if(it==num1) count1++;
        else if(it==num2) count2++;
        else if(!count1) {num1=it;count1=1;}
        else if(!count2) {num2=it;count2=1;}
        else {count1--;count2--;}
    }
    count1=0,count2=0;
    for(auto it:nums){
        if(it==num1) count1++;
        else if(it==num2) count2++;
    }
    vector<int> res;
    if(count1>(nums.size()/3)) res.push_back(num1);
    if(count2>(nums.size()/3)) res.push_back(num2);
    return res;
}
```
Kadane's Algorithm
```
int maxSubArray(vector<int>& a) {
    int sum=0,ans=INT_MIN;
    for(auto it:a){
        sum+=it;
        ans=max(ans,sum);
        if(sum<0) sum=0;
    }
    return ans;
}
```
Stock Buy and Sell
```
int maxProfit(vector<int>& a) {
    int mi=a[0],ma=a[0],ans=INT_MIN;
    for(int i=0;i<a.size();i++){
        if(a[i]<mi) mi=ma=a[i];
        if(a[i]>ma) ma=a[i];
        ans=max(ans,ma-mi);
    }
    return ans;
}
```
Rearrange Array Elements by Sign
```
vector<int> rearrangeArray(vector<int>& nums) {
    vector<int> ans(nums.size(),0);
    int a=0,b=1;
    for(int i=0;i<nums.size();i++){
        if(nums[i]>=0){
            ans[a]=nums[i];
            a+=2;
        }
        else{
            ans[b]=nums[i];
            b+=2;
        }
    }
    return ans;
}
```
Next Permutation
```
void nextPermutation(vector<int>& nums) {
    int i;
    for(i=nums.size()-2;i>=0;i--) if(nums[i]<nums[i+1]) break;   
    if(i<0) reverse(nums.begin(),nums.end());
    else{
        int l;
        for(l=nums.size()-1;l>i;l--) if(nums[l]>nums[i]) break;
        swap(nums[i],nums[l]);
        reverse(nums.begin()+i+1,nums.end());
    }
}
```
Longest Consecutive Sequence
```
int longestConsecutive(vector<int>& nums) {
    unordered_set<int> s(nums.begin(),nums.end());
    int res=0;
    for(auto i:nums){
        if(s.find(i)==s.end()) continue;
        s.erase(i);
        int p=i-1,n=i+1;
        while(s.find(p)!=s.end()) s.erase(p--);
        while(s.find(n)!=s.end()) s.erase(n++);
        res=max(res,n-p-1);
    }
    return res;
}
```
Set Matrix Zeroes
```
void setZeroes(vector<vector<int>>& m) {
    int r=m.size(),c=m[0].size();
    int row=1;
    for(int i=0;i<c;i++) if(m[0][i]==0) row=0;
    for(int i=0;i<r;i++) if(m[i][0]==0) m[0][0]=0;
    for(int i=1;i<r;i++){
        for(int j=0;j<c;j++){
            if(i==0 && j==0) continue;
            if(m[i][j]==0){
                m[0][j]=0;
                m[i][0]=0;
            }
        }
    }
    for(int i=1;i<r;i++){
        for(int j=1;j<c;j++){
            if(m[0][j]==0 || m[i][0]==0){
                m[i][j]=0;
            }
        }
    }
    for(int i=1;i<c;i++) if(row==0) m[0][i]=0;
    for(int i=0;i<r;i++) if(m[0][0]==0) m[i][0]=0;
    if(row==0) m[0][0]=0;
}
```
Rotate Matrix
```
void rotate(vector<vector<int>>& a) {
    int n=a.size();
    for(int i=1;i<n;i++) for(int j=0;j<i;j++) swap(a[i][j],a[j][i]);
    for(int i=0;i<n;i++) reverse(a[i].begin(),a[i].end());
}
```
Spiral Matrix
```
vector<int> spiralOrder(vector<vector<int>>& m) {
    vector<int> v;
    int x1=0,y1=0,x2=0,y2=m[0].size()-1,x3=m.size()-1,y3=m[0].size()-1,x4=m.size()-1,y4=0;
    while(x1<=x4 && y1<=y2){
        if(x1==x4){
            for(int i=y1;i<=y2;i++) v.push_back(m[x1][i]);
        }
        else if(y1==y2){
            for(int i=x1;i<=x4;i++) v.push_back(m[i][y1]);
        }
        else{
        for(int i=y1;i<y2;i++) v.push_back(m[x1][i]);
        for(int i=x2;i<x3;i++) v.push_back(m[i][y2]);
        for(int i=y3;i>y4;i--) v.push_back(m[x3][i]);
        for(int i=x4;i>x1;i--) v.push_back(m[i][y4]);
        }
        x1++,y1++,x2++,y2--,x3--,y3--,x4--,y4++;
    }
    return v;
}
```
Count subarrays with given sum
```
int subarraySum(vector<int>& a, int t) {
    int s=0,c=0;
    unordered_map<int,int> mp;
    mp[0]++;
    for(auto it:a){
        s+=it;
        c+=mp[s-t];
        mp[s]++;
    }
    return c;
}
```
Pascal's Triangle
```
vector<vector<int>> generate(int n) {
    vector<vector<int>> ans(n);
    ans[0].push_back(1);
    if(n==1) return ans;
    ans[1].push_back(1);
    ans[1].push_back(1);
    if(n==2) return ans;
    for(int i=2;i<n;i++){
        ans[i].push_back(1);
        for(int j=1;j<i;j++){
            ans[i].push_back(ans[i-1][j-1]+ans[i-1][j]);
        }
        ans[i].push_back(1);
    }
    return ans;
}
```
3 Sum
```
vector<vector<int>> threeSum(vector<int>& a) {
    vector<vector<int>> ans;
    int n=a.size();
    sort(a.begin(),a.end());
    for(int i=0;i<=n-3;i++){
        if(i>0 && a[i]==a[i-1]) continue;
        int j=i+1,k=n-1;
        while(j<k){
            if(a[i]+a[j]+a[k]==0){
                ans.push_back({a[i],a[j],a[k]});
                while (j<k && a[j]==a[j+1]) j++;
                while (j<k && a[k]==a[k-1]) k--;
                j++;k--;
            }
            else if(a[i]+a[j]+a[k]>0) k--;
            else j++;
        }
    }
    return ans;
}
```
4 Sum
```
vector<vector<int>> fourSum(vector<int>& a, int t) {
    sort(a.begin(),a.end());
    set<vector<int>> ans;
    vector<vector<int>> res;
    long long int v;
    if(a.size()<4) return res;
    for(int i=0;i<a.size()-3;i++){
        for(int j=i+1;j<a.size()-2;j++){
            int l=j+1,h=a.size()-1;
            while(l<h){
                v=a[i],v+=a[j],v+=a[l],v+=a[h];
                if(v<t) l++;
                else if(v>t) h--;
                else ans.insert({a[i],a[j],a[l++],a[h--]});
            } 
        }
    }
    for(auto it:ans) res.push_back(it);
    return  res;
}
```
Count subarrays with given XOR
```
int subarraysWithXorK(vector<int> a, int k) {
    int n = a.size(); 
    int xr = 0;
    map<int, int> mp; 
    mp[xr]++; 
    int c = 0;
    for (int i = 0; i < n; i++) {
        xr = xr ^ a[i];
        int x = xr ^ k;
        c+= mp[x];
        mp[xr]++;
    }
    return c;
}
```
Merge Overlapping Subintervals
```
vector<vector<int>> merge(vector<vector<int>>& a) {
    sort(a.begin(),a.end());
    int start=a[0][0],end=a[0][1];
    vector<vector<int>> res;
    for(int i=0;i<a.size();i++){
        if(end>=a[i][0]) end=max(end,a[i][1]);
        else{
            res.push_back({start,end});
            start=a[i][0];
            end=a[i][1];
        }
    }
    res.push_back({start,end});
    return res;
}
```
Merge Sorted Arrays Without Extra Space
```
void merge(vector<int>& a1, int m, vector<int>& a2, int n) {
    int i=m-1,j=n-1,k=m+n-1;
    while(i>=0 && j>=0){
        if(a2[j]>a1[i]) a1[k--]=a2[j--];
        else a1[k--]=a1[i--];
    }
    while(j>=0) a1[k--]=a2[j--];
}
```

