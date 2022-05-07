# cpp-project-
super market system 
#include<iostream>
#include<fstream>
using namespace std;

class shopping

{
private:
    /* data */
    int pcode;
    float price;
    float dis;
    string pname;

public:
            void menu();
            void administration();
            void buyer();
            void add();
            void edit();
            void rem();
            void list();
            void receipt();

};


void shopping :: menu()
{
    int choice;
    string email;
    string password;

    cout<<"\t\t\t\t---------------------------------------------------------------------------------\n";
    cout<<"\t\t\t\t\t                                                                                \n";
    cout<<"\t\t\t\t\t                      SuperMarket Main Menu                                     \n";
    cout<<"\t\t\t\t\t                                                                                \n";
    cout <<"\t\t\t\t---------------------------------------------------------------------------------\n";
    cout<<"\n\n";
    cout<<"\t\t\t\t|                       1)administrator                      |\n";
    cout<<"\t\t\t\t|                                                            |\n";
    cout<<"\t\t\t\t|                       2) buyer                             |\n";
    cout<<"\t\t\t\t|                                                            |\n";          
    cout<<"\t\t\t\t|                       3)exit                               |\n";
    cout<<"\t\t\t\t|                                                            |\n";
    cout<<"\n";
    cout<<"\t\t\t\t    Please select your choice::       ";
    cin>>choice;
    cout<<"\n\n";
    switch (choice)
    {
        case 1 :
            cout<<"\t\t\t\t Please login \n\n\n";
            cout<<"\t\t\t\t Enter Email :";
            cin>>email;

            cout<<"\t\t\t\t Enter password :";
            cin >>password;

            if(email=="p@gmail.com"  && password=="12345")
            {
                administration();

            }
            else{
                cout<<"Invalid  emali/password ";

            }
            break;
        
        case 2 :
        { buyer();
        }

        case 3 :
        {
            exit(0);
        }
        default:{
            cout<<" Please select the given option ";
        } 
    }
}

void shopping :: administration()
{
    m:
    int choice;
    cout<<"\n";
    cout<<"\t\t\t\t        Administration menu          \n";
    cout<<"\t\t\t\t |------1) Add the Product-----------|\n";
    cout<<"\t\t\t\t |                                   |\n";   
    cout<<"\t\t\t\t |------2) modify  the Product-------|\n";
    cout<<"\t\t\t\t |                                   |\n";   
    cout<<"\t\t\t\t |------3) Delete  the Product-------|\n";
    cout<<"\t\t\t\t |                                   |\n";  
    cout<<"\t\t\t\t |------4) Back to main menu---------|\n";   
    cout<<"\n";
    cout<<"\t\t\t\t Please enter your choice ::   ";
    cin>> choice;

    switch (choice)
    {
        case 1:
        {
            add();
            break;
        }
        case 2:
        {
            edit();
            break;
        }

        case 3:{
            rem();
            break;
        
        }
        case 4 :
        {
            menu();
            break;
        }
        
        default:
        {
            cout<<"Invalid Choice ";
        }
    }
    goto m;
}



void shopping :: buyer ()
{
    m:
    int choice;
    cout<<"\n\t\t\t\t     Buyer                                 \n";
    cout<<"\n\t\t\t\t ------------------------------------------\n";
    cout<<"\n\t\t\t\t       1)Buy product                       \n";
     cout<<"\n\t\t\t\t                                          \n";
     cout<<"\n\t\t\t\t      2) go back                          \n";

     cout<<"\t\t\t\t Enter your choice :";
                    cin>>choice;


     switch (choice)
     {
        case 1:
                receipt();
                break;
        case 2 :
                menu();
            break;
        
        default:
        cout<<"Invalid Choice ";
     }
    goto m;

}

void shopping :: add()

{   
    m:
    fstream data ;
    int c;
    int token=0;
    float p;
    float d;
    string n;

    cout<<"\n\n\t\t\t\t Add new product ";
    cout<<"\n\n\t\t\t\t product code of the product :  ";
    cin>>pcode;
    cout<<"\n\n\t\t\t\t Name of the product :  ";
    cin>>pname;
    cout<<"\n\n\t\t\t\t Prize of the Product : ";
    cin>>price;
    cout<<"\n\n\t\t\t\t discount on product : ";
    cin>>dis;

    data.open("database.txt",ios::in);

    if(!data )
    {
        data.open("database.txt",ios::app|ios::out);
        data<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<dis<<"\n";
        data.close();
    }
    else{
        data>>c>>n>>p>>d;
        
        while (!data.eof())
        {
            if ( c ==pcode)
            {
               token ++;
            }
            data>>c>>n>>p>>d;
        }
        data.close();
        
        
        if(token==1)
        goto m;
        else{
            data.open("database.txt",ios::app|ios::out);
        data<<" "<<pcode<<" "<<pname<< " "<<price<<" "<<dis<<"\n";
        data.close();
    
        }
    }
 cout<<"\n\n\t\t Record insertted !";
}



