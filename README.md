
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
