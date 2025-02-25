Download Link : https://programming.engineering/product/subroutines-and-calling-conventions-2/

# Subroutines-and-Calling-Conventions
Subroutines and Calling Conventions

1.1 Debugging Assembly

7.1 For information on debugging or the autograder, jump to the debugging section. Please note that Docker must be running, but it doesn’t need to be within the image.

1.2 Factorial

Given a value n, calculate the factorial by implementing the Factorial and Multiply Subroutines. Return the final answer. The pseudocode can be found in section 3.1.1.

Below is a list of what we have provided you for this method.

    label named “MULTIPLY” where the multiply subroutine begins

    label named “FACTORIAL” where the factorial subroutine begins

    label named “STACK” where the start of the stack is located

1.3 Insertion Sort

Given an array of integers, you will be tasked with implementing an insertion sort to put them in ascending order. The pseudocode can be found in section 3.2.1.

Below is a list of what we have provided you for this method.

    label named “INSERTION SORT” where the insertion sort subroutine begins

    label named “STACK” where the start of the stack is located

    values of the original array starting at x4000

1.4 Preorder Traversal

For this subroutine, you will write a subroutine to execute a preorder traversal on a binary tree and put the result into an array. The pseudocode can be found in section 3.3.1.

Below is a list of what we have provided you for this method.

    label named “PREORDER TRAVERSAL” where the preorder traversal subroutine begins

    label named “STACK” where the start of the stack is located

    the nodes of the binary tree with value, address of the left node, and address of the right node, starting at x4000

    the result array starting at x4020

1.5 Advice from your TAs

    More information on the LC-3 Calling Convention can be found on Canvas under Lab slides 9 and 10 and in Lecture Slides L10 and L11.

    More detailed information on each LC-3 instruction can be found in the Patt/Patel book Appendix A (also on Canvas under LC3 Resources).

    When converting pseudocode into assembly, become human compilers and translate one line of pseu-docode into one (or more) lines of assembly. One line at a time. Don’t look at the pseudocode and try to optimize things in your head and write the entire function. Trust us when we say translating one line at a time is the way. So, put on blinders. Ignore previous and future lines of code.

    Don’t assume a register still retains a value from a previous LD.

    Don’t assume the condition code reflects the register you think it does (NZP).

    Checkout the Appendix for helpful resources

    The local autograder is a shell script which should be run in your local terminal (not the docker terminal).

    Remember that this HW will be demoed. There will be an announcement soon over the demo details!

The above strategy ofcourse produces inefficient code. But, it produces correct assembly code, every time. Not clever code. Not optimized code. Not short code. But correct code. So, if you ever find it difficult to write assembly, just go at it one step at a time :)

psst..also you could come to office hours or post on ed discussion but definitely try that advice first :DD

    Overview

2.1 Purpose

Now that you’ve been introduced to assembly, think back to some high level languages you know such as Python or Java. When writing code in Python or Java, you typically use functions or methods. Functions and methods are called subroutines in assembly language.

In assembly language, how do we handle jumping around to different parts of memory to execute code from functions or methods? How do we remember where in memory the current function was called from (where to return to)? How do we pass arguments to the subroutine, and then pass the return value back to the caller?

The goal of this assignment is to introduce you to the Stack and the Calling Convention in LC-3 Assembly. This will be accomplished by writing your own subroutines, calling subroutines, and even creating subroutines that call themselves (recursion). By the end of this assignment, you should have a strong understanding of the LC-3 Calling Convention and the Stack Frame, and how subroutines are implemented in assembly language.

2.2 Task

You will implement each of the three subroutines (functions) listed below in LC-3 assembly language. Please see the detailed instructions for each subroutine on the following pages. The autograder checks for certain subroutine calls with arguments pushed in the correct order, so we suggest that you follow the provided algorithms when writing your assembly code. Your subroutines must adhere to the LC-3 calling convention.

    factorial.asm

    insertionSort.asm

    preorderTraversal.asm

Please read the TLDR (listed above) for more helpful resources. Please check the rest of this document for some advice on debugging your assembly code, as well some general tips for successfully writing assembly code.

The assignment is due by 11:59 PM on March 7th, 2023. You could also submit the assignment by March 8th, 2023 for a late penalty of 25% of your overall grade.

2.3 Criteria

Your assignment will be graded based on your ability to correctly translate the given pseudocode for sub-routines (functions) into LC-3 assembly code, following the LC-3 calling convention. Please use the LC-3 instruction set when writing these programs. Check the deliverables section for deadlines and other related information.

You must obtain the correct values for each function. In addition, registers R0-R5 and R7 must be restored from the perspective of the caller, so they contain the same values before and after the caller’s JSR call. Your subroutine must return to the correct point in the caller’s code, and the caller must find the return value on the stack where it is expected to be. If you follow the LC-3 calling convention correctly, each of these things will happen automatically.

While we will give partial credit where we can, your code must assemble with no warnings or errors. (Complx will tell you if there are any.) If your code does not assemble, we will not be able to grade that file and you will not receive any points. Each function is in a separate file, so you will not lose all points if one function does not assemble. Good luck and have fun!

    Detailed Instructions

3.1 Part 1

3.1.1 Factorial

The Factorial of a number is the product of that number and all of the numbers below it. In factorial.asm, we want you to implement two subroutines: MULTIPLY and FACTORIAL (see the following pseudocodes for more details). Note that the numbers that we will give you are strictly greater than or equal to 0. As a reminder, please do not change the names of provided subroutines. Otherwise, your submission will not pass the autograder.

For example:

factorial(0) should return 1

factorial(1) should return 1

factorial(2) should return 2

