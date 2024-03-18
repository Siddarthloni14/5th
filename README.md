# 5th5. Develop a Program in C for the following Stack Applications
a. Evaluation of Suffix expression with single digit operands and operators: +, -, *, /, %, ^



#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <ctype.h>
#include <math.h>

#define MAX_SIZE 100

// Stack structure
struct Stack {
    int items[MAX_SIZE];
    int top;
};

// Function prototypes
void initializeStack(struct Stack *s);
bool isEmpty(struct Stack *s);
bool isFull(struct Stack *s);
void push(struct Stack *s, int value);
int pop(struct Stack *s);
int evaluatePostfix(char *postfix);

int main() {
    char postfix[MAX_SIZE];

    // Input postfix expression
    printf("Enter postfix expression: ");
    scanf("%s", postfix);

    // Evaluate postfix expression
    int result = evaluatePostfix(postfix);

    // Output result
    printf("Result: %d\n", result);

    return 0;
}

// Function to initialize stack
void initializeStack(struct Stack *s) {
    s->top = -1;
}

// Function to check if the stack is empty
bool isEmpty(struct Stack *s) {
    return s->top == -1;
}

// Function to check if the stack is full
bool isFull(struct Stack *s) {
    return s->top == MAX_SIZE - 1;
}

// Function to push an element onto the stack
void push(struct Stack *s, int value) {
    s->items[++s->top] = value;
}

// Function to pop an element from the stack
int pop(struct Stack *s) {
    return s->items[s->top--];
}

// Function to evaluate postfix expression
int evaluatePostfix(char *postfix) {
    struct Stack stack;
    initializeStack(&stack);
    int i = 0;

    while (postfix[i] != '\0') {
        char token = postfix[i];

        if (isdigit(token)) {
            push(&stack, token - '0');
        } else if (token == '+' || token == '-' || token == '*' || token == '/' || token == '%' || token == '^') {
            int operand2 = pop(&stack);
            int operand1 = pop(&stack);
            int result;

            switch (token) {
                case '+':
                    result = operand1 + operand2;
                    break;
                case '-':
                    result = operand1 - operand2;
                    break;
                case '*':
                    result = operand1 * operand2;
                    break;
                case '/':
                    result = operand1 / operand2;
                    break;
                case '%':
                    result = operand1 % operand2;
                    break;
                case '^':
                    result = (int)pow(operand1, operand2);
                    break;
            }

            push(&stack, result);
        }
        i++;
    }

    return pop(&stack);
}
