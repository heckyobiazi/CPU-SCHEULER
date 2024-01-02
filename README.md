//CMPE351
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
int prem= 0;
int fcfs = 0;
int sjf = 0;
int priority = 0;
int rr = 0;
int sjfprem = 0;
int priorityprem = 0;
int scheduling = 0;

struct node{
	int burst;
	int arrival;
	int prority;
	int numbering;
	int waitingTime;
	struct node *next;
};

struct node *createnode(int, int , int, int);
struct node *createmininode(int );
struct node *createmidnode(int , int );
int is_empty(struct node *);
struct node *insertFront(struct node *, int,int,int,int);
struct node *insertminiFront(struct node *, int);
struct node *insertBack(struct node *, int, int,int,int);
struct node *insertminiBack(struct node *, int);
struct node *insertmidBack(struct node *, int , int);
void insertAfter(struct node *, int, int, int,int);
struct node *deleteFront(struct node *);
void deleteAfter(struct node *afternode);
struct node *moveBeginning(struct node *header, struct node *nodetobegin);
void display(struct node *,struct node *,struct node *,struct node *,struct node *,struct node *);
struct node *swapnodes(struct node *,struct node *);
struct node *removeNode(struct node *header, int numbering);
int count(struct node *);
void printlist2(struct node *header2);
void sortarrival(struct node **, int);
void sortburst(struct node **, int);
void sortpriority(struct node **, int);
void sortnumbering(struct node **, int);
void printlist(struct node *header);

struct node *FSFC(struct node *, struct node **);
struct node *SJF(struct node * , struct node **);
struct node *SJFPREEMP(struct node *, struct node **);
struct node *PRIORITY(struct node * , struct node **);
struct node *PRIORITYPREEMP(struct node *, struct node **);
struct node *RR(struct node* ,struct node **, int );

void displayrr(struct node *);
void displaypriority(struct node *);
void displaysjf(struct node *);
void displayfsfc(struct node *);
void displayprioritypreemp(struct node *);
void displaysjfpreemp(struct node *);

