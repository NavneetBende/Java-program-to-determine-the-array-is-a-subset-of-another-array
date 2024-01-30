Array is a subset of another array in Java
In this section we will determine the program to find if an Array is a subset of another array in Java which is discussed here. If all the elements of array 2 are found in array 1, then array 2 is said to be a subset of array 1.

Array is subset of another array
Example
arr1 = {1,2,3,4,5}  , arr2 = {3,4,5}
arr2 is a subset of arr1 (As, arr1 contains all the elements of arr2)
arr3 = {1,2,3,4,5}   arr4 = {1,2,9}
arr4 is not a subset of arr3 (As, arr3 do not contains all the elements of arr4).
Method Discussed :
Method 1 : Using nested loops
Method 2 : Using sorting and binary search.
Method 3 : Using sorting and merging.
Method 4 : Using Hashing
Method 1 :
Run a loop for loo from index 0 to length of arr2
Run a inner loop from index 0 to length of arr2
If(arr2[i]==arr1[j]), then break the inner loop
Check if(j==m) then return 0.
Otherwise, return 1.
Method 1 : Code in Java
class Main{

   static boolean isSubset(int arr1[], int arr2[], int m, int n)
    {
        int i = 0;
        int j = 0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < m; j++) {
                if (arr2[i] == arr1[j])
                    break;
            }
 
            if (j == m)
            return false;
        }
 
        return true;
    }
 
    public static void main(String args[])
    {
        int arr1[] = { 11, 10, 13, 21, 30, 70 };
        int arr2[] = { 11, 30, 70, 10 };
    
        int m = arr1.length;
        int n = arr2.length;
 
        if (isSubset(arr1, arr2, m, n))
            System.out.print("arr2[] is subset of arr1[] ");
        else
            System.out.print("arr2[] is not subset of arr1[] ");
 
    }
}
Output :
arr2[] is subset of arr1[]
Related Pages
Find maximum product sub-array in a given array

Finding Arrays are disjoint or not

Determine can all numbers of an array be made equal

Finding Minimum sum of absolute difference of given array

Sort an array according to the order defined by another array 

Method 2 :
In this method we first sort arr1 then, using binary search we find the elements of arr2 in arr1

Sort arr1[] using inbuilt sort function.
For each element of arr2[], do binary search for it in sorted arr1[].
If the element is not found then return 0.
If all elements are present then return 1.
Method 2 : Code in Java
import java.util.Arrays;
class Main{

   static boolean isSubset(int arr1[], int arr2[], int m, int n)
    {
        int i = 0;
 
        for (i = 0; i < n; i++) {
            if (binarySearch(arr1, 0, m - 1, arr2[i]) == -1)
                return false;
        }
 
        return true;
    }
 
    static int binarySearch(int arr[], int low, int high, int x)
    {
        if (high >= low)
        {
            /*low + (high - low)/2;*/
            int mid = (low + high)/ 2;
 
            if ((mid == 0 || x > arr[mid - 1])&& (arr[mid] == x))
                return mid;
            else if (x > arr[mid])
                return binarySearch(arr,(mid + 1), high,x);
            else
                return binarySearch(arr, low,(mid - 1), x);
        }
        return -1;
    }
    public static void main(String args[])
    {
        int arr1[] = { 11, 10, 13, 21, 30, 70 };
        int arr2[] = { 11, 30, 70, 10 };
    
        int m = arr1.length;
        int n = arr2.length;
        
        Arrays.sort(arr1);
 
        if (isSubset(arr1, arr2, m, n))
            System.out.print("arr2[] is subset of arr1[] ");
        else
            System.out.print("arr2[] is not subset of arr1[] ");
 
    }
}
Output :
arr2[] is subset of arr1[]
Method 3 :
Sort both arrays: arr1[] and arr2[] using inbuilt sort function.
Use Merging process to see if all elements of sorted arr2[] are present in sorted arr1[].
Method 3 : Code in Java
import java.util.Arrays;
class Main{

   static boolean isSubset(int arr1[], int arr2[], int m, int n)
    {
        int i = 0, j = 0;
 
        if (m < n)
            return false;
 
        Arrays.sort(arr1); // sorts arr1
        Arrays.sort(arr2); // sorts arr2
 
        while (i < n && j < m) {
            if (arr1[j] < arr2[i])
                j++;
            else if (arr1[j] == arr2[i]) {
                j++;
                i++;
            }
            else if (arr1[j] > arr2[i])
                return false;
        }
 
        if (i < n)
            return false;
        else
            return true;
    }
 
    
    public static void main(String args[])
    {
        int arr1[] = { 11, 10, 13, 21, 30, 70 };
        int arr2[] = { 11, 30, 70, 10 };
    
        int m = arr1.length;
        int n = arr2.length;
        
        if (isSubset(arr1, arr2, m, n))
            System.out.print("arr2[] is subset of arr1[] ");
        else
            System.out.print("arr2[] is not subset of arr1[] ");
 
    }
}
Output :
arr2[] is subset of arr1[]
Method 4 :
In this method we will use the concept of hashing.

Method 4 : Code in Java
import java.util.Arrays;
import java.util.HashSet;
class Main{

   static boolean isSubset(int arr1[], int arr2[], int m, int n)
    {
        HashSet set = new HashSet<>();
 
        for (int i = 0; i < m; i++) {
            if (!set.contains(arr1[i]))
                set.add(arr1[i]);
        }
 
        
        for (int i = 0; i < n; i++)
        {
            if (!set.contains(arr2[i]))
                return false;
        }
        return true;
    }
 
    
    public static void main(String args[])
    {
        int arr1[] = { 11, 10, 13, 21, 30, 70 };
        int arr2[] = { 11, 30, 70, 10 };
    
        int m = arr1.length;
        int n = arr2.length;
        
        if (isSubset(arr1, arr2, m, n))
            System.out.print("arr2[] is subset of arr1[] ");
        else
            System.out.print("arr2[] is not subset of arr1[] ");
 
    }
}
Output :
arr2[] is subset of arr1[]
