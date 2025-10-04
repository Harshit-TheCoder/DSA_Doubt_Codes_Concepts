## An Odd Number has divisors all of which are odd.

--- 
## To break a number in 'k' parts of different powers of 2, i.e, num = 2^a + 2^b + 2^c + .... k times EXACTLY,
- it is possible only if number of set bits in num <= k <= num

---

## In terms of bits, a number num always lies between [ b^k , b^(k+1) -1 ]
- Eg, if base is 4 then [4^0, 4^(0+1) - 1] -> 0 - 3
- [4^1, 4^(1+1) - 1] -> 4 - 15
-  [4^2, 4^(2+1) - 1] -> 16 - 63 and so on

---

## XOR Basis Trick (Short Form)
    Purpose
    Represent all subset XORs compactly.
    Answer queries like max subset XOR, kth subset XOR, representability.
    Rules
    Insert Rule:
        For each number, reduce it with current basis (XOR out higher bits).
        If it becomes 0 → skip (dependent).
        Else put it in the basis at its MSB position.
        ✅ Reason: Ensures basis is linearly independent, like Gaussian elimination.
    Max XOR Rule:
        Start ans = 0.
        From high → low bits: if ans ^ basis[i] > ans, then do ans ^= basis[i].
        ✅ Reason: Always try to add higher-bit vectors if they increase the number.
    Representability Rule:
        To check if x is possible, reduce x using basis.
        If x ends as 0 → yes, else no.
        ✅ Reason: If x lies in the span of basis, it can be formed.
    Count Rule:
        If basis size = k, then number of distinct subset XORs = 2^k.
        ✅ Reason: Each basis element can be included or not, independently.
    Complexity
    Build basis: O(n · log(maxA))
    (Each number reduced by up to log(maxA) bits).
    Max XOR query: O(log(maxA))
    Representability check: O(log(maxA))
    Distinct count: just O(1) (2^k).

    for(int num: nums){
        for(int i=31;i>=0;i--){
            if((num & (1 << i)) == 0) continue;
            if(basis[i] == 0){
                basis[i] = num;
                break;
            }
            num ^= basis[i];
        }
    }

    int ans = 0;
    for(int i=31;i>=0;i--) ans = Math.max(ans, ans^basis[i]);

---

## If there are two arrays and an inuequality given or some relation to relate two arrays
- always combine the two arrays together using the inequality

--- 

## Difference Array Concept
 - For range updates, we can use difference arrays to precalculate the range in O(n) time.
 - int diff[] = new int[n]
 - diff[l] += 1, diff[r+1] -= -1

---

## Remove some occurences of one character to make string palindrome
    i = 0, j= n-1
    See if s[i] == s[j] do i++; j--;
    else removal of either s[i] or s[j] will make string palidrome else string cannot be palindrome.
    string 0...i-1 and j+1 .... n-1 is already palindrome, 
    between i and j ignore wherever s[i] == s[j]. 
    if s[i] != s[j] and both are not character to be removed then return false.
    else simulate removing the character using two pointers till i<=j.

---

## Jump Array Concept
    In an array, [a1, a2, a3, a4, .... an] you have two operations,
    1. move ahead to a strictly smaller element 
    2. move behind to a strictly greater element
    calculate prefix max, suffix min array, 
    now for each element, 
    start from i=n-2 to i = 0.
    1. p[i] > s[i + 1] then let x = p[i], y = s[i+1] then it is always possible i -> x -> y -> (i+1) then ans[i] = ans[i+1]
    2. p[i] <= s[i + 1] then no valid jump is possible so ans[i] = p[i]

---

## Decrease Array Concept
    let a = [a1, a2, a3, ......, an], you have to choose two ai , aj,  i not = j and decrease both 1 and ultimately see if array can be 0.
    here two conditions are,
    1. Array sum must be even because everytime we are decreasing sum by 2.
    2. Also the largest element M must be M <= S - M where S is sum because to make M 0 we need atleast M 1's among other elements

---

## If we are given 3 binary strings and we have to arrange them in a way such that we get maximum binary number,
- Always remember for 2 strings s and t, iff s + t > t + s,
- Do brute force for 3 strings and do above operation for all 6 permutations.

---

## Find number of rectangles in binary matrix
- Start from top to bottom.
- At each level count height of histograms and count the rectangles using monotonic stack
---

## Segment Problems
- When given an array of segments `[(l1, r1), (l2, r2), ... (ln, rn)]`,  
  **focus on their intersections**.
- Use a **difference array** or **difference map** to handle updates and queries over segments effectively.

---

## Trailing Zeroes in Numbers
- Trailing zeroes are determined by factors of **2** and **5**:
- If multiplying a number `k ≤ m` to maximize trailing zeroes:
1. Count the factors of 2 and 5 in `k`.
2. Balance them such that `count(2) = count(5)`.
3. Multiply by 10 until `k * 10 > m`.
4. Finally, maximize by multiplying with `m/k`.

---

## Making Numbers Equal by Adding Residuals
Transform `[p, q, r, s, t, u, v, w] → [a, a, a, a, a, a, a, a]`  
using remainder patterns of `x % 10`:

