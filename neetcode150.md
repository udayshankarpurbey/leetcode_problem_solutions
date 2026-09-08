# NeetCode 150 

### 1. Two Sum

```ts
function twoSum(nums: number[], target: number): number[] {
    const remainder = new Map();

    for(let i = 0 ; i<nums.length;i++) {
        const cur = nums[i];
        const rem = target - cur;
        const s = remainder.get(cur)
        if(s != undefined) {
            return [i ,s];
        }
        remainder.set(rem , i)
    }
};
```

### 136. Single Number

```ts
function singleNumber(nums: number[]): number {
    let newNum : number | undefined ;
    nums.forEach((x : number) => newNum =x^newNum)
    return newNum == undefined ? 0 : Number(newNum)
};
```

### 191. Number of 1 Bits

```ts
function hammingWeight(n: number): number {
    return n.toString(2)?.replaceAll('0','')?.length
};
```

### 20. Valid Parentheses

```ts
function isValid(s: string): boolean {
    const bracketArray = [];

    for(let val of s) {
        if(val == '(' || val == '{' || val == '[') {
            bracketArray.push(val)
        } else {
            const match = bracketArray[bracketArray.length - 1] 
            
            switch (val) {
                case ')':
                    if (match !== '(') return false;
                    bracketArray.pop();
                    break;

                case '}':
                    if (match !== '{') return false;
                    bracketArray.pop();
                    break;

                case ']':
                    if (match !== '[') return false;
                    bracketArray.pop();
                    break;
            }
        }
    }
    return bracketArray.length == 0 ? true : false;
};
```

### 202. Happy Number

```ts
function isHappy(n: number): boolean {
    return numSquareSumAsNewNum(n , new Set<number>());
};

function numSquareSumAsNewNum(n : number , numberSet : Set<number>) : boolean{
    const nvalue = n.toString()
    let newValue = 0;
    for(let val of nvalue) {
        newValue += Number(val) * Number(val)
    }
        console.log(newValue , newValue === 1 ,numberSet)

    if(numberSet.has(newValue)) return false;
    if(newValue === 1) return true;

    numberSet.add(newValue);

    return numSquareSumAsNewNum(newValue , numberSet)
}
```

### 190. Reverse Bits

```ts
function reverseBits(n: number): number {
    const binaryBit = (n >>> 0).toString(2).padStart(32, '0');
    const reveserBinaryBit = binaryBit.split('').reverse().join('');
    return parseInt(reveserBinaryBit , 2) || 0;
};
```

### 217. Contains Duplicate

```ts
function containsDuplicate(nums: number[]): boolean {
    const numMap = new Set();
    for(let num of nums) {
        if(!numMap.has(num)) {
            numMap.add(num)
        } else {
            return true;
        }
    }
    return false;
};
```

### 70. Climbing Stairs

```ts
function climbStairs(n: number): number {
    const climbStairMap = new Map();
    for(let i = 0 ; i<= n ; i++) {
        if(i == 0 || i == 1){
            climbStairMap.set(i,1)
        } else {
            climbStairMap.set(i , (climbStairMap.get((i- 2)) + climbStairMap.get((i- 1))))
        }
    }
    return n >= 2?(climbStairMap.get((n- 2)) + climbStairMap.get((n- 1))) : 1
};
```

### 66. Plus One

```ts
function plusOne(digits: number[]): number[] {
    let numberString = '';
    const numberArray = [];
    for(let num of digits) {
        numberString += num
    }
    const number : string =( BigInt(numberString) + BigInt(1) ).toString();
    for(let n of number) {
        numberArray.push(Number(n))
    }
    return numberArray
};
```

### 268. Missing Number

```ts
function missingNumber(nums: number[]): number {
    const numSet = new Set(nums)
    for(let i = 0; i<=nums.length ; i++) {
        if(!numSet.has(i)) return i
    }
};
```

### 242. Valid Anagram

```ts
function isAnagram(s: string, t: string): boolean {
    if(s.length !== t.length) return false ;
    const sWithTheirLength = new Map();
    const tWithTheirLength = new Map();

    for (let i = 0; i<s.length; i++ ) {
        const sLetter =  s[i] ;
        const tLetter = t[i] ;

        if(sWithTheirLength.has(sLetter)) {
            sWithTheirLength.set(
                sLetter , sWithTheirLength.get(sLetter) + 1
            )
            
        } else {
            sWithTheirLength.set(
                sLetter , 1
            )
        }
        

         if(tWithTheirLength.has(tLetter)) {
            tWithTheirLength.set(
                tLetter , tWithTheirLength.get(tLetter) + 1
            )
            
        } else {
            tWithTheirLength.set(
                tLetter , 1
            )
        }
    } 

    for (const s of sWithTheirLength.keys()) {
        if(tWithTheirLength.get(s) !== sWithTheirLength.get(s)) return false
    }

    return true;
};
```

### 206. Reverse Linked List

