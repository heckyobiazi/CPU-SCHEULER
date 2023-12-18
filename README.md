//  CMPE351
//PROJECT TO SIMULATE THE SERVICE OF JOBS IN CPU SCHEDULING USING BOTH PREEMPTIVE AND NON PREEMPTIVE 
#include<stdio.h>
#include<iostream>
#include<unistd.h>
#include<string.h>
#include<fstream>
#include <cctype> 
#include<cstdlib>

using namespace std;
int globalstop = 1;

struct node{
	int burst;
	int arrival;
	int prority;
	struct node *next;
};

struct node *createnode(int, int , int);
struct node *createmininode(int );
int is_empty(struct node *);
struct node *insertFront(struct node *, int,int, int);
struct node *insertBack(struct node *, int, int, int);
struct node *insertminiBack(struct node *header, int item1);
void insertAfter(struct node *, int, int, int);
struct node *deleteFront(struct node *);
void display(struct node *);


struct node *FSFC(struct node *header, struct node *header2);
void SJF(int , int );
void PRIORITY(int, int , int);
void RR(int , int );

void PREEMPT();
void NONPREEMPT();



int main(int argc, char* argv[])
{
	if (argc != 5) {
        cout << "Usage: " << argv[0] << " -f inputFileName -o outputFileName" <<endl;
        return 1;
    }

    string inputFile;
    string outputFile;

    for (int i = 1; i < argc; ++i) {
         string arg = argv[i];
      
        if (arg == "-f" && i + 1 < argc) {
            inputFile = argv[i + 1];
        }

        if (arg == "-o" && i + 1 < argc) {
            outputFile = argv[i + 1];
        }
    }

    if (inputFile.empty() || outputFile.empty()) {
       cout << "Invalid command-line arguments. Usage: " << argv[0] << " -f inputFileName -o outputFileName" <<endl;
        return 1;
    }
	
	struct node *header = NULL;
	struct node *header2 = 	NULL;
	int item_1, item_2, item_3;
	 int a = 0;
	 int mini_arr[3];
	 char c;
	 char digit_str[2];
	 int cnt;
	 
	  ifstream input(inputFile);

    if (input.is_open()) {
        while (input.get(c)) {
            if (isdigit(c)) {
                digit_str[0] = c;
                digit_str[1] = '\0';
                mini_arr[a] = atoi(digit_str);
                a++;
            }

            if (a == 3) {
                a--;
                item_3 = mini_arr[a];
                item_2 = mini_arr[a - 1];
                item_1 = mini_arr[a - 2];
                a = 0;
            }

            if (header == NULL) {
                header = createnode(item_1, item_2, item_3);
            } else {
                header = insertBack(header, item_1, item_2, item_3);
            }
        }
    } else {
        cout << "Error opening input file: " << inputFile << endl;
        return 1;
    }
      
    
    int temp1;
	int temp2;
	int temp3;
	if(header == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		while(header->next != NULL)
		{
		    temp = header->next;
			while(temp != NULL)
			{
          if(header->arrival > temp->arrival)
		  {
             temp1 = header->burst;
			 header->burst = temp->burst;
			 temp->burst = temp1;

             temp2 = header->arrival;
			 header->arrival = temp->arrival;
			 temp->arrival = temp2;

			 temp3 = header->prority;
			 header->burst = temp->burst;
			 temp->burst = temp3;
		  }
		  temp = temp->next;
		  }
		     header = header->next;
		}

    
	double averaget;
	int waittime;
	   
	
	int output;
cout<<"This are the various Options you can choose from: /n 1. Scheduling /n 2. Preemptive(off) /n 3. Show Output  /n 4. Exit /n";
cout<<"Option";
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
			FSFC(header, header2);
			break;
		}
		
		case 2:{
			cout<<"This is Shortest Job First"<<endl;
			SJF();
			break;
		}
		
		case 3:{
			cout<<"This is Priority Scheduling"<<endl;
			PRIORITY();
			break;
		}
		
		case 4:{
			cout<<"This is Round Robin"<<endl;
			RR(int, int);
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
		display(header2);
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
return 0;
}


struct node *createnode(int item1, int item2, int item3)
{
	struct node *temp;
	temp = (struct node *)malloc(sizeof(node));
	temp->burst = item1;
	temp->arrival = item2;
	temp->prority = item3;
	temp->next = NULL;
	
	return temp;
}

struct node *createmininode(int item1)
{
	struct node *temp;
	temp = (struct node *)malloc(sizeof(node));
	temp->burst = item1;
	temp->next = NULL;
	
	return temp;
}
int is_empty(struct node *header)
{
	if(header == NULL)
	{
		return 1;
	}
	else
	{
		return 0;
	}
}

struct node *insertFront(struct node *header, int item1, int item2, int item3)
{
	struct node *temp;
	temp = createnode(item1,item2,item3);
	temp->next = header;
	header =  temp;
	
	return header;
}
struct node *insertBack(struct node *header, int item1, int item2, int item3)
{
	struct node *temp;
	struct node *ht;
	temp = createnode(item1, item2, item3);
	ht = header;
	while(ht->next != NULL)
	{
		ht = ht->next;
	}
	ht->next = temp;
	
	return header;
}

struct node *insertminiBack(struct node *header, int item)
{
	struct node *temp;
	struct node *ht;
	temp = createmininode(item);
	ht = header;
	while(ht->next != NULL)
	{
		ht = ht->next;
	}
	ht->next = temp;
	
	return header;
}

void insertAfter(struct node *afternode, int item1, int item2, int item3)
{
	struct node *temp;
	temp = createnode(item1, item2, item3);
	temp->next = afternode->next;
	afternode->next = temp;
}
struct node *deleteFront(struct node *header)
{
	if(header == NULL)
	{
		cout<<"The list is empty";
		exit(1);
	}
	else
	{
	struct node *temp;
	temp = header;
	header = temp->next;
	free(temp);
}
	
	return header;
}

struct node *FSFC(struct node *header, struct node *header2)
{
	int cnt = 0;
	   while(header != NULL)
	   {
		if(header2 == NULL)
		{
			 header2 = createmininode(header->burst);
		}
		 else{
		 header2 = insertminiBack(header2, header->burst + header2->burst);
		 header2 = header2->next;
		 }
		
		header = header->next;
	   }

		
	}
 return header2;
}

void display(struct node *header2)
{
	int a = 1;
	int avgtime = 0;
	int average;
	struct node *temp;
	temp = header2;
	while(temp != NULL)
	{
		cout<<"Process"<<a<<"waiting time is "<<temp->burst;
		avgtime += temp->burst;
		temp = temp->next;
		a++;
	}

	average = avgtime/(a-1);
	cout<<"Average waiting time is ";
	cout<<endl;
}
