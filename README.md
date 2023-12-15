# CMPE355
//PROJECT TO SIMULATE THE SERVICE OF JOBS IN CPU SCHEDULING USING BOTH PREEMPTIVE AND NON PREEMPTIVE 
#include<stdio.h>
#include<iostream>
#include<unistd.h>
#include<string.h>
#include<fstream>

using namespace std;
int globalstop = 1;


void FSFC(int burst[], int arrive[]);
void SJF(int burst[], int arrive[]);
void PRIORITY(int burst[], int arrive[], int prior[]);
void RR(int quantum, int burst[]);

void PREEMPT();
void NONPREEMPT();

int main()
{
	int a = 0;
	 string filetxt;
	 int arr[100][3];
	 char c;
	 ifstream newfile;
   newfile.open("in.txt",ios::in); 
   if(newfile.is_open())
   {
      while(newfile.get(c))
      { 
      if(isdigit(c))
      {
      	arr[a] = c;
	  }
         cout << arr[a]<< "\n"; 
         if(arr[a])
         a++;
      }
      newfile.close(); 
      
       
	
	int output;
cout<<"This are the various Options you can choose from: /n 1. Scheduling /n 2. Preemptive(off) /n 3. Show Output  /n 4. Exit";
cin>>output;

while(globalstop ==1)
{

switch(output)
{
	case 1: {
	int schedule;	
	cout<<"This is the scheduling form, Please choose which scheduking method you want"<<endl;
	cout<<"1. First Come First Serve /n 2.Shortest Job First /n 3. Priority schdeuling /n 4. Round Robin";
	cin>>schedule;
	
	switch(schedule)
	{
		case 1:{
			cout<<"This is First Come First Serve"<<endl;
			FCFS(burst[],arrive[]);
			break;
		}
		
		case 2:{
			cout<<"This is Shortest Job First"<<endl;
			SJF(burst[],arrive[]);
			break;
		}
		
		case 3:{
			cout<<"This is Priority Scheduling"<<endl;
			PRIORITY(burst[],arrive[],priority[]);
			break;
		}
		
		case 4:{
			cout<<"This is Round Robin"<<endl;
			RR(quantum, burst[]);
			break;
		}
		
		default:{
			cout<<"Wrong input"<<endl;
			exit(1);
			break;
		}
	}
		
		
		break;
	}
	case 2:{
		int mode;
		cout<<"Please Select Your Mode. /n 1.Preemptive /n 2.Non-Preemptive";
		cin>>mode;
		switch(mode)
		{
			case 1:{
				cout<<"This is the preemptive mode";
				break;
			}
			
			case 2:{
				cout<<"This is the non-preemptive mode";
				break;
			}
				
		}
		break;
	}
	
	case 3:{
		display();
		break;
	}
	
	case 4:{
		bool ans;
		cout<<"Are you sure you want to exit the simulation:";
		cin>>ans;
		if(ans)
		{
			globalstop = 0;
			display();
			exit(1);
		}
		else {
			globalstop = 1;
		}
		break;
	}
	
	default:{
		
		break;
	}
}
}
}