```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
    const numberList = getListValue(head , [])
    addValueInList(head , numberList , (numberList.length - 1));
    return head;
};

function getListValue(head: ListNode | null , data) : number[] {
    if(head === null) return data;
    data.push(head.val);
    if(head.next === null) return data;
    return getListValue(head.next , data)
}

function addValueInList(head: ListNode | null , data : number[] , dataLength : number) {
    if(head === null) return null;
    head.val = data[dataLength];
    data.pop();
    if(head.next === null) return null;
    return addValueInList(head.next , data ,(dataLength - 1) )
}
```

### 104. Maximum Depth of Binary Tree

```ts
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function maxDepth(root: TreeNode | null): number {
    return getNextNodevalue(root , 0);
};

function getNextNodevalue(root: TreeNode | null ,maxDepth : number) : number  {
    if(root === null ) return maxDepth;

    maxDepth += 1;
    
    if(root.left === null &&  root.right === null) return maxDepth;

    return Math.max(
        getNextNodevalue(root.left , maxDepth),
        getNextNodevalue(root.right , maxDepth)
    );

}
```

### 763. Partition Labels

```ts
type StringInfo = {
  isDuplicate: boolean;
  maxPosition: number;
};

function partitionLabels(s: string): number[] {
    const stringWithTheirPosition  = new Map<string , StringInfo>();

    for(let i = 0 ; i<s.length ; i++) {
        const val : string = s[i];
        if( stringWithTheirPosition.has(val)) {
            stringWithTheirPosition.set(val , {isDuplicate : true ,maxPosition : i  })

        } else {
            stringWithTheirPosition.set(val , {isDuplicate : false , maxPosition : i})
        }        
    }

    const partitionStringArray : number[] = [];
    let partitionMaxPosition : number = 0;
    let currentString : string = '';

    for(let i = 0 ; i<s.length ; i++) {
        const val : string = s[i];
        const sValue : StringInfo = stringWithTheirPosition.get(val)
        currentString += val;
        if(sValue.isDuplicate)  {
            partitionMaxPosition = Math.max(sValue.maxPosition , partitionMaxPosition)
        }

        if(partitionMaxPosition <= i) {
            partitionStringArray.push(currentString.length);
            currentString = ''
        }
        
    }

    return partitionStringArray;
    
};
```

### 78. Subsets

```ts
function subsets(nums: number[]): number[][] {
    return generateAllSubsets(nums)
};


function generateAllSubsets(num: number[] , subsets :number [][] =[[]]): number[][] {
    const subsetLength : number = subsets.length
    const numLength : number = num.length;
    
    for(let i = 0 ; i< subsetLength ; i++) {
        subsets.push([...subsets[i] ,num[0]])
    }
        
    if(numLength > 1) return generateAllSubsets(num.slice(1) , subsets)
    
    return subsets
}
```

### 7. Reverse Integer

```ts
function reverse(x: number): number {
    const safeInt32 = (2 ** 31);
    if (x < -safeInt32 || x > safeInt32 - 1) return 0;    
    const reversedVal = (x >= 0) ? Number(x.toString().split('').reverse().join('')) : (Number((x * -1 ).toString().split('').reverse().join('')) * -1)
    return (reversedVal < -safeInt32 || reversedVal > safeInt32 - 1) ? 0 : reversedVal
};
```

### 90. Subsets II

```ts
function subsetsWithDup(nums: number[]): number[][] {
    const subSets : number[][] = [[]]
    const subsetSet = new Set();
    for(let num of nums.sort()) {
        const numberSubset = [];
        for(let ss of subSets) {
            const key = [...ss , num]
            if(!subsetSet.has(key.join('')))  {
                numberSubset.push(key)
                subsetSet.add(key.join(''))
            }
        }
        subSets.push(...numberSubset)
    }
    return [...new Set([...subSets])]
};
```

### 167. Two Sum II - Input Array Is Sorted

```ts
function twoSum(numbers: number[], target: number): number[] {
    const remainerTarget = new Map();

    for(let i = 0 ; i<numbers.length; i++) {
        const num = numbers[i];
        const reaminder = target - num 
        if(remainerTarget.has(num)) {
            return [(remainerTarget.get(num) + 1),(i + 1)]
        }
        else {
            remainerTarget.set(reaminder , i)
        }
    }
};
```

```ts
function twoSum(numbers: number[], target: number): number[] {
    const remainderMap = new Map();
    for(let i = 0; i<numbers.length; i++) {
        const num = numbers[i];
        if(remainderMap.has(num)) return[remainderMap.get(num),i+1];

        remainderMap.set((target - num) , i+1);
    }

    return [];
}
```

### 647. Palindromic Substrings

```ts
function countSubstrings(s: string): number {

    let subStringCount = 0;

    const stringLength = s.length;

    for (let i = 0; i < stringLength; i++) {
        if (i === 0) {
            subStringCount += stringLength;
            continue;
        }

        let left = 0;
        let right = 0 + i;
        while (right < stringLength) {
            // const sub = s.slice(left , right + 1);
            if (isPalindrome(s, left, right)) subStringCount++;
            left++;
            right++;
        }
    }

    return subStringCount;
}

function isPalindrome(s: string, l: number, r: number): boolean {
    if (!s) return false;
    if (l === r) return true;
    let left = l;
    let right = r;

    while (left < right) {
        if (s[left] !== s[right]) return false;
        else {
            left++;
            right--;
        }
    }

    return true;
}
```

