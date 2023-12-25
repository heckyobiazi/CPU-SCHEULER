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
int is_empty(struct node *);
struct node *insertFront(struct node *, int,int,int,int);
struct node *insertminiFront(struct node *, int);
struct node *insertBack(struct node *, int, int,int,int);
struct node *insertminiBack(struct node *, int);
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
void printlist(struct node *header);

struct node *FSFC(struct node *, struct node **);
struct node *SJF(struct node * , struct node **);
void PRIORITY(int, int , int);
void RR(int , int );

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
      
       header = createnode(12, 0, 0, 1);
       header = insertBack(header, 4, 0, 0, 2);
       header = insertBack(header, 2, 0, 0, 3);
       header = insertBack(header, 6, 0, 0, 4);
       header = insertBack(header, 5, 0, 0, 5);
       
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
std::cout<<"Option";
cin>>output;

switch(output)
{
	case 1: {
	int schedule;	
	std::cout<<"This is the scheduling form, Please choose which scheduking method you want"<<endl;
	std::cout<<"1. First Come First Serve \n 2.Shortest Job First \n 3. Priority schdeuling\n 4. Round Robin" ;
	cin>>schedule;
	
	switch(schedule)
	{
		case 1:{
			std::cout<<"This is First Come First Serve"<<endl;
			header2 = NULL;
	   	newheader = FSFC(header, &header2);
		cout<<"\nreturned success";
			break;
		}
		
		case 2:{
			std::cout<<"This is Shortest Job First"<<endl;
			header2 = NULL;
	       newheader = SJF(header, &header2);
		   cout<<"\nreturned success";
			break;
		}
		
		case 3:{
			std::cout<<"This is Priority Scheduling"<<endl;
			break;
		}
		
		case 4:{
			std::cout<<"This is Round Robin"<<endl;
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


struct node *createnode(int item1, int item2, int item3, int item_4)
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
		cout<<"The list cannot be delete it";
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
	int wt = 0;
	prem = 0;
	struct node *temp;
	struct node **ht;
	temp = header;
	ht = header2;
	
	   while(temp != NULL)
	   {
	if (*ht == NULL) {
    *ht = createmininode(0);
} 
else 
{
    a = (*ht)->burst;
    
    b = temp->burst;
    
    wt = b + a;
   
    *ht = insertminiBack(*ht, wt);

    ht = &((*ht)->next);
    temp = temp->next;
       }
	   }
	    
	    ///printlist2(header2);
		 return *header2;
	}



struct node *SJF(struct node *header , struct node **header2)
{
	if(prem == 0 )
	{
	std::cout<<"We are running a non-preemptive shortest job first scheduler";
  /*  int temp1;
	int temp2;
	int temp3;
	int temp4;
	struct node *min;
	min = createnode(header->burst,header->arrival,header->numbering,header->prority);*/
	int num = 0;
	int totalprocess;
	struct node **header3;
	struct node *head;
	struct node *temp;
	struct node *tmp;
	tmp = NULL;	
	temp = header;
     header3 = header2;

	if(header == NULL)
	{
      std::cout<<"LIST IS EMPTY";
	}
	else
	{
    totalprocess = count(header);
    cout<<"\n";
    cout<<totalprocess<<"\n";
	}
    
	int total = totalprocess + 1;
	int cnt = 0;
	 
	 for(int i=0; i<total; i++)
	   {
		if(*header2 == NULL)
		{
			 head = temp->next;
			 
			if(temp->arrival == head->arrival)
			{
				
    	    	while(temp->arrival == head->arrival)
	        	{
	        		cnt++;
	        		head = head->next;
	  	      	if(head == NULL)
	        		{
	        			break;
					}
  		        
        }
	        	
		     	sortburst(&temp,cnt+1);	
		     	printlist(temp);
		     	cout<<"\n";
		     	*header3 = createmininode(temp->arrival);
		     	cout<<temp->arrival<<"\n";
		     	
		 }
	
			else
			{
			 *header3 = createmininode(temp->arrival);

		     }
	   }
		 else    //saying a header2 has already been created
		 {   
			/*if(i == header3->arrival)
			{
				header3 = header3->next;
			}
			a = header3->burst-1;*/
			if(temp->arrival <= i )
			{
			if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            cout<<tmp->burst<<"\n";
            temp = temp->next;
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
			temp = temp->next;
			num++;
			}
		}
		else
		{
				if(tmp == NULL)
			{
            tmp = createnode(temp->burst, temp->arrival, temp->prority, temp->numbering);
            temp = temp->next;
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
			temp = temp->next;
			num++;
			}
		}
		 }
	   }

		if(num == total-1)
		{
		sortburst(&tmp, num);
		
		
		int a,b,wt;
		int final;

	   while(tmp != NULL)
	   {

		 a = (*header3)->burst;
   
         b = tmp->burst;
    
        wt = b + a;
       final = wt - tmp->arrival;
        *header3 = insertminiBack(*header3, final);
       
         header3 = &((*header3)->next);
        tmp = tmp->next;
	   }
    }
		 //i need to put the header to read the arrival time of each  process that has the same arrival time and pick the smallest and whilist
		 //picking the smallest, also putting it in another ll, hmm, i think that will work, after each iteration. okay, tommorow we will work
		 //with putting the ll in a loop and in that loop, it checks if it the arrival time behind it has shorter burst time, to evaluate what will hqppen,
		 //but normally, we are to check it in a loop to know which process whill be picked after it has ran the amountvof burst time
		 //and then putting the ones that are not rady in another struct node* or ll i guess;
		 
	
      // printlist2(header2);

		 return *header3;
	}
		 }

  /* if(prem == 1)
   {
	std::cout<<"This is the preemptive mode";
   }

*/
      
	

void display(struct node *header2)
{
	int a = 1;
	int avgtime = 0;
	double average;
	struct node *temp_no2;
	temp_no2 = header2;
    int temp1;
	int temp2;
	int temp3;
	int temp4;
	if(header2 == NULL)
	{
      cout<<"LIST IS EMPTY";
	}
	else
	{
		struct node *temp;
		while(header2->next != NULL)
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
	}

	while(temp_no2->next != NULL)
	{
		cout<<"Process "<<a<<" waiting time is "<<temp_no2->burst<<"ms \n";
		avgtime += temp_no2->burst;
		temp_no2 = temp_no2->next;
		a++;
	}

	average = avgtime/(a-1);
	cout<<"Average waiting time is "<<average<<"ms";
	cout<<endl;
}
