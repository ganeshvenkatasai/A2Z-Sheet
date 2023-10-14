
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
Find the repeating and missing numbers
```
```

Count inversions
```
int merge(vector<int> &arr, int low, int mid, int high) {
    vector<int> temp;
    int left = low;
    int right = mid + 1;
    int cnt = 0;
    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left]);
            left++;
        }
        else {
            temp.push_back(arr[right]);
            cnt += (mid - left + 1); //Modification 2
            right++;
        }
    }
    while (left <= mid) temp.push_back(arr[left++]);
    while (right <= high) temp.push_back(arr[right++]);
    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
    return cnt; 
}

int mergeSort(vector<int> &arr, int low, int high) {
    int cnt = 0;
    if (low >= high) return cnt;
    int mid = (low + high) / 2 ;
    cnt += mergeSort(arr, low, mid);
    cnt += mergeSort(arr, mid + 1, high);
    cnt += merge(arr, low, mid, high);
    return cnt;
}
```

Reverse Pairs
```
int merge(vector<int>& arr,int l,int m,int r){
    int i=l,j,count=0;
    for(j=m+1;j<=r;j++){
        while(i<=m && arr[i]<=2LL*arr[j]) i++;
        count+=(m+1-i);
    }
    int d[r-l+1];
    i=l,j=m+1;
    int k=0;
    while(i<=m && j<=r){
        if(arr[i]<=arr[j]) d[k++]=arr[i++];
        else d[k++]=arr[j++];
    }
    while(i<=m) d[k++]=arr[i++];
    while(j<=r) d[k++]=arr[j++];
    k=0;
    for(int i=l;i<=r;i++) arr[i]=d[k++];
    return count;
}

int mergeSort(vector<int>& arr,int l,int r){
    if(l==r) return 0;
    int count=0;
    int m=l+(r-l)/2;
    count+=mergeSort(arr,l,m);
    count+=mergeSort(arr,m+1,r);
    count+=merge(arr,l,m,r);
    return count;
}
```
Maximum Product Subarray
```
int maxProduct(vector<int>& a) {
    int mi=1,ma=1,v,r=INT_MIN;
    for(auto it:a){
        v=max({it,it*mi,it*ma});
        mi=min({it,it*mi,it*ma});
        ma=v;
        r=max(r,ma);
    }
    return r;
}
```

# Binary Search

Search an Element

```
int search(vector<int>& a, int t) {
    int l=0,r=a.size()-1,m;
    while(l<=r){
        m=(l+r)/2;
        if(a[m]<t) l=m+1;
        else if(a[m]>t) r=m-1;
        else return m;
    }
    return -1;
}
```
Lower Bound 
```
int lowerBound(vector<int> arr, int n, int x) {
    int low = 0, high = n - 1;
    int ans = n;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] >= x)  ans = mid, high = mid - 1;
        else low = mid + 1;
    }
    return ans;
}
```
Upper Bound
```
int upperBound(vector<int> &arr, int x, int n) {
    int low = 0, high = n - 1;
    int ans = n;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] > x) ans = mid, high = mid - 1;
        else low = mid + 1;
    }
    return ans;
}
```
Floor and Ceil
```
int findFloor(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int ans = -1;
	while (low <= high) {
		int mid = (low + high) / 2;
		if (arr[mid] <= x) ans = arr[mid], low = mid + 1;
		else high = mid - 1;
	}
	return ans;
}

int findCeil(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int ans = -1;
	while (low <= high) {
		int mid = (low + high) / 2;
		if (arr[mid] >= x) ans = arr[mid], high = mid - 1;
		else low = mid + 1;
	}
	return ans;
}
```
First and Last Occurance
```
int firstOccurance(vector<int>& a, int t){
    int ans = -1, low = 0, high = a.size()-1, mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if(a[mid] >= t) ans = mid, high = mid - 1;
        else low = mid + 1;
    }
    return ans;
}

int lastOccurance(vector<int>& a, int t){
    int ans = -1, low = 0, high = a.size()-1, mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if(a[mid] <= t) ans = mid, low = mid + 1;
        else high = mid - 1;
    }
    return ans;
}
```
Search in Rotated Sorted Array (Unique values)

```
int search(vector<int>& arr, int k) {
    int low = 0, high = arr.size() - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == k) return mid;
        if (arr[low] <= arr[mid]) {
            if (arr[low] <= k && k < arr[mid]) high = mid - 1;
            else low = mid + 1;
        }
        else { 
            if (arr[mid] < k && k <= arr[high]) low = mid + 1;
            else high = mid - 1;
        }
    }
    return -1;
}
```
Search in Rotated Sorted Array (Duplicate values)
```
bool search(vector<int>&arr, int k) {
    int n = arr.size(); 
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == k) return true;
        if (arr[low] == arr[mid] && arr[mid] == arr[high]) {
            low = low + 1;
            high = high - 1;
        }
        else if (arr[low] <= arr[mid]) {
            if (arr[low] <= k && k < arr[mid]) {
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        else { 
            if (arr[mid] < k && k <= arr[high]) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
    }
    return false;
}
```
Minimum in Rotated Sorted Array