int main(int argc, char* argv[])
{
  /*
	if (argc != 5) {
        std::cout<< "Usage: " << argv[0] << " -f inputFileName -o outputFileName" <<endl;
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
       std::cout<<"Invalid command-line arguments. Usage: " << argv[0] << " -f inputFileName -o outputFileName" <<endl;
        return 1;
    }
	
	struct node *header = NULL;
	struct node *header2 ;
	int item_1, item_2, item_3, item_4;
	item_4 = 1;
	 int a = 0;
	 int mini_arr[3];
	 char c;
	 char digit_str[2];
	 int cnt;
	 string premmode;
     string scheduler;
	 
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
                header = createnode(item_1, item_2, item_3, item_4);
				item_4++;
            } else {
                header = insertBack(header, item_1, item_2, item_3, item_4);
				item_4++;
            }
        }
    } else {
        std::cout << "Error opening input file: " << inputFile << endl;
        return 1;
    }
     */
      
      	struct node *header = NULL;
	struct node *header2 ;
	struct node *newheader;
	struct node *newheader2;
	struct node *newheader3;
	struct node *newheader4;
	struct node *newheader5;
	struct node *newheader6;
	int item_1, item_2, item_3, item_4;
	item_4 = 1;
	 int a = 0;
	 int mini_arr[3];
	 char c;
	 char digit_str[2];
	 int cnt;
	 string scheduler;
	 string premmode;
	 
	 
    
      
       header = createnode(5, 0, 3, 1);
       header = insertBack(header, 4, 1, 2, 2);
       header = insertBack(header, 3, 1, 1, 3);
       header = insertBack(header, 4, 2, 2, 4);
       header = insertBack(header, 3, 3, 1, 5);
       
       
      int size = 0;
	  size = count(header);
    
   /* int temp1;
	int temp2;
	int temp3;
	int temp4;*/
	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
       sortarrival(&header, size);
	}
	//cout<<"\n";
	 
	

	double averaget;
	int waittime;
	   
	
	int output;
	while(globalstop == 1)
	{
		if(prem == 1)
	 {
		premmode = "ON";
	 }
	 else 
	 {
		premmode = "OFF";
	 }
	 
	 
	 if(scheduling == 1)
	 {
	 	scheduler = "First Come First Serve";
	 }
	 else if(scheduling == 2)
	 {
	 scheduler = "Shortest Job First";	
	 }
	 else if(scheduling == 3)
	 {
	 	scheduler = "Priority Scheduler";
	 }
	 else if(scheduling == 4)
	 {
	 	scheduler = "Round Robin";
	 }
	 else
	 { scheduler = "none";
	 }
std::cout << "These are the various options you can choose from:\n 1. Scheduling ("<<scheduler<<")\n 2. Preemptive ("<<premmode<<") \n 3. Show Output\n 4. Exit\n";
std::cout<<"Option > ";
cin>>output;

switch(output)
{
	case 1: {
	int schedule;	
	std::cout<<"This is the scheduling form, Please choose which scheduking method you want"<<endl;
	std::cout<<"1. First Come First Serve \n2. Shortest Job First \n3. Priority schdeuling\n4. Round Robin" ;
	std::cout<<"option > ";
	cin>>schedule;
	
	switch(schedule)
	{
		case 1:{
			scheduling = 1;
			if(prem == 0)
			{
			std::cout<<"This is First Come First Serve"<<endl;
			newheader = NULL;
	   	    newheader = FSFC(header, &newheader);
            cout<<"\nreturned success\n";
		    cout<<"\n";
	        }
	        else if(prem == 1)
	        {
 	       cout<<"\nThis scheduler can only be ran in non preemptive mode\n";
		   cout<<"\n";
			}
			break;
		}
		
		case 2:{
			scheduling = 2;
			std::cout<<"This is Shortest Job First"<<endl;
			
			if(prem == 0)
          {
			 newheader2 = NULL;
	       newheader2 = SJF(header, &newheader2);
		   cout<<"\nreturned success\n";
		   cout<<"\n";
	       }
	       else if(prem == 1)
	       {
	        newheader3 = NULL;
          newheader3 = SJFPREEMP(header, & newheader3);
           printlist(newheader3);
		   cout << "\nreturned success\n";
		   cout << "\n";

		   }
			break;
		}
		
		case 3:{
			scheduling = 3;
			std::cout<<"This is Priority Scheduling"<<endl;
			if(prem == 0)
			{
			 newheader4 = NULL;
			std::cout<<"This is the non preemptive mode"<<endl;
	       newheader4 = PRIORITY(header, & newheader4);
		   cout<<"\nreturned success\n";
		   cout<<"\n";
	        }
	        else if(prem == 1)
           {
           	 newheader5 = NULL;
           	std::cout<<"This is the preemptive mode"<<endl;
           newheader5 = PRIORITYPREEMP(header, & newheader5);
		   printlist(newheader5);	
    	   cout<<"\nreturned success\n";
		   cout<<"\n";
			}
	        
			break;
		}
		
		case 4:{
			scheduling = 4;
			if(prem == 0)
			{
			int q;
			std::cout<<"This is Round Robin"<<endl;
			 newheader6 = NULL;
			cout<<"\nPlease enter the quantum time: ";
			cin>>q;
			if(q > 0)
         	{
           newheader6 = RR(header, & newheader6, q);
		   cout<<"\nreturned success\n";
		   cout<<"\n";
            }
		   else
		   {
		   	cout<<"Quantum time should be greater than 0";
		   }
	      }
	      else
	      {
	      	cout<<"This scheduling can only be ran in preemptive mode\n";
		  }
			break;
		}
		
		default:{
			std::cout<<"Wrong input"<<endl;
			exit(1);
			break;
		}
	}
		
		
		break;
	}
	case 2:{
		int mode;
		std::cout<<"Please Select Your Mode. \n 1.Preemptive \n 2.Non-Preemptive";
		cin>>mode;
		switch(mode)
		{
			case 1:{
				std::cout<<"This is the preemptive mode";
				prem = 1;
				break;
			}
			
			case 2:{
				std::cout<<"This is the non-preemptive mode";
				prem = 0;
				break;
			}
				
		}
		break;
	}
	
	case 3:{
		display(newheader,newheader2,newheader3,newheader4,newheader5,newheader6);
		break;
	}
	
	case 4:{
		bool ans;
		std::cout<<"Are you sure you want to exit the simulation:(1 for yes/0 for no)";
		cin>>ans;
		if(ans == 1)
		{
			globalstop = 0;
			display(newheader,newheader2,newheader3,newheader4,newheader5,newheader6);
			exit(1);
		}
		else 
		{
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


struct node *createnode(int item1, int item2, int item3, int item4)
{
	struct node *temp;
	temp = (struct node *)malloc(sizeof(node));
	temp->burst = item1;
	temp->arrival = item2;
	temp->prority = item3;
	temp->numbering = item4;
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

struct node *createmidnode(int item1, int item2)
{
	struct node *temp;
	temp = (struct node *)malloc(sizeof(node));
	temp->burst = item1;
	temp->numbering = item2;
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

struct node *insertFront(struct node *header, int item1, int item2, int item3, int item4)
{
	struct node *temp;
	temp = createnode(item1,item2,item3,item4);
	temp->next = header;
	header =  temp;
	
	return header;
}

struct node *insertminiFront(struct node *header, int item)
{
	struct node *temp;
	temp = createmininode(item);
	temp->next = header;
	header =  temp;
	
	return header;
}

struct node *insertBack(struct node *header, int item1, int item2, int item3, int item4)
{
	struct node *temp;
	struct node *ht;
	temp = createnode(item1, item2, item3, item4);
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

struct node *insertmidBack(struct node *header, int item, int item2)
{
	struct node *temp;
	struct node *ht;
	temp = createmidnode(item,item2);
	ht = header;
	while(ht->next != NULL)
	{
		ht = ht->next;
	}
	ht->next = temp;
	
	return header;
}

void insertAfter(struct node *afternode, int item1, int item2, int item3, int item4)
{
	struct node *temp;
	temp = createnode(item1, item2, item3, item4);
	temp->next = afternode->next;
	afternode->next = temp;
}
struct node *deleteFront(struct node *header)
{
	if(header == NULL)
	{
		std::cout<<"The list is empty";
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

void deleteAfter(struct node *afternode)
{
	if(afternode->next == NULL)
	{
		std::cout<<"The list cannot be delete it";
		exit(1);
	}
	else
	{
		struct node *temp;
		temp = afternode->next;
		afternode->next = temp->next;
		free(temp);
	}
	
}

struct node *moveBeginning(struct node *header, struct node *nodetobegin)
{
	struct node*temp;
	struct node *tmp;
	int w,x,y,z;
	w = nodetobegin->next->burst;
	x = nodetobegin->next->arrival;
	y = nodetobegin->next->prority;
	z = nodetobegin->next->numbering;
    deleteAfter(nodetobegin);
    temp = createnode(w,x,y,z);
    temp->next = header;
    header = temp;
		
		return header;
}

struct node *swapnodes(struct node *temp, struct node *tp)
{
	int temp1, temp2, temp3, temp4;
	struct node *t = tp->next;
	tp->next = temp;
	temp->next = t;
			 return tp;
}

void freeList(struct node *header) 
{
    while (header != NULL) 
	{
        struct node *temp = header;
        header = header->next;
        delete temp;
    }
}

struct node *removeNode(struct node *header, int numbering) 
{
    struct node *temp = header;
    struct node *prev = NULL;

    while (temp != NULL && temp->numbering != numbering) 
	{
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) 
	{
        
        return header;
    }

    if (prev == NULL) 
	{
        
        header = temp->next;
    } 
	else 
	{
        prev->next = temp->next;
    }

    free(temp);
    return header;
}

void sortburst(struct node **header, int size)
{
	struct node **ht;
	int swap;
	for(int i=0; i<=size-1; i++)
	{
		ht = header;
		swap =0;
		for(int j=0; j< size-i-1; j++)
		{
			struct node *h1 = *ht;
			struct node *h2 = h1->next;
			
			if(h1->burst > h2->burst)
			{
				*ht = swapnodes(h1,h2);
				swap =1;
			}
			ht = &(*ht)->next;
		}
		
		if(swap ==0)
		{
			break;
			
		}
	}
}


void sortarrival(struct node **header, int size)
{
	struct node **ht;
	int swap;
	for(int i=0; i<=size-1; i++)
	{
		ht = header;
		swap =0;
		for(int j=0; j< size-i-1; j++)
		{
			struct node *h1 = *ht;
			struct node *h2 = h1->next;
			
			if(h1->arrival > h2->arrival)
			{
				*ht = swapnodes(h1,h2);
				swap =1;
			}
			ht = &(*ht)->next;
		}
		
		if(swap ==0)
		{
			break;
			
		}
	}
}

void sortpriority(struct node **header, int size)
{
	struct node **ht;
	int swap;
	for(int i=0; i<=size-1; i++)
	{
		ht = header;
		swap =0;
		for(int j=0; j< size-i-1; j++)
		{
			struct node *h1 = *ht;
			struct node *h2 = h1->next;
			
			if(h1->prority > h2->prority)
			{
				*ht = swapnodes(h1,h2);
				swap =1;
			}
			ht = &(*ht)->next;
		}
		
		if(swap ==0)
		{
			break;
			
		}
	}
}

void sortnumbering(struct node **header, int size)
{
	struct node **ht;
	int swap;
	for(int i=0; i<=size-1; i++)
	{
		ht = header;
		swap =0;
		for(int j=0; j< size-i-1; j++)
		{
			struct node *h1 = *ht;
			struct node *h2 = h1->next;
			
			if(h1->numbering > h2->numbering)
			{
				*ht = swapnodes(h1,h2);
				swap =1;
			}
			ht = &(*ht)->next;
		}
		
		if(swap ==0)
		{
			break;
			
		}
	}
}

int count(struct node *header)
{
	struct node *temp;
	temp = header;
	int cnt;
	 cnt = 0;
	while(temp != NULL)
	{
		cnt = cnt + 1;
		temp = temp->next;		
    }
 return cnt;

}

void printlist(struct node *header)
{
	if(header == NULL)
	{
		cout<<"The list is empty";
		exit(1);
	}
	else
	{
		struct node *temp;
		int x;
		temp = header;
		while(temp != NULL)
		{
		x = temp->burst;
		cout<<x<<", ";
		temp = temp->next;	
		}
		cout<<endl;
	}
}

void printlist2(struct node **header2)
 {
    struct node **temp = header2;
    while (temp != NULL) {
        cout << (*temp)->burst << " ";
        temp = &((*temp)->next);
    }
    cout << endl;
}


struct node *FSFC(struct node *header, struct node **newheader)
{
	int a;
	int b;
	int final;
	int cnt;
	int num = 0;
	int wt = 0;
	prem = 0;
	struct node *temp;
	struct node *tip;
	struct node **ht;
	struct node *temp2;
	temp = header;
	ht = newheader;
	tip = NULL;
	temp2 = header;
	cnt = count(header);
	   while(temp != NULL)
	   {num++;
	if (*ht == NULL) {
    *ht = createmininode(0);
    tip = createmininode(0);
} 
else 
{ 
    a = tip->burst;
    b = temp->burst;
    wt = b + a;
  tip = insertminiBack(tip, wt);
  tip = tip->next;
  
    a = tip->burst;
       
    temp = temp->next;
    if(cnt < num)
    {
    	break;
	}
	else
	{
   final = a - temp->arrival;
   *ht = insertminiBack(*ht, final);
    
    ht = &((*ht)->next);
   }
}
	   }
	    
	    fcfs = 1;
	    ///printlist2(header2);
		 return *newheader;
	}



struct node *SJF(struct node *header , struct node **newheader2)
{
  	if(prem == 0)
      	{
      		std::cout<<"We are running a non-preemptive shortest job first scheduler";
      		
      		int num = 0;
	int totalprocess;
	int numbering;
	struct node **header3;
	struct node *head;
	struct node *ht;
	struct node *temp4;
	struct node *temp;
	struct node *tmp;
	struct node *tip;
	tip = NULL;
	tmp = NULL;	
	temp = header;
     header3 = newheader2;

	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
    totalprocess = count(temp);
	}
    
	int total = totalprocess + 1;
	int cnt = 0;
	 
	 for(int i=0; i<totalprocess; i++)
	   {
		if(*newheader2 == NULL)
		{
			 head = temp->next;
		     	*header3 = createmidnode(temp->arrival,temp->numbering);
		     	tip = createmidnode(temp->burst,temp->numbering);
		     	//i am going to create a temporary struct to acesss the lowest temp, we will access it
		     	//without going through the pointer to avoid changes and when we acess the lowest, we collect the temp numbering and utilize it
 	             temp4 = createnode(head->burst, head->arrival, head->prority, head->numbering);
 	              ht = head->next;
 	            	while(ht != NULL)
 	            	{
 	            	if(temp4->burst > ht->burst)
 	            	{
			         temp4 = createnode(ht->burst, ht->arrival, ht->prority, ht->numbering);		 	   
                     }
					 ht = ht->next;
                   }
			   numbering = temp4->numbering; 
			
				 *header3 = insertmidBack(*header3,temp->burst - temp->next->arrival,numbering);
		       

	   }
		 else    //saying a header2 has already been created
		 {   
			if(temp->arrival <= i )
			{
			temp = temp->next;
			if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            num++;
			}
			else
			{
				if(temp->burst > tmp->burst)
				{
					tmp = insertBack(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
				else{
					tmp = insertFront(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
			num++;
			}
		}
		else
		{
			temp = temp->next;
				if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            num++;
			}
			else
			{
				if(temp->prority > tmp->prority)
				{
					tmp = insertBack(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
				else{
					tmp = insertFront(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
			num++;
			}
		}
		 }
	   }

      
		if(num == totalprocess-1)
		{
		sortarrival(&tmp, num);
		sortburst(&tmp, num);
		
		
		int a,b,wt;
		int final;

	   while(tmp != NULL)
	   {

		 a = tip->burst;
         b = tmp->burst;
         wt = b + a;
         
       tip = insertmidBack(tip, wt, tmp->numbering);
        tip = tip->next;
        
        tmp = tmp->next;
        if(tmp == NULL)
        {
        	break;
		}
        final = wt - tmp->arrival;
        *header3 = insertmidBack(*header3, final,tmp->numbering);
       
         header3 = &((*header3)->next);
	   }
    }
	 
      // printlist2(header2);
      //printlist(header);

        sjf = 1;
		 return *newheader2;
	}
		 }

struct node *SJFPREEMP(struct node *header, struct node **newheader3)
 {
 	printlist(header);
    std::cout << "We are running a preemptive shortest scheduler\n";

    struct node *waitingtimeht = NULL;
    int current = 0;
    int process = count(header);
    struct node *head = header;  

    struct node **header3;
    header3 = newheader3;
    
    struct node *headercopy = NULL;
    struct node *copytemp = header;
    while (copytemp != NULL)
	 {
	 	if(headercopy == NULL)
	 	{
	 		headercopy = createnode(copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
		 }
		 else
		 {
        headercopy = insertBack(headercopy, copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
    }
        copytemp = copytemp->next;
    }

    while (process > 0)
	 {
        struct node *min = NULL;
        struct node *temp = headercopy;

        while (temp != NULL && temp->arrival <= current)
		 {
            if (min == NULL || temp->burst < min->burst || (temp->burst == min->burst && temp->arrival < min->arrival))
			 {
                min = temp;
            }
            temp = temp->next;
        }

        if (min != NULL)
		 {
            min->burst--;

            struct node *waitingTemp = headercopy;
            while (waitingTemp != NULL) 
			{
                if (waitingTemp->arrival <= current && waitingTemp->numbering != min->numbering)
		 		{
                    waitingTemp->waitingTime++;
                }
                waitingTemp = waitingTemp->next;
            }
    
            if (min->burst == 0) 
			{
				
                int final;
                final = min->waitingTime;
                
                if(process == 1)
                {
                final++;	
				}
				
                if (*header3 == NULL)
				 {
                    *header3 = createmidnode(final, min->numbering);
                 } 
				else 
				{
                    *header3 = insertmidBack(*header3, final, min->numbering);
                }
                process--;

                headercopy = removeNode(headercopy, min->numbering);
            }
        }

        current++;
    }

    printlist(header);
    //printlist2(header2);
    
    sjfprem = 1;
    
    return *newheader3;
}
      
      struct node *PRIORITY(struct node *header, struct node **newheader4)
      {
      	if(prem == 0)
      	{
      		std::cout<<"We are running a non-preemptive priority scheduler";
      		
   		
      		int num = 0;
	int totalprocess;
	int temp1,temp2,temp3;
	struct node *temp4;
	struct node **header3;
	struct node *head;
	struct node *ht;
	struct node *temp;
	struct node *tmp;
	struct node *tip;
	tip = NULL;
	tmp = NULL;	
	temp = header;
     header3 = newheader4;
    head = header;

	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
    totalprocess = count(temp);
	}
    
	int total = totalprocess + 1;
	int cnt = 0;
	int numbering;
	 
	 for(int i=0; i<totalprocess; i++)
	   {
		if(*newheader4 == NULL)
		{
				
		     	*header3 = createmidnode(temp->arrival,temp->numbering);
		     	tip = createmidnode(temp->burst,temp->numbering);
		     	//i am going to create a temporary struct to acesss the lowest temp, we will access it
		     	//without going through the pointer to avoid changes and when we acess the lowest, we collect the temp numbering and utilize it
 	            temp4 = createnode(head->burst, head->arrival, head->prority, head->numbering);
 	            ht = head->next;
 	            	while(ht != NULL)
 	            	{
 	            	if(temp4->burst > ht->burst)
 	            	{
			         temp4 = createnode(ht->burst, ht->arrival, ht->prority, ht->numbering);		 	   
                     }
					 ht = ht->next;
                   }
			   numbering = temp4->numbering; 
			
				 *header3 = insertmidBack(*header3,temp->burst - temp->next->arrival,numbering);
    

	   }
		 else    //saying a header2 has already been created
		 {   
			if(temp->arrival <= i )
			{
			temp = temp->next;
			if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);

            num++;
			}
			else
			{
				if(temp->prority > tmp->prority)
				{
					tmp = insertBack(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
				else{
					tmp = insertFront(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
			num++;
			}
		}
		else
		{
			temp = temp->next;
				if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            num++;
			}
			else
			{
				if(temp->prority > tmp->prority)
				{
					tmp = insertBack(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
				else{
					tmp = insertFront(tmp, temp->burst, temp->arrival, temp->prority,temp->numbering);
				}
			num++;
			}
		}
		 }
	   }

		if(num == totalprocess-1)
		{
		sortarrival(&tmp, num);
		sortpriority(&tmp, num);
		
		
		int a,b,wt;
		int final;

	   while(tmp != NULL)
	   {

		 a = tip->burst;
         b = tmp->burst;
         wt = b + a;
         
       tip = insertmidBack(tip, wt, tmp->numbering);
        tip = tip->next;
        
        tmp = tmp->next;
        if(tmp == NULL)
        {
        	break;
		}
        final = wt - tmp->arrival;
        *header3 = insertmidBack(*header3, final,tmp->numbering);
       
         header3 = &((*header3)->next);
	   }
    }
	 
      // printlist2(header2);
      //printlist(header);

        priority = 1;
		 return *newheader4;
      	
	  }
}

struct node *PRIORITYPREEMP(struct node *header, struct node **newheader5)
{
    std::cout << "We are running a preemptive priority scheduler";

    struct node *waitingtimeht = NULL;
    int current = 0;
    struct node **header3;
    header3 = newheader5;

    struct node *headercopy = NULL;
    struct node *copytemp = header;
    while (copytemp != NULL)
    {
        if (headercopy == NULL)
        {
            headercopy = createnode(copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
        }
        else
        {
            headercopy = insertBack(headercopy, copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
        }
        copytemp = copytemp->next;
    }

    int process = count(headercopy);
    struct node *head = headercopy;

    while (process > 0)
    {
        struct node *min = NULL;
        struct node *temp = headercopy;

        while (temp != NULL && temp->arrival <= current)
        {
            if (min == NULL || temp->prority < min->prority || (temp->prority == min->prority && temp->arrival < min->arrival))
            {
                min = temp;
            }
            temp = temp->next;
        }

        if (min != NULL)
        {
           

            min->burst--;
            
            struct node *waitingTemp;
			waitingTemp = headercopy;
            
            while (waitingTemp != NULL)
            {
                if (waitingTemp->arrival <= current && waitingTemp->numbering != min->numbering)
                {
                	printlist(waitingTemp);
                    waitingTemp->waitingTime = waitingTemp->waitingTime + 1 ;
                }
                waitingTemp = waitingTemp->next;
            }

            if (min->burst == 0)
            {
                int final;
                final = min->waitingTime;

               /* if (process == 1)
                {
                    final++;
                }*/

                if (*header3 == NULL)
                {
                    *header3 = createmidnode(final, min->numbering);
                }
                else
                {
                    *header3 = insertmidBack(*header3, final, min->numbering);
                }
                process--;

                headercopy = removeNode(headercopy, min->numbering);
            }
        }

        current++;
    }
    printlist(header);

    priorityprem = 1;

    return *newheader5;
}


struct node *RR(struct node *header ,struct node **newheader6, int quantum )
{
	std::cout<<"This is Round Robin scheduling";
	int num;
	int process;
	int res = 0;
	int max,final;
	int a = 1;
	int col = quantum;
	int totalnum;
	int totalprocess = 0;
	struct node **header3;
	struct node *head;
	struct node *ht;
	struct node *temp;
 	struct node *tmp;
	struct node *hd;
	struct node *tip;
	
	tip = NULL;
    header3 = newheader6;   
    process = count(header);
    
    struct node *headercopy = NULL;
    struct node *copytemp = header;
    while (copytemp != NULL)
	 {
	 	if(headercopy == NULL)
	 	{
	 		headercopy = createnode(copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
		 }
		 else
		 {
        headercopy = insertBack(headercopy, copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
    }
        copytemp = copytemp->next;
    }
    
   	temp = headercopy;
	head = headercopy;
    
    while(temp != NULL)
    {
    	totalprocess = totalprocess + temp->burst;
    	temp = temp->next;
	}
	temp = head;

while (totalprocess != 0)
{
    if (quantum <= temp->burst)
    {
        totalprocess -= quantum;
        num = temp->burst - quantum;
        temp = insertBack(temp, num, temp->arrival, temp->prority, temp->numbering);
        if (tip == NULL)
        {
            tip = createmidnode(quantum, temp->numbering);
            cout << temp->burst;
            res++;
        }
        else
        {   
            col += quantum;
            tip = insertmidBack(tip, col, temp->numbering);
            res++;
        }
    }
    else
    {  
        totalprocess -= temp->burst;
        if (tip == NULL)
        {
            tip = createmidnode(quantum, temp->numbering);
            res++;
        }
        else
        {
            col += temp->burst;
            tip = insertmidBack(tip, col, temp->numbering);
            res++;
        }
    }
    temp = temp->next;
   
}
	sortnumbering(&tip, res);
	process++;
	
	while(process != a)
	{
		while(tip->numbering == a)
		{
			max = tip->burst;
			tip = tip->next;
			if(tip == NULL)
		{
			break;
		}
		}
		final = max - head->burst - head->arrival;
		if(*newheader6 == NULL)
		{
			*header3 = createmidnode(final,a);
		}
		else
		{
			*header3 = insertmidBack(*header3,final,a);
			//header3 = &((*header3)->next);
		}
		a++;
		head = head->next;
	}
	
	rr = 1;
	
	return *newheader6;
}
	

void displaysjfpreemp(struct node *newheader3)
{
	cout<<"\n This scheduler is the Shortest Job First Preemptive scheduler Waiting time\n";
	
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	
	 struct node *headercopy = NULL;
    struct node *copytemp = newheader3;
    while (copytemp != NULL)
	 {
	 	if(headercopy == NULL)
	 	{
	 		headercopy = createnode(copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
		 }
		 else
		 {
        headercopy = insertBack(headercopy, copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
    }
        copytemp = copytemp->next;
    }
	
	temp_no2 = headercopy;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(headercopy == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(headercopy);
	   sortnumbering(&headercopy,num);
	}
    
	while(headercopy != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<headercopy->burst<<"ms \n";
		avgtime += headercopy->burst;
		headercopy = headercopy->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms\n";
}

void displayprioritypreemp(struct node *newheader5)
{
	cout<<"\n This scheduler is the Priority Preemptive scheduler Waiting time\n";
	
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	
	struct node *headercopy = NULL;
    struct node *copytemp = newheader5;
    while (copytemp != NULL)
	 {
	 	if(headercopy == NULL)
	 	{
	 		headercopy = createnode(copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
		 }
		 else
		 {
        headercopy = insertBack(headercopy, copytemp->burst, copytemp->arrival, copytemp->prority, copytemp->numbering);
    }
        copytemp = copytemp->next;
    }
	
	temp_no2 = headercopy;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(headercopy == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(headercopy);
	    sortnumbering(&headercopy,num);
	}
	//printlist(temp_no2);
    
	while(headercopy != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<headercopy->burst<<"ms \n";
		avgtime += headercopy->burst;
		headercopy = headercopy->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms\n";
}

	void displayfsfc(struct node *newheader)
{
	cout<<"\n This scheduler is the First Come First Serve scheduler Waiting time\n";
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	temp_no2 = newheader;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(newheader == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(newheader);
	sortnumbering(&newheader,num);
	}
	//printlist(temp_no2);
    
	while(newheader != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<newheader->burst<<"ms \n";
		avgtime += newheader->burst;
		newheader = newheader->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms";
	std::cout<<endl;
}

void displaysjf(struct node *newheader2)
{
	cout<<"\n This scheduler is the Shortest Job First Non Preemptive scheduler Waiting time\n";
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	temp_no2 = newheader2;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(newheader2 == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(newheader2);
	sortnumbering(&newheader2,num);
	}
	//printlist(temp_no2);
    
	while(newheader2 != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<newheader2->burst<<"ms \n";
		avgtime += newheader2->burst;
		newheader2 = newheader2->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms";
	std::cout<<endl;
}

void displaypriority(struct node *newheader4)
{
	cout<<"\n This scheduler is the Priority Non Preemptive Scheduler Waiting time\n";
	
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	temp_no2 = newheader4;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(newheader4 == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(newheader4);
	sortnumbering(&newheader4,num);
	}
	//printlist(temp_no2);
    
	while(newheader4 != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<newheader4->burst<<"ms \n";
		avgtime += newheader4->burst;
		newheader4 = newheader4->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms";
	std::cout<<endl;
}

void displayrr(struct node *newheader6)
{
	cout<<"\n This scheduler is the Round Robin scheduler Waiting time\n";
	
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	temp_no2 = newheader6;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(newheader6 == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(newheader6);
	sortnumbering(&newheader6,num);
	}
//	printlist(temp_no2);
    
	while(newheader6 != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<newheader6->burst<<"ms \n";
		avgtime += newheader6->burst;
		newheader6 = newheader6->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms";
	std::cout<<endl;
}

void display(struct node *newheader,struct node *newheader2, struct node *newheader3, struct node *newheader4, struct node *newheader5, struct node *newheader6)
{
	if(fcfs == 1)
	{
		displayfsfc(newheader);
	}
	
	if(sjf == 1)
	{
		displaysjf(newheader2);
	}
	
	if(priority == 1)
	{
		displaypriority(newheader4);
	}
	
	if(rr == 1)
	{
		displayrr(newheader6);
	}
	
	if(sjfprem == 1)
	{
		displaysjfpreemp(newheader3);
	}
	
	if(priorityprem == 1)
	{
		displayprioritypreemp(newheader5);
	}
}