factorial(3) should return 6

3.1.2 Pseudocode

Here are the pseudocodes for these subroutines:

MULTIPLY(int a, int b) {

int ret = 0;

while (b > 0):

ret += a;

b–;

return ret;

}

FACTORIAL(int n) {

int ret = 1;

for (int x = 2; x <= n; x++) {

ret = MULTIPLY(ret, x);

}

return ret;

}

Note: since there are two loops in the MULTIPLY and FACTORIAL subroutines, make sure you use different label names for those loops. In general, you should not have two loops with the same name in the same program.

3.2 Part 2

3.2.1 Insertion Sort

For this part of this assignment, you will be implementing insertion sort on an array of integers in insertionSort.asm. As a reminder, please do not change the names of provided subroutines. Otherwise, your submission will not pass the autograder.

If you are unfamiliar with insertion sort and would like more information about it, see www.geeksforgeeks.

org/recursive-insertion-sort/.

3.2.2 Pseudocode

Here is the pseudocode for this subroutine:

INSERTION_SORT(int[] arr (addr), int length) {

if (length <= 1) {

return;

}

INSERTION_SORT(arr, length – 1);

int last_element = arr[length – 1];

int n = length – 2;

while (n >= 0 && arr[n] > last_element) {

arr[n + 1] = arr[n];

n–;

}

arr[n + 1] = last_element;

}

Let’s do an example of insertion sort in action and see how the array looks throughout our above algorithm!

2
	

3
	

1
	

1
	

6
	

Given
					

2
	

3
	

1
	

1
	

6
	

INSERTION SORT(arr, 4)
				

2
	

3
	

1
	

1
	

INSERTION SORT(arr, 3)
			

2
	

3
	

1
	

INSERTION SORT(arr, 2)
		

2
	

3
	

INSERTION SORT(arr, 1)

    Return

    3 last element movement=0

1
	

2
	

3
	

last element movement=2
					

1
	

1
	

2
	

3
	

last element movement=2
					

1
	

1
	

2
	

3
	

6
	

last element movement=0

3.3 Part 3

3.3.1 Preorder Traversal

For this part of the assignment, you will write a recursive traversal subroutine for a binary tree in preorderTraversal.asm. The parameters of the function are the tree’s root (provided as an address in memory), the array to store

the result in (also provided as an address in memory), and the index in the array to store the next result in. As a reminder, please do not change the names of provided subroutines or otherwise your submission will not pass the autograder.

If you are unfamiliar with the preorder traversal and would like more information about it, see www.

geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/.

3.3.2 Binary Tree Data Structure

The below figure has 3 parts (the actual tree, the memory layout of that tree, and the visualization of that tree) depicting how each node in our tree is laid out in our memory. Each node will have three attributes: its value, its left node, and its right node. Note that each node is treated as an address in memory.

Given some node that lives at address x:

    mem[x] = node.data

    mem[x + 1] = node.left

    mem[x + 2] = node.right

For example, x4000 holds the data of a node, x4001 holds the address of the left child of that node, and x4002 holds the address of the right child of that node. For a leaf node (a node with no child) such as node 8 in our example, x4008 holds the data and x4009 and x400A both hold 0 since node 8 has no child nodes.

See https://www.geeksforgeeks.org/binary-tree-data-structure/ for more information regarding bi-nary trees.

3.3.3 Pseudocode

Here is the pseudocode for this subroutine:

PREORDER_TRAVERSAL(Node root (addr), int[] arr (addr), int index) { if (root == 0) {

return index;

}

arr[index] = root.data;

index++;

index = PREORDER_TRAVERSAL(root.left, arr, index); return PREORDER_TRAVERSAL(root.right, arr, index);

}

*Note: 0 is equivalent to NULL

Let’s do an example of a preorder traversal in action on a binary tree and see how it builds our result array!

    Autograder

To run the autograder locally, follow the steps below depending on your operating system:

    Mac/Linux Users:

        Navigate to the directory your homework is in (in your terminal on your host machine, not in the Docker container via your browser)

        Run the command sudo chmod +x grade.sh

        Now run ./grade.sh

    Windows Users:

        In Git Bash (or Docker Quickstart Terminal for legacy Docker installations) navigate to the directory your homework is in

        Run chmod +x grade.sh

        Run ./grade.sh

Note: The checker may not reflect your final grade on this assignment. We reserve the right to update the autograder as we see fit when grading.

    Deliverables

Turn in the following files to Gradescope:

    factorial.asm

    insertionSort.asm

    preorderTraversal.asm

Note: Please do not wait until the last minute to run/test your homework. Last-minute turn-ins will result in long queue times for grading on Gradescope. You have been warned.

    Demos

This homework will be demoed. The demos will be ten minutes long and will occur IN PERSON.

Stay tuned for details as the due date approaches.

    Sign up for a demo time slot via Canvas before the beginning of the first demo slot. This is the only way you can ensure you will have a slot.

    If you cannot attend any of the predetermined demo time slots, e-mail the Head TA Sophie Imhof (simhof3@gatech.edu) before the week of demos.

    If you know you are going to miss your demo, you may cancel your slot on Canvas with no penalty, as long as you cancel 24 hours in advance. However, you are not guaranteed another time slot. If you cancel within 24 hours of your demo, it will be counted as a missed demo.

    Your overall homework score will be ((homework_score * 0.5) + (demo_score * 0.5)), meaning if you received a 90% on your homework, but a 30% on the demo, you would receive an overall score of 60%. If you miss your demo you will not receive any of these points, and the maximum you can receive on the homework is 50%.

    You will be able to make up one of your missed demos at the end of the semester for half credit.