- **Cycles of residuals:**
- `0 → 0`
- `1 → 1, 2,4,8,6 ... cycle`
- `2 → 2,4,8,6 ... cycle`
- `3 → 3,6, 2,4,8,6 ... cycle`
- `4 → 4,8,6, 2,4,8,6 ... cycle`
- `5 → 5,0`
- `6 → 6, 2,4,8,6 ... cycle`
- `7 → 7,4,8,6, 2,4,8,6 ... cycle`
- `8 → 8,6, 2,4,8,6 ... cycle`
- `9 → 9,8,6, 2,4,8,6 ... cycle`

- To make all equal:
  Ensure `(p + residual(p % 10))` for all numbers gives the **same remainder**.  
The set of remainders must have **size 1**.

---

## Binary Search on Answer
- When the problem asks to **Minimize/Maximize X** and search space is **sorted**:
1. Apply **Binary Search** on the answer.
2. Use a helper function to check feasibility with `mid`.
3. Ask: **"Can this task be completed with `mid` that satisfies X?"**

---

## Inequalities
- For inequality problems:  
**Always try to simplify the given inequality first.**

---

## Manhattan Distance in 2D Matrices
- Key property:  
**Manhattan distance between one pair is independent of others.**
- Separate coordinates into **X and Y** and handle distances **independently**.

---

## Shifting Houses Problem
- For problems with houses and gaps:
- Shifting each house left/right by 1 to maximize the largest gap.
- **The middle house will never move.**

---

## DP on Divisors
- When applying DP transitions on divisors:
- Finding divisors for all numbers up to `N` costs only:
  ```
  O(N log N)
  ```
- Use this to design efficient transitions.

---

## Algebraic Equations
- If given an algebraic relation between **array elements and indices**:  
**Simplify the equation first** before applying further logic.

---

## XOR Concept
- If XOR of all elements of an array is 0 **YOU CAN REDUCE ARRAY INTO ATLEAST TWO ELEMENTS OF SAME ELEMENT 'X' **
- If XOR of all elements of an array is X **YOU CAN REDUCE TO ATLEAST 2 ELEMENTS 'X' IFF X APPEARS IN PREFIX XOR MORE THAN TWO TIMES **

---

## 2D PLANE AND MANHATTAN DISTANCE
- If points given in 2D plane, and we have to find group of points such that from all those points distance to all input point is minimum, then **FIND MEDIAN POINT AFTER SEPARATING X AND Y**
- IF NUMBER OF POINTS ARE ODD THEN ONLY **1 MEDIAN POINT** ELSE **MEDIAN POINTS FORM A RECTANGLE**
- FORMULA FOR IT IS : DX - DX1 + 1)*(DY2 - DY1 + 1)

---

## FRACTION REDUCTION
- To reduce a fraction to its simplest form ALWAYS **SEPARATE NUMERATOR AND DENOMINATOR AND REDUCE THEM WITH GCD(NUMERATOR, DENOMINATOR)**

---

## DEPENDING ON CONDITIONS U CAN USE PRIORITY QUEUE IN BFS

---

## DFS TO FIND SUBTREE SIZE (ALWAYS REMEMBER)
	static void dfs(List<List<Integer>> graph, int node, int par, int dp[]){
	    dp[node] = 1;
	    for(int neighbour: graph.get(node)){
	      if(neighbour == par) continue; // Don't go back to parent
	      dfs(graph, neighbour, node, dp); // Explore the child subtree
	      dp[node] += dp[neighbour]; // Add child's subtree size
	    }
  	}

---

## IN BINARY SEARCH ON ANSWER, HELPER FUNCTION CAN ALSO HAVE N^2 COMPLEXITY
--- 
## BFS TO FIND COMPONENTS IN A SIMPLE GRAPH
	List<List<Integer>> graph = new ArrayList<>();
	for(int i=0;i<n;i++) graph.add(new ArrayList<>());
	for(int i=0;i<n;i++){
		graph.get(arr[i]).add(i);
		graph.get(i).add(arr[i]);
	}
	boolean[] inTwoCycle = new boolean[n];
	for (int i = 0; i < n; i++) {
	      int j = arr[i];
	      if(arr[j] == i) inTwoCycle[i] = true;
	}
	int[] vis = new int[n];
	int compsWithPair = 0;
	for (int i = 0; i < n; i++){
	      if (vis[i] == 0) {
	        boolean hasPair = false;
	        Queue<Integer> queue = new LinkedList<>();
	        queue.add(i);
	        vis[i] = 1;
	        while (!queue.isEmpty()) {
	          int u = queue.poll();
	          if(inTwoCycle[u] == true) hasPair = true;
	          for (int v : graph.get(u)) {
	            if (vis[v] == 0) {
	              vis[v] = 1;
	              queue.add(v);
	            }
	          } 
	        }
	        if(hasPair) compsWithPair++;
	      }
	    }

---
## GCD PROPERTY -> GCD(a1 + bj, a2 + bj, a3 + bj, ____ , an + bj) = GCD(a1 + bj, a2 - a1, a3 - a1, ___ , an - a1)
---
## SLIDING WINDOW PROBLEM TRICK
- If in any problem you arrive at a condition where length of subarray = sum of subarray elements
- prefix[r] - prefix[l-1] = r - (l-1)
- try subtracting 1 from each element then problem reduces subarray with sum 0

---
## GRAPH PROBLEM TRICK
- When we are asked to minimize distances, and edge weight is not given, ALWAYS PREFER BFS WITH DISTANCE PARAMETER IN QUEUE TO DIJKSTRA
- In these problems if additional constraints are given **ADD EXTRA STATE IN VISITED ARRAY TO HANDLE THAT CONDITION**
	
    

    
    


