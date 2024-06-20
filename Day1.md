### Find the minimum element in the array
### Find the maximum element in the array
### Find the Sum of odd Elements in the array
### Find the Sum of even Elements in the array

```java
import java.util.Scanner;
public class Main
{
	public static void main(String[] args) {
	    try(Scanner sc = new Scanner(System.in)){
	       boolean flag = true;
	       int []Array = new int[1];
            int n = 0;
	       while(flag){
	           System.out.println("Menu");
	           System.out.println("1] Accept array elements");
	           System.out.println("2] Find maximum of the array");
	           System.out.println("3] Find minimum of the array");
	           System.out.println("4] Find sum of odd numbers of the array");
	           System.out.println("5] Find sum of even numbers of the array");
	           System.out.println("6]exit");
    	       System.out.println("Enter choice");
	           int choice = sc.nextInt();
	           
	           switch(choice){
	               case 1:
	                   n = sc.nextInt();
                       Array  = new int[n];
                        for(int i=0;i<n;i++){
                        Array[i] = sc.nextInt();
                        }
	                   break;
                   case 2:
                        System.out.println("maximum in the array is : "+maximun(Array,n));
                       break;
	               case 3:
                        System.out.println("minimum in the array is : "+minimun(Array,n));
	                   break;
                   case 4:
                        System.out.println("odd sum is : "+oddSum(Array,n));
                       break;
                   case 5:
                        System.out.println("even sum is : "+evenSum(Array,n));
                       break;
                   case 6:
                       flag = false;
                       break;
	           }
    	   
	       } 
	    }catch(RuntimeException e){
	        e.printStackTrace();
	    }
	}
	public static int maximun(int []array , int size){
	    int maximum_ele = Integer.MIN_VALUE;
	    for(int i=0;i<size;i++){
	        if(maximum_ele<array[i]){
	            maximum_ele = array[i];
	        }
	    }
	    return maximum_ele;
	}
	public static int minimun(int []array , int size){
	    int maximum_ele = Integer.MAX_VALUE;
	    for(int i=0;i<size;i++){
	        if(maximum_ele>array[i]){
	            maximum_ele = array[i];
	        }
	    }
	    return maximum_ele;
	}
	public static int oddSum(int []array , int size){
	    int sum = 0;
	    for(int i=0;i<size;i++){
	        if(array[i]%2==0){
	            sum += array[i];
	        }
	    }
	    return sum;
	}
	public static int evenSum(int []array , int size){
	    int sum = 0;
	    for(int i=0;i<size;i++){
	        if(array[i]%2==1){
	            sum += array[i];
	        }
	    }
	    return sum;
	}

}
```