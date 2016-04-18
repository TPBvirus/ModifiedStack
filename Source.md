# ModifiedStack
//Language: Java
//Class substitute for Java Stack Class. Generic Implementation.

package datastructures_lab.pkg6;
import java.util.Stack;

public class ModifiedStack<T> implements StackInterface<T>{
    public Stack<T> currentStack;
    public int numberOfEntries;
    
    public ModifiedStack(){//makes a new stack
        Stack<T> newStack = new Stack<>();
        currentStack = newStack;
    }
    
    public int getNumberOfEntries(){
        return numberOfEntries;
    }
    
    //overrides for stackInterface
    @Override
    public void push(T DataHere){
        currentStack.push(DataHere);
        numberOfEntries++;
    }
    @Override
    public T pop(){
        return currentStack.pop();
    }
    @Override
    public void peek(){
        currentStack.peek();
    }
    @Override
    public boolean isEmpty(){
        return numberOfEntries == 0;
    }
    
    // Displays the content of the stack selected without altering stack contents
    public void displayContent(){
        @SuppressWarnings("Unchecked")//suppress warning for the array
        T[] saveArray = (T[])new Object[numberOfEntries];//create new array of objects
        int i = 0;
        
        while (currentStack.isEmpty() != true){// pops values from stack and saves them in an array
            saveArray[i] = currentStack.pop();
            System.out.println(saveArray[i]);
            i++;
        }
        i = i-1; //reset index
        while(i >= 0){//pushs values back into the stack from the array
            currentStack.push(saveArray[i]);
            i--;
        }
    }
    
    /* checkReverse() Compares the passed stack to the current stack reversed to see if they are equal.
     * @param comparedStack
     * @return Boolean
        */
    public boolean checkReverse(ModifiedStack<T> comparedStack){
        boolean result = true; //result
        Object[] comparedArray;
        Object[] thisArray;
        comparedArray = comparedStack.toArray();
        thisArray = this.toArray();
        for(int i = 0; i < thisArray.length/2; i++){ //thisArray reversed/returned to original stack order
            Object temp;
            temp = thisArray[i];
            thisArray[i] = thisArray[thisArray.length - i - 1];
            thisArray[thisArray.length - i - 1] = temp;
        }
        
        for(int i = 0; i < comparedArray.length; i++){//check against the comparedArray
            if(comparedArray[i].equals(thisArray[i]) == false){ //if false
                result = false; //make result false
                break; 
            }
        }
        return result;
    }
    
    /* @return T[]
        Converts values of the current stack into array without the order of the objects
        in the stack being changed.*/
    public T[] toArray(){
        @SuppressWarnings("Unchecked")//suppress warning for the array
        T[] saveArray = (T[])new Object[numberOfEntries];//create new array of objects
        int i = 0;
        
        while (currentStack.isEmpty() != true){// pops values from stack and saves them in an array
            saveArray[i] = currentStack.pop();
            i++;
        }
        i = i-1; //reset index
        while(i >= 0){//pushes values back into the stack from the array
            currentStack.push(saveArray[i]);
            i--;
        }
        return saveArray;
    }
    
    //Test Methods to be Run in Main
    
    public void testReverse(ModifiedStack<T> passed){
        System.out.println("\nTesting checkReverse() method in class OurStack");
        if(this.checkReverse(passed) == true){
            System.out.println("checkReverse returned true. Current Stack == Passed Stack reversed.");
        }
        else
            System.out.println("checkReverse returned false. Current Stack != Passed Stack reversed.");
    }
    
}
//end ModifiedStack Class