```
int findMin(vector<int>& a) {
    int low = 0, high = a.size()-1, mid;
    while (low < high) {
        mid = (low + high) / 2;
        if (a[mid] > a[mid + 1]) return a[mid + 1];
        else if (a[low] < a[mid]) low = mid + 1;
        else high = mid;
    }
    return a[0];
}
```
Single element in a Sorted Array
```
int singleNonDuplicate(vector<int>& a) {
    if(a.size()==1 || a[0]!=a[1]) return a[0];
    if(a[a.size()-1] != a[a.size()-2]) return a[a.size()-1];
    int l=0,r=a.size()-1,m;
    while(l<=r){
        m=(l+r)/2;
        if(a[m-1]!=a[m] && a[m]!=a[m+1]) return a[m];
        else if((m%2==0 && a[m]==a[m+1])  || (m%2!=0 && a[m]==a[m-1])) l=m+1;
        else r=m-1;
    }
    return r;
}
```
Find Peak Element
```
int findPeakElement(vector<int>& a) {
    int n=a.size();
    if(n==1) return 0;
    if(a[0]>a[1]) return 0;
    if(a[n-1]>a[n-2]) return n-1;
    int l=1,r=n-2,m;
    while(l<=r){
        m=(l+r)/2;
        if(a[m-1]<a[m] && a[m]>a[m+1]) return m;
        else if(a[m-1]<a[m]) l=m+1;
        else r=m-1;
    }
    return -1;
}
```
Koko Eating Bananas
```
int minEatingSpeed(vector<int>& a, int h) {
    if(h<a.size()) return -1;
    int l=1,r=*max_element(a.begin(),a.end()),m;
    long long c=0;
    while(l<=r){
        m=(l+r)/2;
        c=0;
        for(int i=0;i<a.size();i++){
            c+=(a[i]/m);
            if(a[i]%m) c++;
        }
        if(c>h) l=m+1;
        else r=m-1;
    }
    return l;
}
```
Minimum Days to Make m Bouquets
```
int minDays(vector<int>& a, int b, int k) {
    if(a.size()/b<k) return -1;
    int l=0,r=*max_element(a.begin(),a.end()),m,c,v;
    while(l<=r){
        m=(l+r)/2;
        c=0;
        v=0;
        for(int i=0;i<a.size();i++){
            if(c==k){
                v++;
                c=0;
            } 
            if(a[i]<=m) c++;
            else c=0;
        }
        if(c==k) v++;
        if(v<b) l=m+1;
        else r=m-1;
    }
    return l;
}
```
Capacity To Ship Packages 
```
int shipWithinDays(vector<int>& a, int d) {
    int l=*max_element(a.begin(),a.end()),r=accumulate(a.begin(),a.end(),0),m,s,c;
    while(l<=r){
        m=(l+r)/2;
        s=0;
        c=1;
        for(auto it:a){
            s+=it;
            if(s>m){
                c++;
                s=it;
            }
        }
        if(c>d) l=m+1;
        else r=m-1;
    }
    return l;
}
```
Kth Missing Positive Number

```
int findKthPositive(vector<int>& a, int k) {
    int l=0,r=a.size()-1,m;
    while(l<=r){
        m=(l+r)/2;
        if(a[m]-m-1<k) l=m+1;
        else r=m-1;
    }
    return k+l;
}
```
Aggressive cows
```
bool canWePlace(vector<int> &stalls, int dist, int cows) {
    int n = stalls.size();
    int cntCows = 1;
    int last = stalls[0];
    for (int i = 1; i < n; i++) {
        if (stalls[i] - last >= dist) {
            cntCows++; //place next cow.
            last = stalls[i];
        }
        if (cntCows >= cows) return true;
    }
    return false;
}
int aggressiveCows(vector<int> &stalls, int k) {
    int n = stalls.size();
    sort(stalls.begin(), stalls.end());
    int low = 1, high = stalls[n - 1] - stalls[0];
    while (low <= high) {
        int mid = (low + high) / 2;
        if (canWePlace(stalls, mid, k) == true) low = mid + 1;
        else high = mid - 1;
    }
    return high;
}
```
Book Allocation
```
bool canAllocate(vector<int>& arr, int m, int threshold){
    int students = 1;
    int pages = 0;
    for (int i = 0; i < arr.size(); i++) {
        if (pages + arr[i] <= threshold) {
            pages += arr[i];
        }
        else {
            pages = arr[i];
            students++;
        }
    }
    return students <= m;
}

int findPages(vector<int>& arr, int n, int m) {
    if(m>n) return -1;
    int low = *max_element(arr.begin(),arr.end());
    int high = accumulate(arr.begin(),arr.end(),0);
    while (low <= high) {
        int mid = (low + high) / 2;
        if(canAllocate(arr,m,mid)) high = mid - 1;
        else high = low = mid + 1;
    }
    return low;
}
```
Split Array Largest Sum
```
bool f(vector<int>& a, int m,int k){
    int c=1,s=0;
    for(int i=0;i<a.size();i++){
        if(s+a[i]<=m){
            s+=a[i];
        }
        else{
            s=a[i];
            c++;
        }
    }
    return c<=k;
}

int splitArray(vector<int>& a, int k) {
    int l=*max_element(a.begin(),a.end()),r=accumulate(a.begin(),a.end(),0),m;
    while(l<=r){
        m=(l+r)/2;
        if(f(a,m,k)) r=m-1;
        else l=m+1;
    }
    return l;
}
```
Painter’s Partition
```
int countPainters(vector<int> &boards, int time) {
    int n = boards.size();
    int painters = 1;
    long long boardsPainter = 0;
    for (int i = 0; i < n; i++) {
        if (boardsPainter + boards[i] <= time) {
            boardsPainter += boards[i];
        }
        else {
            painters++;
            boardsPainter = boards[i];
        }
    }
    return painters;
}

int findLargestMinDistance(vector<int> &boards, int k) {
    int low = *max_element(boards.begin(), boards.end());
    int high = accumulate(boards.begin(), boards.end(), 0);
    while (low <= high) {
        int mid = (low + high) / 2;
        int painters = countPainters(boards, mid);
        if (painters <= k) high = mid - 1;
        else low = mid + 1;
    }
    return low;
}
```
Minimize Max Distance to Gas Station
```
```
Median of 2 sorted arrays
```
```
Kth element of 2 sorted arrays
```
```
Row with max 1s
```
int countOnes(vector<int> &row){
    int low = 0, high = row.size()-1, mid;
    while(low <= high) {
        mid = (low + high) / 2;
        if(row[mid] < row[mid+1]) {
            return row.size()-mid-1;
        }
        else if(row[mid] == 0) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return row.size()-high-1;
}

int rowWithMax1s(vector<vector<int>> &matrix, int n, int m)
{
    int maxOnes = 0, maxOnesIndex = 0;
    for(int i = 0; i < n; i++) {
        if(matrix[i][0]==1 && maxOnes != m){
            maxOnes = m;
            maxOnesIndex = i;
        }
        else if(matrix[i][m-1]!=0){
            int rowOnes = countOnes(matrix[i]);
            if(rowOnes > maxOnes){
                maxOnes = rowOnes;
                maxOnesIndex = i;
            }
        }
    }
    return maxOnesIndex;
}
```
Search a 2D Matrix
```
bool searchMatrix(vector<vector<int>>& m, int t) {
    int r=m.size(),c=m[0].size(),l=0,h=r*c-1,mid,val;
    while(l<=h){
        mid=(l+h)/2;
        val=m[mid/c][mid%c];
        if(val==t) return true;
        else if(val<t) l=mid+1;
        else h=mid-1;
    }
    return false;
}
```
Search in a row and column wise sorted matrix
```
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int r=matrix.size(),c=matrix[0].size();
    int i=r-1,j=0;
    while(i>=0 && j<c){
        if(matrix[i][j]==target) return true;
        else if(matrix[i][j]<target) j++;
        else i--;
    }
    return false;
}
```
Find Peak Element (2D Matrix)
```
```
Matrix Median
```
```

