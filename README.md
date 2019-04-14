# SJF
Scheduler using shortest job first scheduling and print the outlook of Gant chart on the computer screen


#include <stdio.h>
#include <stdlib.h>
#define MAXIMUM_PROCESS 100

struct process {
    int pid;
    int b_time;
    int w_time;
};

typedef struct process Process;

double ave_wtime;
int tot_wtime;

void sort_btime(Process p[], int a);
void calc_wtime(Process p[], int a);
void gant_c(Process p[], int a);

int main()
{
    Process p[MAXIMUM_PROCESS];
    int a, i, j;
    puts("\n\n\t\tSHORTEST JOB FIRST SCHEDULING ALGORITHM \n");

    printf("\t\tEnter total process: ");
    scanf("%d", &a);
    printf("\t\tEnter burst time for each process:\n");
    for(i=0; i<a; i++) {
        printf("\t\tP[%d]: ", i+1);
        scanf("%d", &p[i].b_time);
        p[i].pid = i+1;
    }

    sort_btime(p, a);
    calc_wtime(p, a);

    ave_wtime = (double) ( (double)tot_wtime / (double) a );

    puts("");
    printf("\t\tAverage Waiting Time: %.2lf\n",ave_wtime);

    printf("\t\tGantt Chart:\n");
    gant_c(p, a);


    return 0;
}

void sort_btime(Process p[], int a)
{
    int i, j;
    Process temp;
    for(i=0; i<a-1; i++) {
        for(j=0; j<a-1-i; j++) {
            if(p[j].b_time > p[j+1].b_time) {
                temp = p[j];
                p[j] = p[j+1];
                p[j+1] = temp;
            }
        }
    }
}

void calc_wtime(Process p[], int n)
{
    int i;
    tot_wtime = 0;
    p[0].w_time = 0;
    for(i=1; i<n; i++) {
        p[i].w_time = p[i-1].w_time + p[i-1].b_time;
        tot_wtime += p[i].w_time;
    }
}

void gant_c(Process p[], int n)
{
    int i, j;
    int last = p[n-1].b_time + ( n== 1 ? 0 : p[n-1].w_time);
    // for upper line
    printf(" ");
    for(i=0; i<n; i++) {
        for(j=0; j<p[i].b_time; j++) printf("--");
        printf(" ");
    }
    
    printf("\n|");

 // for middle line
    for(i=0; i<n; i++) {
        for(j=0; j<p[i].b_time-1; j++) printf(" ");
        printf("p%d", p[i].pid);
        for(j=0; j<p[i].b_time-1; j++) printf(" ");
        printf("|");
    }
    
    printf("\n ");
    
    // for bottom line
    for(i=0; i<n; i++) {
        for(j=0; j<p[i].b_time; j++) printf("--");
        printf(" ");
    }
    
    printf("\n");

    // printing waiting time
    int minus = 0;
    for(i=0; i<n; i++) {
        if(p[i].w_time>9) printf(" ");
        printf("%d", p[i].w_time);
        if(p[i+1].w_time>9){
          minus = 1;
        }
        
        if(i+1 == n )  if (last>9) minus = 1;
        for(j=0; j<p[i].b_time-minus; j++) printf("  ");

    }
    if(last>9) printf(" ");
    printf("%d\n", last);
}
