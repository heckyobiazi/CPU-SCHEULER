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
int prem= 0;

struct node{
	int burst;
	int arrival;
	int prority;
	int numbering;
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
void display(struct node *);
struct node *swapnodes(struct node *,struct node *);
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
	 if(prem == 1)
	 {
		premmode = "ON";
	 }
	 else
	 {
		premmode = "OFF";
	 }
	 
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
	int item_1, item_2, item_3, item_4;
	item_4 = 1;
	 int a = 0;
	 int mini_arr[3];
	 char c;
	 char digit_str[2];
	 int cnt;
	 string premmode;
 if(prem == 1)
	 {
		premmode = "ON";
	 }
	 else
	 {
		premmode = "OFF";
	 }
      
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
std::cout << "These are the various options you can choose from:\n 1. Scheduling\n 2. Preemptive ( " <<premmode<< ") \n 3. Show Output\n 4. Exit\n";
std::cout<<"Option >";
cin>>output;

switch(output)
{
	case 1: {
	int schedule;	
	std::cout<<"This is the scheduling form, Please choose which scheduking method you want"<<endl;
	std::cout<<"1. First Come First Serve \n 2.Shortest Job First \n 3. Priority schdeuling\n 4. Round Robin" ;
	std::cout<<"option >";
	cin>>schedule;
	
	switch(schedule)
	{
		case 1:{
			if(prem == 0)
			{
			std::cout<<"This is First Come First Serve"<<endl;
			header2 = NULL;
	   	    newheader = FSFC(header, &header2);
            cout<<"\nreturned success\n";
		    cout<<"\n";
	        }
	        else if(prem == 1)
	        {
 	       cout<<"\nreturned success\n";
		   cout<<"\n";
			}
			break;
		}
		
		case 2:{
			std::cout<<"This is Shortest Job First"<<endl;
			header2 = NULL;
			if(prem == 0)
          {
			 
	       newheader = SJF(header, &header2);
		   cout<<"\nreturned success\n";
		   cout<<"\n";
	       }
	       else if(prem == 1)
	       {
       	   cout<<"\nreturned success\n";
		   cout<<"\n";
		   }
			break;
		}
		
		case 3:{
			std::cout<<"This is Priority Scheduling"<<endl;
			header2 = NULL;
			if(prem == 0)
			{
	       newheader = PRIORITY(header, &header2);
		   cout<<"\nreturned success\n";
		   cout<<"\n";
	        }
	        else if(prem == 1)
	        {
	        	
    	   cout<<"\nreturned success\n";
		   cout<<"\n";
			}
	        
			break;
		}
		
		case 4:{
			if(prem == 0)
			{
			int q;
			std::cout<<"This is Round Robin"<<endl;
			header2 = NULL;
			cout<<"\nPlease enter the quantum time: ";
			cin>>q;
			if(q > 0)
         	{
           newheader = RR(header, &header2, q);
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
		display(header2);
		break;
	}
	
	case 4:{
		bool ans;
		std::cout<<"Are you sure you want to exit the simulation:(1 for yes/0 for no)";
		cin>>ans;
		if(ans == 1)
		{
			globalstop = 0;
			display(header2);
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


struct node *FSFC(struct node *header, struct node **header2)
{
	
	
	cout<<"\n";
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
	ht = header2;
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
	    
	    ///printlist2(header2);
		 return *header2;
	}



struct node *SJF(struct node *header , struct node **header2)
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
     header3 = header2;

	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
    totalprocess = count(temp);
    cout<<"\n";
    cout<<totalprocess<<"\n";
	}
    
	int total = totalprocess + 1;
	int cnt = 0;
	 
	 for(int i=0; i<totalprocess; i++)
	   {
		if(*header2 == NULL)
		{
			 head = temp->next;
			 
			
		     	printlist(header);
		     	std::cout<<"\n";
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
		        cout<<"Header2\n";
			    //printlist2(header3);
		     	cout<<temp->next->numbering<<"\n";
		     
		     
		     printlist(header);
	   }
		 else    //saying a header2 has already been created
		 {   
			if(temp->arrival <= i )
			{
			temp = temp->next;
			if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            cout<<"temp numbering for "<<tmp->numbering<<"\n";
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

       cout<<tmp->numbering;
      
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

		 return *header3;
	}
		 }

struct node *SJFPREEMP(struct node *header, struct node **header2)
{
	std::cout<<"We are running a preemptive shortest job first scheduler";
	
	
}
      
      struct node *PRIORITY(struct node *header, struct node **header2)
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
     header3 = header2;
    head = header;

	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
    totalprocess = count(temp);
    cout<<"\n";
    cout<<totalprocess<<"\n";
	}
    
	int total = totalprocess + 1;
	int cnt = 0;
	int numbering;
	 
	 for(int i=0; i<totalprocess; i++)
	   {
		if(*header2 == NULL)
		{
				
		     	printlist(header);
		     	cout<<"\n";
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
		        cout<<"Header2\n";
			    //printlist2(header3);
		     	cout<<temp->next->numbering<<"\n";
		     
		     
		     printlist(header);
	   }
		 else    //saying a header2 has already been created
		 {   
			if(temp->arrival <= i )
			{
			temp = temp->next;
			if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            cout<<"temp numbering for "<<tmp->numbering<<"\n";
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

       cout<<tmp->numbering;
      
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

		 return *header3;
      	
	  }
}

struct node *PRIORITYPREEMP(struct node *header, struct node **header2)
{
	std::cout<<"We are running a preemptive priority scheduler";
	int num = 0;
	int process;
	int res = 0;
	int max,final;
	int a = 0;
	int totalnum;
	int totalprocess = 0;
	struct node **header3;
	struct node *head;
	struct node *ht;
	struct node *temp;
 	struct node *tmp;
	struct node *hd;
	struct node *tip;
	struct node *min;
	int minimum;
	
	min = createmidnode(temp->prority,0);
	tip = NULL;
	temp = header;
	head = header;
    header3 = header2;   
    process = count(header);
    
    while(temp != NULL)
    {
    	totalprocess = totalprocess + temp->burst;
    	temp = temp->next;
	}
	temp = head;
	std::cout<<totalprocess;
	min = temp;
	
	while(totalprocess != 0)
	{
		while(temp->arrival == a)
		{
			if(min->prority > temp->prority)
			{   
            	if(tmp == NULL)
				{
					createnode(minimum, a,min->prority,min->numbering);
				}
				else
				{
				tmp = insertBack(tmp, minimum,a,min->prority,min->numbering);
				}
			
				min->prority = temp->prority;
				min->numbering = temp->numbering;
				minimum = temp->burst;
				
				if(num >= minimum)
				{
					res+=num;
					tip = insertmidBack(tip,res,temp->numbering); 
				}
				
		if(tip == NULL)
		{
			num++;
			tip = createmidnode(0,min->numbering);
			minimum--;
		}
		else
		{
			num++;
			res +=minimum; 
			tip = insertmidBack(tip,minimum,min->numbering);
			minimum--;
		}
				
			}
			else if(min->prority == temp->prority)
			{
				min->prority = temp->prority;
				min->numbering = temp->numbering;
				minimum = temp->burst;
				
				
		if(tip == NULL)
		{
			num++;
			tip = createmidnode(0,min->numbering);
			minimum--;
		}
		else
		{
			num++;
			res +=minimum; 
			tip = insertmidBack(tip,minimum,min->numbering);
			minimum--;
		}
			}
			else
			{
				
			temp = insertBack(temp, temp->burst,temp->arrival,temp->prority,temp->numbering);
							
			}
			temp = temp->next;
		}
		
		a++;		
		totalprocess--;
	}
	
}

struct node *RR(struct node *header ,struct node **header2, int quantum )
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
	temp = header;
	head = header;
    header3 = header2;   
    process = count(header);
    
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
		if(*header2 == NULL)
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
	return *header2;
}
	

void display(struct node *header2)
{
	double a = 1;
	double avgtime = 0;
    double average;
	struct node *temp_no2;
	temp_no2 = header2;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	int num;
	if(header2 == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		num = count(header2);
		/*while(header2->next != NULL)
		{
		    temp = header2->next;
			while(temp != NULL)
			{
          if(header2->numbering > temp->numbering)
		  {
             temp1 = header2->burst;
			 header2->burst = temp->burst;
			 temp->burst = temp1;

             temp2 = header2->arrival;
			 header2->arrival = temp->arrival;
			 temp->arrival = temp2;

			 temp3 = header2->prority;
			 header2->burst = temp->burst;
			 temp->burst = temp3;

			 temp4 = header2->numbering;
			 header2->numbering = temp->numbering;
			 temp->numbering = temp4;
		  }
		  temp = temp->next;
		  }
		     header2 = header2->next;
		}
	}*/
	sortnumbering(&header2,num);
	}

	while(temp_no2 != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<temp_no2->burst<<"ms \n";
		avgtime += temp_no2->burst;
		temp_no2 = temp_no2->next;
		a++;
	}

	average = avgtime/(a-1);
	std::cout<<"Average waiting time is "<<average<<"ms";
	std::cout<<endl;
}