# String

Remove Outermost Parentheses
```
string removeOuterParentheses(string s) {
    int c=0;
    string a;
    for(auto it:s){
        it=='('?c++:c--; 
        if((it!='(' || c!=1) && (it!=')' || c!=0)) a+=it;
    }
    return a;
}
```
Reverse Words in a String
```
string reverseWords(string s) {
    string t,a;
    for(auto it:s){
        if(it==' ') {if(t.size()) a=t+" "+a, t="";}
        else t+=it;
    }
    if(t.size()) a=t+" "+a;
    a.pop_back();
    return a;
}
```
Isomorphic String
```
bool isIsomorphic(string s, string t) {
    unordered_map<char,char> mp1,mp2;
    for(int i=0;i<s.size();i++){
        if(mp1.find(t[i])!=mp1.end()) if(mp1[t[i]]!=s[i]) return false;
        if(mp2.find(s[i])!=mp2.end()) if(mp2[s[i]]!=t[i]) return false;
        mp1[t[i]]=s[i];
        mp2[s[i]]=t[i];
    }
    return true;
}
```
One string is a rotation of another
```
```
Valid Anagram
```
bool isAnagram(string s, string t) {
    int freq[26]={0},c=0;
    for(int i=0;i<s.size();i++){
        freq[s[i]-'a']++;
        c++;
    }
    for(int i=0;i<t.size();i++){
        freq[t[i]-'a']--;
        if(freq[t[i]-'a']>=0) c--;
        else return false;
    }
    if(c) return false;
    return true;
}
```
Sort Characters By Frequency
```
static bool comp(pair<int,char> a,pair<int,char> b){
    if(a.first>b.first) return true;
    return false;
}

string frequencySort(string s) {
    unordered_map<char,int> mp;
    for(auto it:s) mp[it]++;
    vector<pair<int,char>> v;
    for(auto it:mp) v.push_back({it.second,it.first});
    sort(v.begin(),v.end(),comp);
    string a;
    for(int i=0;i<v.size();i++){
        while(v[i].first--) a+=v[i].second;
    }
    return a;
}
```
Max Nesting Depth of the Parentheses
```
int maxDepth(string s) {
    int c=0,a=0;
    for(auto it:s){
        if(it=='(') c++;
        if(it==')') c--;
        a=max(a,c);
    }
    return a;
}
```
Roman to Integer
```
int r2n(char c){
    int x;
    c=='I'? x=1:c=='V'?x=5:c=='X'?x=10:c=='L'x=50:c=='C'?x=100:c=='D'?x=500:c=='M'?x=1000:x=0;
    return x;
}

int romanToInt(string s) {
    int x,y,sum=0,i;
    for (i=0; i<s.size(); i++) {
        x=r2n(s[i]);
        i!=s.size()-1?y=r2n(s[i+1]):y=0;
        if(x>=y) sum+=x;
        else{
            sum+=(y-x);
            i++;
        }
    }
    return sum;
}
```
Integer to Roman
```
string intToRoman(int num) {
    string ans="";
    int i=0;
    vector<int> nums={1000,900,500,400,100,90,50,40,10,9,5,4,1};
    vector<string> roman={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
    while(num){
        if(num>=nums[i]){
            ans=ans+roman[i];
            num=num-nums[i];
        } 
        else{
            i++;
        }
    }
    return ans;
}
```
String to Integer
```
int myAtoi(string s) {
    int i=0,flag=1;
    int n=s.size();
    if(n==0) return 0;
    while(i<n && s[i]==' ') i++;
    if(i==n) return 0;
    if(s[i]=='-') flag=-1, i++;
    else if(s[i]=='+') i++;
    long int res=0;
    while(s[i]>='0' && s[i]<='9'){
        res=res*10;
        if(res>=INT_MAX || res<=INT_MIN) break;
        res=res+(s[i]-'0');
        i++;
    }
    if(flag==-1) res=res*flag;
    if(res<=INT_MIN) return INT_MIN;
    if(res>=INT_MAX) return INT_MAX;
    return res;
}
```
Count Number of Substrings
```
```
Longest Palindromic Substring
```
string longestPalindrome(string s) {
    vector<vector<bool>> dp(s.size(),vector<bool>(s.size(),false));
    int l=0,r=0;
    for(int i=0;i<s.size();i++){
        for(int j=0;j<s.size()-i;j++){
            if(i==0) dp[j][j]=true;
            else if(i==1 && s[j]==s[j+1]) dp[j][j+1]=true, l=j, r=j+i;
            else if(s[j]==s[j+i] && dp[j+1][j+i-1]){ dp[j][j+i]=true; if(i+1>r-l+1) l=j, r=j+i;}
        }
    }
    return s.substr(l,r-l+1);
}
```
Sum of Beauty of All Substrings

```
int beautySum(string s) {
    if(s.size()<3) return 0;
    vector<vector<int>> v(26,vector<int>(s.size()));
    v[s[0]-'a'][0]=1;
    for(int j=1;j<s.size();j++){
        for(int i=0;i<26;i++) v[i][j]=v[i][j-1];
        v[s[j]-'a'][j]++;
    }

    int a=0,mi,ma;
    for(int i=0;i<s.size()-2;i++){
        for(int j=i+2;j<s.size();j++){
            mi=501,ma=0;
            for(int k=0;k<26;k++){
                if(!v[k][j] || (i>0 && !(v[k][j]-v[k][i-1]))) continue;
                i==0?mi=min(mi,v[k][j]):mi=min(mi,v[k][j]-v[k][i-1]);
                i==0?ma=max(ma,v[k][j]):ma=max(ma,v[k][j]-v[k][i-1]);
            }
            a+=(ma-mi);
        }
    }
    return a;
}
```
# Linked List

# Recursion

# Bit Manipulation

# Stack and Queue

# Sliding Window and Two Pointer

# Heap

# Greedy

# Binary Tree 

# Binary Search Tree

# Graph

