**C++ solution of Largest Rectangle in Histogram**

class Solution {
public:
    vector<int> prevsmaller(vector<int> arr){
        stack<int> st;
        st.push(-1);
        vector<int>ans(arr.size());
        for(int i=0; i<arr.size();i++){
            int curr = arr[i];
            while(st.top() != -1 && arr[st.top()] >=curr){
                st.pop();
            }
            ans[i]=st.top();
            st.push(i);//index push kr rhe h 
        }
        return ans;
    }
    vector<int> nextsmaller(vector<int> arr){
        stack<int> st;
        int n = arr.size();
        st.push(n);
        vector<int>ans(n);
        for(int i=arr.size()-1; i>=0; i--){
            int curr = arr[i];
            while(st.top() != n && arr[st.top()]>=curr){
                st.pop();
            }
            ans[i]=st.top();
            st.push(i);//index push kr rhe h 
        }
        return ans;
    }
    
    int largestRectangleArea(vector<int>& heights) {
        vector<int> prev =prevsmaller(heights); 
        vector<int> next =nextsmaller(heights); 
        int maxarea = INT_MIN;
        for(int i=0;i<heights.size(); i++){

            int length = heights[i];
            int width = next[i]-prev[i]-1;

            int area = length * width;
            maxarea = max(maxarea,area);

             
        }
        return maxarea;

    }
};
