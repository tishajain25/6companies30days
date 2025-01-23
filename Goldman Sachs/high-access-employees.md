# High-Access Employees

[Problem Link](https://leetcode.com/problems/high-access-employees/description/) 


Given a list of employee names and their access times (in "HHMM" format), find employees who accessed the system three or more times within any one-hour window. An hour window 
means the difference between the earliest and latest access times is less than 60 minutes.

Return the names of such employees in any order.

### Sample Input 
```
access_times = [["a", "0549"], ["b", "0457"], ["a", "0532"], ["a", "0621"], ["b", "0540"]]
```
### Sample Output 
```
["a"]
```

### Solution
```java
class Solution {
    public List<String> findHighAccessEmployees(List<List<String>> access_times) {
        Map<String, List<Integer>> d = new HashMap<>();
        for (var e : access_times) {
            String name = e.get(0), s = e.get(1);
            int t = Integer.valueOf(s.substring(0, 2)) * 60 + Integer.valueOf(s.substring(2));
            d.computeIfAbsent(name, k -> new ArrayList<>()).add(t);
        }
        List<String> ans = new ArrayList<>();
        for (var e : d.entrySet()) {
            String name = e.getKey();
            var ts = e.getValue();
            Collections.sort(ts);
            for (int i = 2; i < ts.size(); ++i) {
                if (ts.get(i) - ts.get(i - 2) < 60) {
                    ans.add(name);
                    break;
                }
            }
        }
        return ans;
    }
}
```

### Accepted
![Screenshot 2025-01-23 at 1 58 13 PM](https://github.com/user-attachments/assets/31b5cad7-4644-4555-9d9a-e39a52759ebe)
