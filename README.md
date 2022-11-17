# oslabcheating
//os-lab
#even odd
read -p "Enter a number: " number
if [ $((number%2)) -eq 0 ]
then
  echo "Number is even."
else
  echo "Number is odd."
fi


//factorial
num=5
factorial=1
 
counter=$num
 
while [[ $counter -gt 0 ]]; do
   factorial=$(( $factorial * $counter ))
   counter=$(( $counter - 1 ))
done
 
echo $factorial




//fibonacci
//N=6
# Fibonacci Series
a=0
b=1
echo "The Fibonacci series is : "
for (( i=0; i<N; i++ ))
do
    echo -n "$a "
    fn=$((a + b))
    a=$b
    b=$fn
done



//switch
echo -n "Enter the name of a country: "
read COUNTRY

echo -n "The official language of $COUNTRY is "

case $COUNTRY in

  Lithuania)
    echo -n "Lithuanian"
    ;;

  Romania | Moldova)
    echo -n "Romanian"
    ;;

  Italy | "San Marino" | Switzerland | "Vatican City")
    echo -n "Italian"
    ;;

  *)
    echo -n "unknown"
    ;;
esac



//priority
using namespace std;
struct Process{
int pid;
int bt;
int priority;
};
bool comparison(Process a, Process b){
return (a.priority > b.priority);
}
void findWaitingTime(Process proc[], int n,int wt[]){
wt[0] = 0;
for (int i = 1; i < n ; i++ )
wt[i] = proc[i-1].bt + wt[i-1] ;
}
void findTurnAroundTime( Process proc[], int n, int wt[], int
tat[]){
for (int i = 0; i < n ; i++)
tat[i] = proc[i].bt + wt[i];
}
void findavgTime(Process proc[], int n){
int wt[n], tat[n], total_wt = 0, total_tat = 0;
findWaitingTime(proc, n, wt);
cout << "\nProcesses "<< " Burst time "<< " Waiting time "
<< " Turn around time\n";
for (int i=0; i<n; i++){
total_wt = total_wt + wt[i];
total_tat = total_tat + tat[i];
cout << " " << proc[i].pid << "\t\t"
<< proc[i].bt << "\t " << wt[i]
<< "\t\t " << tat[i] <<endl;
}
cout << "\nAverage waiting time = "<< (float)total_wt /
(float)n;
cout << "\nAverage turn around time = "<< (float)total_tat
/ (float)n<<endl;
}
void priorityScheduling(Process proc[], int n){
sort(proc, proc + n, comparison);
cout<< "Order in which processes gets executed \n";
for (int i = 0 ; i < n; i++)
cout << proc[i].pid <<" " ;
findavgTime(proc, n);
}
int main(){
Process proc[] = {{1, 10, 2}, {2, 5, 0}, {3, 8, 1}};
int n = sizeof proc / sizeof proc[0];
priorityScheduling(proc, n);
return 0;
}