void shopping :: edit()
{
    fstream data, data1;
    int pkey;
    int token=0 ,c;
    float p;
    float d;
    string n;

    cout<<"\n\t\t\t Modify the Record";
    cout <<"\n\t\t\t product code :";
    cin>>pkey ;

    data.open("database.txt",ios::in);
    if(!data){
        cout<<"\n\t\tFile does not exists";
    }
    else{
        data1.open("database1.txt",ios::app|ios::out);
        
        data>>pcode>>pname>>price>>dis;
        while(!data.eof())
        {
            if(pkey==pcode)
            {
                cout<<"\n\t\tProduct New Code : ";
                cin>>c;
                cout<<"\n\t\t Name of  the product : ";
                cin>>n;
                cout<<"\n\t\t\t price : ";
                cin>>p;
                cout<<"\n\t\t Discount  :";
                cin>>d;
                data1<<" "<<c<<" "<<n<<" "<<p<<" "<<d<<" \n";
                cout<<"\n\t\t Record  edited";
                token++; 
            }
            else{
                data1<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<dis<<"\n";
            }
            data>>pcode>>pname>>price>>dis;
        }
        data.close();
        data1.close();

        remove("database.txt");
        rename("database1.txt","database.txt");

        if(token==0)
        {
            cout<<"\n\n Record not Found  sorry !";
        }
    }
}



void shopping::rem()
{
    fstream data, data1;
    int pkey;
    int token=0;
    cout<<"\n\t\t Delete product";
    cout<<"\n\n\t Product code :";
    cin>>pkey;
    data.open("database.txt",ios::in);
    if(!data)
    {
        cout<<"file does not exists";
    }
    else {
        data1.open("database1.txt",ios::app|ios::out);
        data>>pcode>>pname>>price>>dis;
        while (!data.eof())
        {
            if(pcode==pkey)
            {
                cout<<"\n\n\t Product deleated successfully ";
                token++;
            }
        
            else {
            data1<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<dis<<"\n";

             }
             data>>pcode>>pname>>price>>dis;
        }
        data.close();
        data1.close();
        remove("database.txt");
        rename("database1.txt","database.txt");

        if(token==0)
        {
            cout<<"\n\n Records not found ";
        }
        
    }
}


void shopping :: list()
{
    fstream data;
    data.open("database.txt",ios::in);
    cout<<"\n\n!..................................................................\n" ;
    cout<<"productNo\t\tName\t\t\t\tprice\n";
    cout<<"\n\n!..................................................................\n" ;
    data>>pcode>>pname>>price>>dis;
    while (!data.eof())
    {
        cout<<pcode<<"\t\t"<<pname<<"\t\t"<<price<<"\n";
        data>>pcode>>pname>>price>>dis;
    }
    data.close();
}

void shopping:: receipt()
{
    fstream data;
    int arrc[100];
   int arrq[100];
   char choice;
   int c=0;
   float amount=0;
   float dis =0;
   float total=0;

   cout<<"\n\n\t\t\t RECEIPT";
   data.open("database.txt",ios::in);
   if(!data)
   {
       cout<<"\n\n Empty Database ";

   }
   else{
       data.close();
       list();
       cout<<"\n|-------------------------------------------------------------------------|\n";
       cout<<"\n|                                                                         |\n";
       cout<<"\n|                     Please place the order                              | \n";
       cout<<"\n|                                                                         |\n";
       cout<<"\n|-------------------------------------------------------------------------|\n";
       do{
             m:

           cout<<"\n\n Enter Product code  : ";
           cin>>arrc[c];
           cout<<"\n\n Enter the product quantity : ";
           cin>>arrq[c];
           for(int i=0;i<c;i++)
           {
               if(arrc[c]==arrc[i])
               {
                   cout<<"\n\n Duplicate product code. Please try again !";
                   goto m;
               }
           }
           c++;
           cout<<"\n\n Do you want to buy another product ? if yes then press y else no ";
           cin >>choice;
        }
       while(choice=='y');
       cout<<"\n\n";
      cout<<c;
     
     cout<<"\n\n\t\t\t----------------------------RECEIPT-----------------------------\n";
     cout<<"\nProduct No \t Product name  \t Product quantity \t\tprice \t\tAmount \t Amount with discount \n";

     for(int i=0;i<c;i++)
     {   
         data.open ("database.txt",ios::in);
         data>>pcode>> pname >>price>>dis;
         while (!data.eof())
         {
             if(pcode==arrc[i])
             {
                 amount=price*arrq[i];
                 dis=amount-(amount*dis/100);
                 total=total+dis;
                 cout<<"\n"<<pcode<<"\t\t\t"<<pname<<"\t\t"<<arrq[i]<<"\t\t\t"<<price<<"\t\t"<<amount<<"\t\t"<<dis;
             }
           data>>pcode>>pname>>price>>dis;
         }
     
        
     data.close();
     }
   } 
   cout<<"\n\n -------------------------------------------------------------------------------";
   cout<<"\n total amount :"<<total;
}



int main()
{
    shopping p;
    p.menu();
}