BFS
```
vector<int>bfsOfGraph(int V, vector<int> adj[]){
    vector<int> bfs; 
    vector<int> vis(V, 0); 
    queue<int> q; 
    q.push(0); 
    vis[0] = 1; 
    while(!q.empty()) {
        int node = q.front();
        q.pop(); 
        bfs.push_back(node); 
        for(auto it : adj[node]) {
            if(!vis[it]) {
                q.push(it); 
                vis[it] = 1; 
            }
        }
    }
    return bfs; 
}
```
DFS
```
void dfs(int node, vector<int> &vis, vector<int> adj[], vector<int> &storeDfs) {
    storeDfs.push_back(node); 
    vis[node] = 1; 
    for(auto it : adj[node]) {
        if(!vis[it]) {
            dfs(it, vis, adj, storeDfs); 
        }
    }
}

vector<int>dfsOfGraph(int V, vector<int> adj[]){
    vector<int> storeDfs; 
    vector<int> vis(V+1, 0); 
    for(int i = 1;i<=V;i++) {
        if(!vis[i]) dfs(i, vis, adj, storeDfs); 
    }
    return storeDfs; 
}
```
Number of Provinces
```
void f(int node,int n,vector<vector<int>>& g,vector<bool> &vis){
    vis[node]=true;
    for(int i=0;i<n;i++){
        if(g[node][i]==1 && !vis[i]){
            f(i,n,g,vis);
        }
    }
}

int findCircleNum(vector<vector<int>>& g) {
    int n=g.size(),count=0;
    vector<bool> vis(n,false);
    for(int i=0;i<n;i++){
        if(!vis[i]){
            f(i,n,g,vis);
            count++;
        }
    }
    return count;
}
```
Connected Components in Matrix
```
```
Rotting Oranges
```
int orangesRotting(vector<vector<int>>& grid) {
    queue<pair<int,int>> q;
    int tot=0,cnt=0,ans=0;
    for(int i=0;i<grid.size();i++){
        for(int j=0;j<grid[0].size();j++){
            if(grid[i][j]!=0) tot++;
            if(grid[i][j]==2) q.push({i,j});
        }
    }
    int dx[]={0,0,1,-1};
    int dy[]={1,-1,0,0};
    while(!q.empty()){
        int sz=q.size();
        cnt+=sz;
        while(sz--){
            int x=q.front().first;
            int y=q.front().second;
            q.pop();
            for(int i=0;i<4;i++){
                int nx=x+dx[i];
                int ny=y+dy[i];
                if(nx>=0 && ny>=0 && nx<grid.size() && ny<grid[0].size() && grid[nx][ny]==1){
                    grid[nx][ny]=2;
                    q.push({nx,ny});
                } 
            }
        }
        if(!q.empty()) ans++;
    }
    if(tot==cnt) return ans;
    else return -1;
}
```
Flood fill
```
void dfs(vector<vector<int>>& m, int i, int j,int p, int n){
    if(i>=0 && i<m.size() && j>=0 && j<m[0].size() && m[i][j]==p){
        m[i][j]=n;
        int x[4]={0,0,1,-1};
        int y[4]={1,-1,0,0};
        for(int k=0;k<4;k++) dfs(m,i+x[k],j+y[k],p,n);
    }
    return;
}

vector<vector<int>> floodFill(vector<vector<int>>& m, int i, int j, int new_color) {
    int prev_color=m[i][j];
    if(prev_color == new_color) return m;
    dfs(m,i,j,prev_color,new_color);
    return m;
}
```
Cycle check Undirected Graph BFS
```
bool checkForCycle(int s, int V, vector<int> adj[], vector<int>& visited)
{
    vector<int> parent(V, -1);
    queue<pair<int,int>> q;
    visited[s] = true;
    q.push({s, -1});
    while (!q.empty()) {
        int node = q.front().first;
        int par = q.front().second;
        q.pop();
        for (auto it : adj[node]) {
            if (!visited[it]) {
                visited[it] = true;
                q.push({it, node});
            }
            else if (par != it)
                return true;
        }
    }
    return false;
}

bool isCycle(int V, vector<int>adj[]){
    vector<int> vis(V, 0); 
    for(int i = 0;i<V;i++) {
        if(!vis[i]) {
            if(checkForCycle(i, V, adj, vis)) return true; 
        }
    }
    return false; 
}
```
Cycle check Undirected Graph DFS
```
bool checkForCycle(int node, int parent, vector<int> &vis, vector<int> adj[]) {
    vis[node] = 1; 
    for(auto it: adj[node]) {
        if(!vis[it]) {
            if(checkForCycle(it, node, vis, adj)) 
                return true; 
        }
        else if(it!=parent) 
            return true; 
    }
    return false; 
}

bool isCycle(int V, vector<int>adj[]){
    vector<int> vis(V+1, 0); 
    for(int i = 0;i<V;i++) {
        if(!vis[i]) {
            if(checkForCycle(i, -1, vis, adj)) return true; 
        }
    }
    return false; 
}
```
Cycle check Directed Graph BFS
```
bool isCyclic(int N, vector<int> adj[]) {
    queue<int> q; 
    vector<int> indegree(N, 0); 
    for(int i = 0;i<N;i++) {
        for(auto it: adj[i]) {
            indegree[it]++; 
        }
    }
    for(int i = 0;i<N;i++) {
        if(indegree[i] == 0) {
            q.push(i); 
        }
    }
    int cnt = 0;
    while(!q.empty()) {
        int node = q.front(); 
        q.pop(); 
        cnt++; 
        for(auto it : adj[node]) {
            indegree[it]--;
            if(indegree[it] == 0) {
                q.push(it); 
            }
        }
    }
    if(cnt == N) return false; 
    return true; 
}
```
Cycle check Directed Graph DFS
```
bool checkCycle(int node, vector<int> adj[], int vis[], int dfsVis[]) {
    vis[node] = 1; 
    dfsVis[node] = 1; 
    for(auto it : adj[node]) {
        if(!vis[it]) {
            if(checkCycle(it, adj, vis, dfsVis)) return true;
        } else if(dfsVis[it]) {
            return true; 
        }
    }
    dfsVis[node] = 0; 
    return false;
}

bool isCyclic(int N, vector<int> adj[]) {
    int vis[N], dfsVis[N]; 
    memset(vis, 0, sizeof vis); 
    memset(dfsVis, 0, sizeof dfsVis); 
    for(int i = 0;i<N;i++) {
        if(!vis[i]) {
            if(checkCycle(i, adj, vis, dfsVis)) {
                return true; 
            }
        }
    }
    return false; 
}
```
0/1 Matrix
```
```
Surrounded Regions
```
void f(int i,int j,vector<vector<char>>& board,int r,int c){
    if(i<0 || i>=r || j<0 || j>=c || board[i][j]!='O'){
        return;
    }
    if(board[i][j]=='O') board[i][j]='#';
    f(i+1,j,board,r,c);
    f(i-1,j,board,r,c);
    f(i,j+1,board,r,c);
    f(i,j-1,board,r,c);
}

void solve(vector<vector<char>>& board) {
    int r=board.size();
    int c=board[0].size();
    for(int i=0;i<r;i++){
        for(int j=0;j<c;j++){
            if((i==0 || i==r-1 || j==0 || j==c-1) &&  board[i][j]=='O'){
                f(i,j,board,r,c);
            }
        }
    }
        for(int i=0;i<r;i++){
        for(int j=0;j<c;j++){
            if(board[i][j]=='#') board[i][j]='O';
            else board[i][j]='X';
        }
    }   
}
```
Number of Enclaves
```
void dfs(vector<vector<int>>& m,int i,int j){
    if(i>=0 && i<m.size() && j>=0 && j<m[0].size() && m[i][j]==1){
        m[i][j]=0;
        int x[4]={0,0,1,-1};
        int y[4]={1,-1,0,0};
        for(int k=0;k<4;k++) dfs(m,i+x[k],j+y[k]);
    }
}

int numEnclaves(vector<vector<int>>& m) {
    int r=m.size(),c=m[0].size(),count=0;
    for(int i=0;i<r;i++) for(int j=0;j<c;j++) if((i==0 || i==r-1 || j==0 || j==c-1) && m[i][j]==1) dfs(m,i,j);
    for(int i=0;i<r;i++) for(int j=0;j<c;j++) if(m[i][j]) count++;
    return count; 
}
```
Word Ladder 1
```
int ladderLength(string s, string t, vector<string>& a) {
    unordered_map<string,bool> mp;
    for(int i=0;i<a.size();i++) mp[a[i]]=false; 
    queue<string> q;
    string temp;
    int step=1;
    q.push(s);
    while(!q.empty()){
        int sz=q.size();
        while(sz--){
            string x=q.front();
            if(x==t) return step;
            q.pop();
            for(int i=0;i<x.size();i++){
                for(char j='a';j<='z';j++){
                    temp=x;
                    temp[i]=j;
                    if(mp.find(temp)!=mp.end() && !mp[temp]){
                        mp[temp]=true;
                        q.push(temp);
                    }
                }
            }
        }
        step++;
    }
    return 0;
}
```
Word Ladder 2
```
```
Number of Islands 2
```
void bfs(int row, int col, vector<vector<int>> &vis, vector<vector<char>>&grid) {
    vis[row][col] = 1; 
    queue<pair<int,int>> q;
    q.push({row, col}); 
    int n = grid.size(); 
    int m = grid[0].size(); 
    while(!q.empty()) {
        int row = q.front().first; 
        int col = q.front().second; 
        q.pop(); 
        for(int delrow = -1; delrow<=1;delrow++) {
            for(int delcol = -1; delcol <= 1; delcol++) {
                int nrow = row + delrow; 
                int ncol = col + delcol; 
                if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m 
                && grid[nrow][ncol] == '1' && !vis[nrow][ncol]) {
                    vis[nrow][ncol] = 1; 
                    q.push({nrow, ncol}); 
                }
            }
        }
    }
}

int numIslands(vector<vector<char>>& grid) {
    int n = grid.size(); 
    int m = grid[0].size(); 
    vector<vector<int>> vis(n, vector<int>(m, 0)); 
    int cnt = 0; 
    for(int row = 0; row < n ; row++) {
        for(int col = 0; col < m ;col++) {
            if(!vis[row][col] && grid[row][col] == '1') {
                cnt++; 
                bfs(row, col, vis, grid); 
            }
        }
    }
    return cnt; 
}
```
Bipartite Graph
```
bool isBipartite(vector<vector<int>>& g) {
    vector<int> vis(g.size(),-1);
    queue<int> q;
    for(int i=0;i<g.size();i++){
        if(vis[i]!=-1) continue;
        q.push(i);
        vis[i]=0;
        int node;
        while(!q.empty()){
            node=q.front();
            q.pop();
            for(auto it:g[node]){
                if(vis[it]==-1){
                    vis[it]=1-vis[node];
                    q.push(it);
                }
                else if(vis[it]==vis[node]) return false;
            }
        }
    }
    return true;
}
```
Kahn’s Algorithm (Topological Sort)
```
vector<int> topoSort(int V, vector<int> adj[])
{
    int indegree[V] = {0};
    for (int i = 0; i < V; i++) {
        for (auto it : adj[i]) {
            indegree[it]++;
        }
    }
    queue<int> q;
    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0) {
            q.push(i);
        }
    }
    vector<int> topo;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        topo.push_back(node);
        for (auto it : adj[node]) {
            indegree[it]--;
            if (indegree[it] == 0) q.push(it);
        }
    }
    return topo;
}
```
Course Schedule 1
```
bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    vector<int> g[numCourses];
    vector<int> in(numCourses,0);
    for(int i=0;i<prerequisites.size();i++){
        g[prerequisites[i][1]].push_back(prerequisites[i][0]);
        in[prerequisites[i][0]]++;
    }
    int count=0;
    queue<int> q;
    for(int i=0;i<numCourses;i++) if(in[i]==0) q.push(i);
    while(!q.empty()){
        int x=q.front();
        q.pop();
        count++;
        for(auto it:g[x]){
            in[it]--;
            if(in[it]==0) q.push(it); 
        }
    }
    if(count==numCourses) return true;
    return false;
}
```
Course Schedule 2
```
vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
    vector<int> ans;
    vector<int> g[numCourses];
    vector<int> in(numCourses,0);
    for(int i=0;i<prerequisites.size();i++){
        g[prerequisites[i][1]].push_back(prerequisites[i][0]);
        in[prerequisites[i][0]]++;
    }
    int count=0;
    queue<int> q;
    for(int i=0;i<numCourses;i++) if(in[i]==0) q.push(i);
    while(!q.empty()){
        int x=q.front();
        ans.push_back(x);
        q.pop();
        count++;
        for(auto it:g[x]){
            in[it]--;
            if(in[it]==0) q.push(it); 
        }
    }
    if(count==numCourses) return ans;
    return {};
}
```
Find Eventual Safe States
```
vector<int> eventualSafeNodes(vector<vector<int>>& l) {
    vector<vector<int>> g(l.size());
    for(int i=0;i<l.size();i++) for(int j=0;j<l[i].size();j++) g[l[i][j]].push_back(i);
    vector<int> in(g.size(),0);
    vector<int> a;
    for(int i=0;i<g.size();i++) for(int j=0;j<g[i].size();j++) in[g[i][j]]++;
    queue<int> q;
    for(int i=0;i<in.size();i++) if(!in[i]) q.push(i);
    while(!q.empty()){
        int x=q.front();
        a.push_back(x);
        q.pop();
        for(auto it:g[x]){
            in[it]--;
            if(!in[it]) q.push(it);
        }
    } 
    sort(a.begin(),a.end());
    return a;
}
```
Alien dictionary
```
```
Shortest Path in Undirected Graph with Unit distance
```
vector<int> shortestPath(vector<vector<int>>& edges, int N,int M, int src){
    vector<int> adj[N]; 
    for(auto it : edges) {
        adj[it[0]].push_back(it[1]); 
        adj[it[1]].push_back(it[0]); 
    }
    int dist[N];
    for(int i = 0;i<N;i++) dist[i] = 1e9;
    dist[src] = 0; 
    queue<int> q;
    q.push(src); 
    while(!q.empty()) {
        int node = q.front(); 
        q.pop(); 
        for(auto it : adj[node]) {
            if(dist[node] + 1 < dist[it]) {
                dist[it] = 1 + dist[node]; 
                q.push(it); 
            }
        }
    }
    return dist; 
}
```
Shortest Path in DAG
```
void topoSort(int node, vector < pair < int, int >> adj[],
    int vis[], stack < int > & st) {
    vis[node] = 1;
    for (auto it: adj[node]) {
        int v = it.first;
        if (!vis[v]) topoSort(v, adj, vis, st);
    }
    st.push(node);
}

vector < int > shortestPath(int N, int M, vector < vector < int >> & edges) {
    vector < pair < int, int >> adj[N];
    for (int i = 0; i < M; i++) {
        int u = edges[i][0];
        int v = edges[i][1];
        int wt = edges[i][2];
        adj[u].push_back({v, wt}); 
    }
    int vis[N] = {0};
    stack < int > st;
    for (int i = 0; i < N; i++) {
        if (!vis[i]) topoSort(i, adj, vis, st);
    }
    vector < int > dist(N);
    for (int i = 0; i < N; i++) dist[i] = 1e9;
    dist[0] = 0;
    while (!st.empty()) {
        int node = st.top();
        st.pop();
        for (auto it: adj[node]) {
            int v = it.first;
            int wt = it.second;
            if (dist[node] + wt < dist[v]) {
                dist[v] = wt + dist[node];
            }
        }
    }
    return dist;
}
```
Dijkstra Algorithm
```
vector <int> dijkstra(int V, vector<vector<int>> adj[], int S) {
    set<pair<int,int>> st; 
    vector<int> dist(V, 1e9); 
    st.insert({0, S}); 
    dist[S] = 0;
    while(!st.empty()) {
        auto it = *(st.begin()); 
        int node = it.second; 
        int dis = it.first; 
        st.erase(it); 
        for(auto it : adj[node]) {
            int adjNode = it[0]; 
            int edgW = it[1]; 
            if(dis + edgW < dist[adjNode]) {
                if(dist[adjNode] != 1e9) st.erase({dist[adjNode], adjNode}); 
                dist[adjNode] = dis + edgW; 
                st.insert({dist[adjNode], adjNode}); 
                }
        }
    }
    return dist; 
}
```
Dijkstra Algorithm (Efficient)
```
vector<int> dijkstra(int V, vector<vector<int>> adj[], int S) { 
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<int> distTo(V, INT_MAX);
    distTo[S] = 0;
    pq.push({0, S});
    while (!pq.empty())
    {
        int node = pq.top().second;
        int dis = pq.top().first;
        pq.pop();
        for (auto it : adj[node])
        {
            int v = it[0];
            int w = it[1];
            if (dis + w < distTo[v])
            {
                distTo[v] = dis + w;
                pq.push({dis + w, v});
            }
        }
    }
    return distTo;
}
```
Shortest Path in Binary Matrix
```
int shortestPathBinaryMatrix(vector<vector<int>>& g) {
    if(g[0][0]==1) return -1;
    queue<pair<int,int>> q;
    q.push({0,0});
    int c=0;
    int x_arr[]={-1,0,1,-1,1,-1,0,1};
    int y_arr[]={-1,-1,-1,0,0,1,1,1};
    int x,y,nx,ny;
    while(!q.empty()){
        c++;
        int sz=q.size();
        while(sz--){
            x=q.front().first;
            y=q.front().second;
            if(x==g.size()-1 && y==g.size()-1) return c;
            q.pop();
            for(int i=0;i<8;i++){
                nx=x+x_arr[i];
                ny=y+y_arr[i];
                if(nx>=0 && nx<g.size() && nx>=0 && ny<g.size() && !g[nx][ny]){
                    g[nx][ny]=1;
                    q.push({nx,ny});
                }
            }
        }
    }
    return -1;
}
```
Path With Minimum Effort
```
int minimumEffortPath(vector<vector<int>>& g) {
    int r=g.size(),c=g[0].size();
    priority_queue<pair<int,pair<int,int>>,vector<pair<int,pair<int,int>>>,greater<pair<int,pair<int,int>>>> pq;
    pq.push({0,{0,0}});
    vector<vector<int>> dist(r,vector<int>(c,1e9));
    dist[0][0]=0;
    int x_arr[]={0,0,1,-1};
    int y_arr[]={1,-1,0,0};
    int nx,ny,diff,x,y,ma;
    while(!pq.empty()){
        auto p=pq.top();
        pq.pop();
        diff=p.first;
        x=p.second.first;
        y=p.second.second;
        if(x==r-1 && y==c-1) return diff;
        for(int i=0;i<4;i++){
            nx=x+x_arr[i];
            ny=y+y_arr[i];
            if(nx>=0 && nx<r && ny>=0 && ny<c){
                ma=max(diff,abs(g[x][y]-g[nx][ny]));
                if(ma<dist[nx][ny]){
                    dist[nx][ny]=ma;
                    pq.push({ma,{nx,ny}});
                }
            }
        }
    }
    return 0;
}
```
Cheapest Flights Within K Stops
```
int findCheapestPrice(int n, vector<vector<int>>& e, int s, int t, int k) {
    vector<pair<int,int>> g[n];
    for(auto it:e) g[it[0]].push_back({it[1],it[2]});
    queue<pair<int,pair<int,int>>> q;
    vector<int> dist(n,1e9);
    q.push({0,{s,0}});
    dist[s]=0;
    int step,node,weight;
    while(!q.empty()){
        auto p=q.front();
        q.pop();
        step=p.first;
        node=p.second.first;
        weight=p.second.second;
        for(auto it:g[node]){
            if(dist[it.first]>it.second+weight && step<=k){
                dist[it.first]=it.second+weight;
                q.push({step+1,{it.first,dist[it.first]}});
            }
        }
    }
    if(dist[t]==1e9) return -1;
    return dist[t];
}
```
Network Delay Time
```
int networkDelayTime(vector<vector<int>>& times, int n, int k) {
    vector<pair<int,int>> g[n];
    for(int i=0;i<times.size();i++){
        g[times[i][0]-1].push_back({times[i][1]-1,times[i][2]});            
    }
    vector<int> dist(n,1e9);
    dist[k-1]=0;
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> q;
    q.push({0,k-1});
    while(!q.empty()){
        int d=q.top().first;
        int x=q.top().second;
        q.pop();
        for(auto it:g[x]){
            if(dist[it.first]>dist[x]+it.second){
                dist[it.first]=dist[x]+it.second;
                q.push({dist[it.first],it.first});
            }
        }
    }
    int ans=INT_MIN;
    for(int i=0;i<n;i++){
        ans=max(ans,dist[i]);
    }
    if(ans==1e9) return -1;
    return ans;
}
```
Number of Ways to Arrive at Destination
```
```
Minimum Multiplications to Reach End
```
int minimumMultiplications(vector<int> &arr, int start, int end) {
    queue<pair<int, int>> q;
    q.push({start, 0});
    vector<int> dist(100000, 1e9);
    dist[start] = 0;
    int mod = 100000;
    while (!q.empty())
    {
        int node = q.front().first;
        int steps = q.front().second;
        q.pop();
        for (auto it : arr)
        {
            int num = (it * node) % mod;
            if (steps + 1 < dist[num])
            {
                dist[num] = steps + 1;
                if (num == end)
                    return steps + 1;
                q.push({num, steps + 1});
            }
        }
    }
    return -1;
}
```
Bellman Ford Algorithm
```
vector<int> bellman_ford(int V, vector<vector<int>>& edges, int S) {
    vector<int> dist(V, 1e8);
    dist[S] = 0;
    for (int i = 0; i < V - 1; i++) {
        for (auto it : edges) {
            int u = it[0];
            int v = it[1];
            int wt = it[2];
            if (dist[u] != 1e8 && dist[u] + wt < dist[v]) {
                dist[v] = dist[u] + wt;
            }
        }
    }
    for (auto it : edges) {
        int u = it[0];
        int v = it[1];
        int wt = it[2];
        if (dist[u] != 1e8 && dist[u] + wt < dist[v]) {
            return { -1};
        }
    }
    return dist;
}
```
Floyd Warshall Algorithm
```
void shortest_distance(vector<vector<int>>&matrix) {
    int n = matrix.size();
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == -1) matrix[i][j] = 1e9;
            if (i == j) matrix[i][j] = 0;
        }
    }
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = min(matrix[i][j], matrix[i][k] + matrix[k][j]);
            }
        }
    }
}
```
Find the City With the Smallest Number of Neighbors at a Threshold Distance
```
    int findTheCity(int n, vector<vector<int>>& e, int t) {
        vector<vector<int>> g(n,vector<int>(n,INT_MAX));
        for(auto it:e){
            g[it[0]][it[1]]=it[2];
            g[it[1]][it[0]]=it[2];
        }
        for(int i=0;i<n;i++) g[i][i]=0;
        for(int k=0;k<n;k++){
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    if(g[i][k]!=INT_MAX && g[k][j]!=INT_MAX) g[i][j]=min(g[i][j],g[i][k]+g[k][j]);
                }
            }
        }
        int c,city=-1,v=n;
        for(int i=0;i<n;i++){
            c=0;
            for(auto j:g[i]){
                if(j<=t) c++;
            }
            if(c<=v){
                v=c;
                city=i;
            }
        }
        return city;
    }
```
Prim’s Algorithm
```
```
Disjoint Set Union
```
public:
    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        parent.resize(n + 1);
        size.resize(n + 1);
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int findUPar(int node) {
        if (node == parent[node])
            return node;
        return parent[node] = findUPar(parent[node]);
    }

    void unionByRank(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v;
        }
        else if (rank[ulp_v] < rank[ulp_u]) {
            parent[ulp_v] = ulp_u;
        }
        else {
            parent[ulp_v] = ulp_u;
            rank[ulp_u]++;
        }
    }

    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        }
        else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
};
```
Kruskal’s Algorithm
```
int spanningTree(int V, vector<vector<int>> adj[]) {
    vector<pair<int, pair<int, int>>> edges;
    for (int i = 0; i < V; i++) {
        for (auto it : adj[i]) {
            int adjNode = it[0];
            int wt = it[1];
            int node = i;
            edges.push_back({wt, {node, adjNode}});
        }
    }
    DisjointSet ds(V);
    sort(edges.begin(), edges.end());
    int mstWt = 0;
    for (auto it : edges) {
        int wt = it.first;
        int u = it.second.first;
        int v = it.second.second;
        if (ds.findUPar(u) != ds.findUPar(v)) {
            mstWt += wt;
            ds.unionBySize(u, v);
        }
    }
    return mstWt;
}
```
Number of Operations to Make Network Connected
```
void f(int node,vector<vector<int>>& g,vector<bool> &vis){
    vis[node]=true;
    for(auto it:g[node]){
        if(!vis[it]) f(it,g,vis);
    }
}

int makeConnected(int n, vector<vector<int>>& c) {
    if(c.size()<n-1) return -1;
    vector<vector<int>> g(n);
    for(auto it:c) g[it[0]].push_back(it[1]),g[it[1]].push_back(it[0]);
    vector<bool> vis(n);
    int a=0;
    for(int i=0;i<n;i++){
        if(!vis[i]) f(i,g,vis),a++;
    }
    return a-1;
}
```
Most Stones Removed with Same Row or Column
```
int par[20001];
int sz[20001];

int parent(int n){
    if(par[n]==n) return n;
    return par[n]=parent(par[n]);
}

void add(int u,int v){
    int u_par=parent(u);
    int v_par=parent(v);
    if(u_par==v_par) return;
    if(sz[u_par]>sz[v_par]){
        par[v_par]=u_par;
        sz[u_par]+=sz[v_par];
    }
    else{
        par[u_par]=v_par;
        sz[v_par]+=sz[u_par];
    }
}

int removeStones(vector<vector<int>>& a) {
    int c=0;
    for(int i=0;i<20001;i++){
        par[i]=i;
        sz[i]=0;
    }
    int row=INT_MIN;
    for(auto it:a) row=max(row,it[0]);
    unordered_set<int> s;
    for(auto it:a){
        add(it[0],it[1]+row+1);
        s.insert(it[0]);
        s.insert(it[1]+row+1);
    }
    for(auto it:s) if(parent(it)==it) c++;
    return a.size()-c;
}
```
Accounts Merge
```
int p[1001];
int sz[1001];

int par(int n){
    if(p[n]==n) return n;
    return p[n]=par(p[n]);
}

void add(int u,int v){
    int pu=par(u);
    int pv=par(v);
    if(pu==pv) return;
    if(sz[pu]>sz[pv]){
        p[pv]=pu;
        sz[pu]+=sz[pv];
    }
    else{
        p[pu]=pv;
        sz[pv]+=sz[pu];
    }
}

vector<vector<string>> accountsMerge(vector<vector<string>>& a) {
    for(int i=0;i<1001;i++){
        p[i]=i;
        sz[i]=0;
    }
    unordered_map<string,int> mp;
    for(int i=0;i<a.size();i++){
        for(int j=1;j<a[i].size();j++){
            if(mp.find(a[i][j])==mp.end()) mp[a[i][j]]=i;
            else add(i,mp[a[i][j]]);
        }
    }
    unordered_map<int,set<string>> acc;
    for(auto it:mp){
        acc[par(it.second)].insert(it.first);
    }
    vector<vector<string>> ans;
    vector<string> usr;
    for(auto it:acc){
        cout<<a[it.first][0]<<" ";
        for(auto j:it.second) cout<<j<<" ";
        cout<<"\n";
        int pa=par(it.first);
        if(it.first==pa) usr.push_back(a[it.first][0]);          
        for(auto j:it.second) usr.push_back(j);
        ans.push_back(usr);
        usr.clear();
    }
    return ans;
}
```
Number of island II
```
```
Making A Large Island
```
int p[250001];
int sz[250001];

int par(int n){
    if(p[n]==n) return n;
    return p[n]=par(p[n]);
}

void add(int u,int v){
    int pu=par(u);
    int pv=par(v);
    if(pu==pv) return;
    if(sz[pu]>sz[pv]){
        p[pv]=pu;
        sz[pu]+=sz[pv];
    }
    else{
        p[pu]=pv;
        sz[pv]+=sz[pu];
    }
}

int largestIsland(vector<vector<int>>& g) {
    for(int i=0;i<250001;i++){
        p[i]=i;
        sz[i]=1;
    }
    int r=g.size(),c=g[0].size(),xa,ya,pa,sum,ans=0;
    set<int> s;
    int x_arr[]={0,0,1,-1},y_arr[]={1,-1,0,0};
    for(int i=0;i<r;i++){
        for(int j=0;j<c;j++){
            if(g[i][j]){
                for(int k=0;k<4;k++){
                    xa=i+x_arr[k];
                    ya=j+y_arr[k];
                    if(xa<0 || xa>=r || ya<0 || ya>=c || !g[xa][ya]) continue;
                    add(i*c+j,xa*c+ya);
                }
            }
        }
    }

    for(int i=0;i<r;i++){
        for(int j=0;j<c;j++){
            if(!g[i][j]){
                sum=0;
                s.clear();
                for(int k=0;k<4;k++){
                    xa=i+x_arr[k];
                    ya=j+y_arr[k];
                    if(xa<0 || xa>=r || ya<0 || ya>=c || !g[xa][ya]) continue;
                    pa=par(xa*c+ya);
                    if(s.find(pa)==s.end()) sum+=sz[pa];
                    s.insert(pa);
                }
                ans=max(ans,sum+1);
            }
        }
    }
    if(!ans) return r*c;
    return ans;
}
```
Swim in rising water
```
```
Bridges in Graph
```
int timer=1;

void f(vector<int> g[],vector<bool> &vis,vector<int> &tin,vector<int> &low,vector<vector<int>> &b,int node,int p){
    vis[node]=true;
    tin[node]=low[node]=timer;
    timer++;
    for(auto it:g[node]){
        if(it==p) continue;
        if(!vis[it]){
            f(g,vis,tin,low,b,it,node);
            low[node]=min(low[node],low[it]);
            if(tin[node]<low[it]) b.push_back({node,it});
        }
        else{
            low[node]=min(low[node],low[it]);
        }
    }
}

vector<vector<int>> criticalConnections(int n, vector<vector<int>>& c) {
    vector<vector<int>> b;
    vector<int> g[n];
    for(auto it:c){
        g[it[0]].push_back(it[1]);
        g[it[1]].push_back(it[0]);
    }
    vector<bool> vis(n);
    vector<int> tin(n);
    vector<int> low(n);
    f(g,vis,tin,low,b,0,-1);
    return b;
}
```
Articulation Point
```
```
Kosaraju's Algorithm
```
void dfs(int node, vector<int> &vis, vector<int> adj[], stack<int> &st) {
    vis[node] = 1;
    for (auto it : adj[node]) {
        if (!vis[it]) {
            dfs(it, vis, adj, st);
        }
    }
    st.push(node);
}

void dfs3(int node, vector<int> &vis, vector<int> adjT[]) {
    vis[node] = 1;
    for (auto it : adjT[node]) {
        if (!vis[it]) {
            dfs3(it, vis, adjT);
        }
    }
}

int kosaraju(int V, vector<int> adj[])
{
    vector<int> vis(V, 0);
    stack<int> st;
    for (int i = 0; i < V; i++) {
        if (!vis[i]) {
            dfs(i, vis, adj, st);
        }
    }
    vector<int> adjT[V];
    for (int i = 0; i < V; i++) {
        vis[i] = 0;
        for (auto it : adj[i]) {
            adjT[it].push_back(i);
        }
    }
    int scc = 0;
    while (!st.empty()) {
        int node = st.top();
        st.pop();
        if (!vis[node]) {
            scc++;
            dfs3(node, vis, adjT);
        }
    }
    return scc;
}
```


# Dynamic Programming

# Trie
