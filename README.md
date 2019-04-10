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


