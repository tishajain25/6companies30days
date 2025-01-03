# Shopping Offers

[Problem Link](https://leetcode.com/problems/shopping-offers/description/) 

You are given the prices of items, special offers (bundles of items at discounted prices), and the number of items you need to buy. 
Determine the minimum cost to buy exactly the required items, using both individual item prices and special offers. 
You cannot buy more items than needed.

### Sample Input 
```
price = [2, 5]
special = [[3, 0, 5], [1, 2, 10]]
needs = [3, 2]
```
### Sample Output 
```
14 
```

### Solution
```java
class Solution {
    public int shoppingOffers(List<Integer> price, List<List<Integer>> special, List<Integer> needs) {
        Map<List<Integer>, Integer> memo = new HashMap<>(); // Memoization map
        return dfs(price, special, needs, memo);
    }
    
    private int dfs(List<Integer> price, List<List<Integer>> special, List<Integer> needs, Map<List<Integer>, Integer> memo) {
        if (memo.containsKey(needs)) {
            return memo.get(needs); // Return precomputed result
        }
        
        // Calculate the cost without any special offers
        int minCost = calculateDirectCost(price, needs);
        
        // Try applying each special offer
        for (List<Integer> offer : special) {
            List<Integer> updatedNeeds = new ArrayList<>(needs);
            boolean validOffer = true;

            // Check if the offer is valid
            for (int i = 0; i < needs.size(); i++) {
                updatedNeeds.set(i, updatedNeeds.get(i) - offer.get(i));
                if (updatedNeeds.get(i) < 0) { // Offer is invalid if it exceeds needs
                    validOffer = false;
                    break;
                }
            }
            
            // If valid, recursively calculate the cost
            if (validOffer) {
                minCost = Math.min(minCost, offer.get(offer.size() - 1) + dfs(price, special, updatedNeeds, memo));
            }
        }
        
        // Store the result in the memoization map
        memo.put(needs, minCost);
        return minCost;
    }
    
    private int calculateDirectCost(List<Integer> price, List<Integer> needs) {
        int cost = 0;
        for (int i = 0; i < price.size(); i++) {
            cost += price.get(i) * needs.get(i); // Cost of buying items directly
        }
        return cost;
    }
}
```

### Accepted
![Screenshot 2025-01-03 at 10 29 13 PM](https://github.com/user-attachments/assets/83464a6d-8570-4038-9d57-125acf44e07e)
