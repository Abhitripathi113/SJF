# SJF
Scheduler using shortest job first scheduling and print the outlook of Gant chart on the computer screen

#include<stdio.h>
#include<string.h>
int main()
{

    int burst_time[20],arrival_time[10],number_of_process,waiting_time[10],turnaround_time[10],i,j,temp,st[10],ft[10];
    int total_wt=0,total_ta=0;
    float average_waiting_time,average_turnaround_time;
    char process_name[10][10],t[10];
   
    printf("\tEnter the number of process:");
    scanf("%d",&number_of_process);
    for(i=0; i<number_of_process; i++)
    {
        printf("\tEnter Process Name, Arrival Time and Burst Time:\n");
        
        scanf("%s%d%d",&process_name[i],&arrival_time[i],&burst_time[i]);
    }