//fifo
#include<stdio.h>
void findWaitingTime(int processes[], int n,int bt[], int wt[]){
wt[0] = 0;
for (int i = 1; i < n ; i++ )
wt[i] = bt[i-1] + wt[i-1] ;
}
void findTurnAroundTime( int processes[], int n, int bt[], int wt[],
int tat[]){
for (int i = 0; i < n ; i++)
tat[i] = bt[i] + wt[i];
}
void findavgTime( int processes[], int n, int bt[]){
int wt[n], tat[n], total_wt = 0, total_tat = 0;
findWaitingTime(processes, n, bt, wt);
findTurnAroundTime(processes, n, bt, wt, tat);
printf("Processes Burst time Waiting time Turn around
time\n");
for (int i=0; i<n; i++){
total_wt = total_wt + wt[i];
total_tat = total_tat + tat[i];
printf(" %d ",(i+1));
printf(" %d ", bt[i] );
printf(" %d",wt[i] );
printf(" %d\n",tat[i] );
}
int s=(float)total_wt / (float)n;
int t=(float)total_tat / (float)n;
printf("Average waiting time = %d\n",s);
printf("Average turn around time = %d \n",t);
}
int main(){
int processes[] = { 1, 2, 3};
int n = sizeof processes / sizeof processes[0];
int burst_time[] = {10, 5, 8};
findavgTime(processes, n, burst_time);
return 0;}


//sjf
#include <stdio.h>
int main(){
int A[100][4];
int i, j, n, total = 0, index, temp;
float avg_wt, avg_tat;
printf("Enter number of process: ");
scanf("%d", &n);
printf("Enter Burst Time:\n");
for (i = 0; i < n; i++) {
printf("P%d: ", i + 1);
scanf("%d", &A[i][1]);
A[i][0] = i + 1;
}
for (i = 0; i < n; i++) {
index = i;
for (j = i + 1; j < n; j++)
if (A[j][1] < A[index][1])
index = j;
temp = A[i][1];
A[i][1] = A[index][1];
A[index][1] = temp;
temp = A[i][0];
A[i][0] = A[index][0];
A[index][0] = temp;
}
A[0][2] = 0;
for (i = 1; i < n; i++) {
A[i][2] = 0;
for (j = 0; j < i; j++)
A[i][2] += A[j][1];
total += A[i][2];
}
avg_wt = (float)total / n;
total = 0;
printf("P BT WT TAT\n");
for (i = 0; i < n; i++) {
A[i][3] = A[i][1] + A[i][2];
total += A[i][3];
printf("P%d %d %d %d\n",
A[i][0],A[i][1], A[i][2], A[i][3]);
}
avg_tat = (float)total / n;
printf("Average Waiting Time= %f", avg_wt);
printf("\nAverage Turnaround Time= %f\n", avg_tat);}



//Round Robin
#include<iostream>
using namespace std;
void findWaitingTime(int processes[], int n,int bt[], int wt[], int
quantum){
int rem_bt[n];
for (int i = 0 ; i < n ; i++)
rem_bt[i] = bt[i];
int t = 0;
while (1){
bool done = true;
for (int i = 0 ; i < n; i++){
if (rem_bt[i] > 0){
done = false;
if (rem_bt[i] > quantum){
t += quantum;
rem_bt[i] -= quantum;
}else{
t = t + rem_bt[i];
wt[i] = t - bt[i];
rem_bt[i] = 0;
}
}
}
if (done == true)
break;
}
}
void findTurnAroundTime(int processes[], int n, int bt[], int wt[],
int tat[]){
for (int i = 0; i < n ; i++)
tat[i] = bt[i] + wt[i];
}
void findavgTime(int processes[], int n, int bt[],int quantum){
int wt[n], tat[n], total_wt = 0, total_tat = 0;
findWaitingTime(processes, n, bt, wt, quantum);
findTurnAroundTime(processes, n, bt, wt, tat);
cout << "PN\t "<< " \tBT "<< " WT " << " \tTAT\n";
for (int i=0; i<n; i++){
total_wt = total_wt + wt[i];
total_tat = total_tat + tat[i];
cout << " " << i+1 << "\t\t" << bt[i] <<"\t "<< wt[i] <<"\t\t
" << tat[i] <<endl;
}
cout << "Average waiting time = "<< (float)total_wt / (float)n;
cout << "\nAverage turn around time = "<< (float)total_tat /
(float)n << endl;
}
int main(){
int processes[] = { 1, 2, 3};
int n = sizeof processes / sizeof processes[0];
int burst_time[] = {10, 5, 8};
int quantum = 2;
findavgTime(processes, n, burst_time, quantum);
return 0;
}


//Daemon
#include <stdio.h> #include <stdlib.h>
#include <unistd.h> #include <sys/types.h>
#include <sys/stat.h>
#include <string.h>
int main(){
FILE *fp= NULL;
pid_t process_id = 0;
pid_t sid = 0;
process_id = fork();
if (process_id < 0){
printf("fork failed!\n");
exit(1);
}
if (process_id > 0){
printf("process_id of child process %d \n", process_id);
exit(0);
}
umask(0);
sid = setsid();
if(sid < 0){
exit(1);
}
chdir("/");
close(STDIN_FILENO);
close(STDOUT_FILENO);
close(STDERR_FILENO);
fp = fopen ("Log.txt", "w+");
while (1){
sleep(1);
fprintf(fp, "Logging info...\n");
fflush(fp);
}
fclose(fp);
return (0);
}


//Fork
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
int main(){
pid_t q= fork();
if(q<0){
printf("Error");
}else if(q==0){
printf("The PID of the child in q=0 is : %d\n",getpid());
printf("The PID of the parent in q=0 is : %d\n",getppid());
}else if(q>0){
printf("The PID of the child in q>0 is : %d\n",getpid());
printf("The PID of the parent in q>0 is : %d\n",q);
}

//Zombie Process
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
int main(){
pid_t child_pid = fork();
if (child_pid > 0)
sleep(50);
else
exit(0);
return 0;
}


//Orphan
#include<stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(){
pid_t pid = fork();
if (pid > 0)
printf("in parent process\n");
else if (pid == 0){
sleep(5);
printf("in child process\n");
}
return 0;}




//Catch a Signal
#include<stdio.h>
#include<signal.h>
#include<unistd.h>
void sig_handler(int signo){
if (signo == SIGINT)
printf("received SIGINT\n");
}
int main(void){
if (signal(SIGINT, sig_handler) == SIG_ERR)
printf("\ncan't catch SIGINT\n");
while(1)
sleep(1);
return 0;
}


//SIGKILL,SIGSTOP and other
#include<stdio.h>
#include<signal.h>
#include<unistd.h>
void sig_handler(int signo){
if (signo == SIGUSR1)
printf("received SIGUSR1\n");
else if (signo == SIGKILL)
printf("received SIGKILL\n");
else if (signo == SIGSTOP)
printf("received SIGSTOP\n");
}
int main(void){
if (signal(SIGUSR1, sig_handler) == SIG_ERR)
printf("\ncan't catch SIGUSR1\n");
if (signal(SIGKILL, sig_handler) == SIG_ERR)
printf("\ncan't catch SIGKILL\n");
if (signal(SIGSTOP, sig_handler) == SIG_ERR)
printf("\ncan't catch SIGSTOP\n");
while(1)
sleep(1);
return 0;}
