# DSA

## Data Structures and Algorithms

### **Time Taken vs. Time Complexity**

- **Time taken** refers to the actual duration an algorithm takes to execute on a specific input and hardware.
- **Time complexity** is a theoretical measure of how the runtime of an algorithm increases as the input size grows. It helps compare algorithms independently of hardware or implementation details.

**Time Complexity (TC):**

- Expressed using Big O notation, e.g., $O(n)$, which describes the upper bound of the algorithm's growth rate.
- Focuses on the worst-case scenario unless stated otherwise.
- Ignores constant factors and lower-order terms to highlight scalability.

![image](https://github.com/user-attachments/assets/b4371071-ae40-4fa5-9075-3665896e2fce)

- O(15) = 5x3 or O(Nx3) or O(3N)

![image](https://github.com/user-attachments/assets/a59102d6-ce19-49f3-bbc7-948cd4000fad)

**Key Points:**

1. Time complexity is usually analyzed for the worst-case input.
2. Constants and less significant terms are omitted for clarity.
3. Big O notation provides a high-level understanding of algorithm efficiency.

## Space Complexity

- **Space complexity** measures the total memory an algorithm uses as a function of input size.
- Total space complexity = Auxiliary space + Input space.
  - **Auxiliary space:** Extra or temporary memory used by the algorithm (excluding input).
  - **Input space:** Memory required to store the input data.
- Space complexity is also represented using Big O notation (e.g., $O(n)$).
- ![image](https://github.com/user-attachments/assets/a885c6a7-8998-4a1e-8481-6acba8f42c8d)

## PRO TIP

Avoid modifying the input data directly. Work with copies or use auxiliary structures when necessary.