### 2. Add Two Numbers

```ts


function addTwoNumbers(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    return sumOfNodes(l1 , l2 , 0 );
    
};

function sumOfNodes(l1: ListNode | null, l2: ListNode | null , carry : number ) :  ListNode | null {
    if(l1 === null && l2 === null && carry === 0) return null;
    
    const node = new ListNode();

    const l1Val = l1 ? l1.val : 0;
    const l2Val = l2 ? l2.val : 0;

    const next1 = l1 ? l1.next : null;
    const next2 = l2 ? l2.next : null;

    const val = l1Val + l2Val + carry;

    node.val = val % 10;
    carry = Math.floor(val / 10);

    node.next = sumOfNodes(next1 , next2, carry)
    return node;
}
```

### 100. Same Tree

```ts
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    
     if (p === null && q === null) {
        return true;
    }

    if (p === null || q === null) {
        return false;
    }

    if (p.val !== q.val) {
        return false;
    }

    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
};
```

### 49. Group Anagrams

```ts
function groupAnagrams(strs: string[]): string[][] {

    const charArray = new Array(26).fill(0)
    const charCodeofa = "a".charCodeAt(0);
    const stringWithItsFrequencyCode = new Map()

    for (let str of strs) {
        for (let char of str) {
            const charCodeOfCharater = char.charCodeAt(0);
            const diff = charCodeOfCharater - charCodeofa;
            charArray[diff] = charArray[diff] + 1;
        }
        const frequency = charArray.join('*');
        if (stringWithItsFrequencyCode.has(frequency)) {
            stringWithItsFrequencyCode.set(frequency, [...stringWithItsFrequencyCode.get(frequency), str])
        } else {
            stringWithItsFrequencyCode.set(frequency, [str])
        }
        charArray.fill(0);
    }
    const group = [];
    stringWithItsFrequencyCode.forEach((value) => group.push(value) )

    return group

};
```

### 347. Top K Frequent Elements

```ts
function topKFrequent(nums: number[], k: number): number[] {
    const numWithFrequency = new Map();

    for(let num of nums) {
        if(numWithFrequency.has(num)) {
            numWithFrequency.set(num , numWithFrequency.get(num) + 1)
        } else {
            numWithFrequency.set(num , 1)
        }
    }
    return [...numWithFrequency].sort((a : number[] , b : number[]) =>  b[1] - a[1]).slice(0,k).map((a : number[] ) => a[0])
};
```

### 128. Longest Consecutive Sequence

```ts
function longestConsecutive(nums: number[]): number {
     if (nums.length < 1) return 0;
    if (nums.length === 1) return 1;

    let maxLongestSequence = 1;
    let currentSequence = 1;
    nums.sort((a: number, b: number) => a - b);
    let left = 0;
    let right = 1;

    while (left < right) {
        if(nums[right] ===undefined) return maxLongestSequence;

        if (nums[left] === nums[right]) { right++; continue }

         if (nums[left] + 1 === nums[right]) {
            currentSequence++;
            left = right;
            right = right + 1;
        } else {
            maxLongestSequence = maxLongestSequence<currentSequence ?currentSequence: maxLongestSequence;
            currentSequence = 1;
            left = right;
            right = right + 1;
        }

        if(maxLongestSequence<currentSequence) {
            maxLongestSequence = currentSequence;
        }
    }
    return maxLongestSequence;
};
```

### 238. Product of Array Except Self

```ts
function productExceptSelf(nums: number[]): number[] {

    const productOfNumbers = nums.reduce((acc : number , curr : number ) => (acc*= curr) , 1);
    return nums.map((num : number , index : number) => {
        if(num == 0) {
            const sum = nums.reduce((total, currentValue, currentIndex) => {
                if (currentIndex === index) {
                    return total; 
                }

                return total * currentValue;
            }, 1);
           
            return sum;
        }
        return productOfNumbers/num
    });  
};
```

### 48. Rotate Image

## solution 1 

```ts
function rotate(matrix: number[][]): void {
    const rotatedMatrix = [];

    for (let i = 0; i < matrix.length; i++) {
        const row = [];
        for (let j = 0; j < matrix.length; j++) {
            row.push(matrix[j][i])
        }
        rotatedMatrix.push(row.reverse())
    }

    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix.length; j++) {
            matrix[i][j] = rotatedMatrix[i][j]
        }
    }
};
```

## solution 2 

```ts
function rotate(matrix: number[][]): void {
    const len = matrix.length;
    matrix.forEach((row : number[]) => row.reverse());
    for(let i = 0; i < len ;i++) {
        for(let j= 0; j < len - i ; j++) {
            const temp = matrix[i][j];
            matrix[i][j] = matrix[len - 1 - j][len- 1 - i];
            matrix[len - 1 - j][len- 1 - i] = temp;
        }
    }
}
```

### 3870. Count Commas in Range

```ts
function countCommas(n: number): number {
    if(n<999) return 0;
    return n-999;
};
```