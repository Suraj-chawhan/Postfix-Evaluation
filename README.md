#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Stack {
    int top;
    int size;
    int* arr;
};

void Push(struct Stack* sp,char n) {
    sp->top++;
    sp->arr[sp->top]=n;
}
int Pop(struct Stack* sp) {
    sp->top--;
    return sp->arr[sp->top];
}

int Postfix(char hunny[]) {
    int n=strlen(hunny);
    struct Stack* sp=(struct Stack*)malloc(sizeof(struct Stack));
    sp->size=10;
    sp->top=-1;
    sp->arr=(int*)malloc(sp->size*sizeof(int));

    int i;
    for(i=0; i<n; i++)
    {
        if(hunny[i]>='0' && hunny[i]<='9') {
            Push(sp,hunny[i]-'0');
        }
        else {
            int val2=sp->arr[sp->top];
            Pop(sp);
            int val1=sp->arr[sp->top];
            Pop(sp);

            switch(hunny[i]) {
            case '*' :
                Push(sp,val2*val1);
                break;
            case '+' :
                Push(sp,val1+val2-'0');
                break;
            case '-' :
                Push(sp,val2-val1);
                break;
            case '/' :
                Push(sp,val1/val2);
                break;
            }

        }

    }



    return sp->arr[sp->top];




}




int main() {
    char hunny[]="12+";
    printf("%d",Postfix(hunny));




}
