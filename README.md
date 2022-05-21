# Sample-Code-for-internship
This program is built using C++ language. It can be used in companies to keep records of their employee. They can perform multiple tasks for instance addEmployee, DeleteEmployee, updateEmployee information and search for a specific employee. The program consists of 2 classes Employee and HRM.


#include<iostream>
#include<fstream>
#include<string>

using namespace std; 

// This is a final project program called Human Resource Management program. 
// This program is built using C++ language. 
// HRM program can be used in companies to keep records of their employee.
// They can perform multiple tasks for instance addEmployee, DeleteEmployee, updateEmployee information and search for a specific employee.
// The program consists of 2 classes Employee and HRM. 


// we make a counter global and set the initial value to 1000
int counter=1000;
// Making Employee class

class Employee
{
    // declaring variables in private class as per requirements.
    private:
        int empID;
        string Firstname;
        string Lastname;
        float workinghours;
        float costPerhour;
        float deduction;
        double annualSalary;
     
    //declaring variables in public class as per requirements and will be used through out the program   
    public:
     
     // making constructor
    Employee()
    {
        // incrementing the counter and setting empID equal to to counter so that it automatically increases by 1.
        counter++;
        empID=counter;
    }
       
     //making of getting funtions  
     
    int get_empID()
    {
        return empID;
    }
    
    string get_Firstname()
    {
        return Firstname;
    }
    
    string get_Lastname()
    {
        return Lastname;
    }
    
    float get_workinghours()
    {
        return workinghours;
    }
    
    float get_costPerhours()
    {
        return costPerhour;
    }
    
    float get_deduction()
    {
        return deduction;
    }
    
    double get_annualSalary()
    {
        // formula used to calculate annualSalary
        annualSalary=(workinghours * costPerhour * 52) - (52 * deduction);
    // setting validation of salary using if else statements (if less than or equal to zero return to 0)
        if(annualSalary <= 0)
         {
            return 0;
         }
        
        else
        {
            return annualSalary;
        }
    }
    
    
    // Making setting functions which will be used to set values
    void set_Firstname(string fn)
    {
        Firstname=fn;
    }
    
    void set_Lastname(string ln)
    {
        Lastname=ln;
    }
    
    void set_workinghours()
    {
        float h;
        cout<< "Enter your weekly working hours"<<endl;
        cin>>h;
        
        // validating weeking hours using while statement (must be between 1 and 60)
        
        while( h<1 || h>60)
        {
            cout <<"Kindly re-enter the number of hours again should be between 1 and 60"<< endl;
            cin>>h;
        }
        // setting after validating
        
        workinghours=h;
    }
    
    void set_costPerhour()
    {
        float c;
        cout<<"Enter your hourly wage"<<endl;
        cin>> c;
        
        // validating hourly wage using while statement (must be more than 0)
        while(c<0)
        {
            cout<<" Kindly re-enter your weekly wage must be more than 0"<< endl;
            cin>> c;
        }
        // setting after validating
        costPerhour=c;
    }
    
    void set_deduction()
    {
        float d;
        cout<<"Enter the deduction amount"<<endl;
        cin>>d;
        
        // validating deduction amount using while statement
        while(d<0)
        {
            cout<<"Kindly re-enter the deduction amount must be more than 0"<<endl;
            cin>>d;
        }
        // setting after validating
        
        deduction=d;
    }
    
    void set_Ewage(int wage)
    {
        costPerhour=wage;
    }
    
    void set_Ededuction(int Deduction)
    {
        deduction=Deduction;
    }
    
    void set_EworkH(int w)
    {
        workinghours=w;
    }
};


// HRM Class

// using separate counter for hrm class
int counter1=0;

// making HRM class to hold all maing functions like addEmployee, DeleteEmployee etc
class HRM
{
    // used public to declare variables and functions as per requirements
    public:
        Employee E[1000];
        int aEmp;
        
        // This funtions reads values from the employee.txt file
        void DataFromFile(string Fname,string Lname, int week, int wage, int ded)
        {
            // setting aEmp equal to counter so that it can incrment after every iteration
            aEmp=counter1;
            
            // will set data of emplyee from txt file
            E[aEmp].set_Firstname(Fname);
            E[aEmp].set_Lastname(Lname);
            E[aEmp].set_EworkH(week);
            E[aEmp].set_Ewage(wage);
            E[aEmp].set_Ededuction(ded);
            // increase the counter by 1
            counter1++;
        }
        
        // funtions that will be used to add new emplyee info
        void addEmployee()
        {
            bool cont= true;
            char YN;
            // using do while loop
            do
            {
                string Fn,Ln; // declaring Fn and Ln
                aEmp=counter1; // setting counter equal to aEmp
                
                // asking user for new employee information
                cout<<"Enter the first name "<< endl;
                cin>>Fn;
                E[aEmp].set_Firstname(Fn);
                
                cout<<"Enter the last name "<<endl;
                cin>>Ln;
                E[aEmp].set_Lastname(Ln);
                
                E[aEmp].set_workinghours();
                
                E[aEmp].set_costPerhour();
                
                E[aEmp].set_deduction();
                
                // displaying the information given
                cout<<"Employee ID  FirstName  LastName  Salary per year ($)"<<endl;
                cout<<"-----------  ---------  --------  -------------------"<<endl;
                cout<<E[aEmp].get_empID()<<"        "<<E[aEmp].get_Firstname()<<"         "<<E[aEmp].get_Lastname()<<"         "<< E[aEmp].get_annualSalary()<<endl;
                
                cout<< "Would you like to add another employee (Y/N)"<< endl;
                cin>>YN;
                // using if statement to stop loop if user wishes not to continue
                if (YN=='N'|| YN=='n')
                {
                    cont=false;
                }
                counter1++;
                 
                // using if statement to display message that total count 100 reached
                if(aEmp==100)
                {
                    cout<<"Total count 100 employees reached!!!"<<endl;
                    break;
                }
        
            }
            while(cont);
            
        }
        // making Search funtion to find employee using employee ID
        int SearchEmployee(int ID)
        {
            // initializing location to -5
            int loc=-5;
            bool found=false;
            bool cont=true;
            char YN;
            
            // using for loop through in array
            
            for(int i=0; i<aEmp+1;i++)
            { 
                // if entered id equals to id in array then set location t0 i 
                if(E[i].get_empID()==ID)
                {
                    found= true;
                    
                    loc=i;
                }
            }
            if(!found) // if id not found display following message
            {
                cout<<"Employee with given ID not found"<< endl;
            }
            return loc;
            
        }
        
        // maing DeleteEmployee funtion if the user wishes to DeleteEmployee information from records
        void DeleteEmployee()
        {
            int ID;
            char YN;
            bool cont=true;
            int n;
            
            // using do while loop
            do
            {
                //asking user for id
                cout<<"Enter employee ID"<<endl;
                cin>>ID;
                // calling SearchEmployee funtions to check for his id
                n=SearchEmployee(ID);
                
                //continue if n!=-5
                if(n!=-5)
                {
                    // asking user if he wishes to delete employee information
                    cout<<"Would you like to delete the following employee"<<endl;
                    cout<<E[n].get_Firstname()<<"  "<<E[n].get_Lastname()<<"  "<<"YES/NO!!"<<endl;
                    cin>>YN;
                    
                    // if he says y then continue
                    if(YN=='y' || YN=='Y')
                    {
                        cout<< "Employee" <<E[n].get_Firstname()<<"  "<< E[n].get_Lastname()<<" is deleted " << endl;
                        
                        for (int i=n;i<aEmp;i++)
                        {
                            // moves the index eg: we delete i=2 then it will be i=2+1 and in array it will be [1,3,4,]
                            E[i]=E[i+1];
                        }
                        
                        // reduce the number of Employee
                        aEmp--;
                        counter1--;
                    }
                    
                }
                 // if not then do this 
                else 
                {
                    cout<<"Employee not deleted"<<endl;
                }
                // ask if he wants to delete more employees
                cout<<"Would you like to delete another employee"<<endl;
                cin>>YN;
                if(YN=='N' || YN== 'n')
                {
                    cont=false;
                }
                
            }
            while(cont);
        }
         // maing updateEmployee funtions to update information
        void updateEmployee()
        {
            int n;
            int ID;
            char YN, YN1;
            bool cont= true;
            bool cont1= true;
            int location;
            
            // using do while loop
            do 
            {
                cout<<"Enter employee ID: "<<endl;
                cin>>ID;
                
                //calling search funtion to find employee using his id
                location=SearchEmployee(ID);
                bool cont1=true;
                while(cont1){
                    if(location!=-5) // continue if id is found means given id found
                    {
                        // giving user choice to update specific field 
                        cout<<"What would you like to update choose from the following options"<<endl;
                        cout<<"1. Firstname"<<endl;
                        cout<<"2. Lastname"<<endl;
                        cout<<"3. Working hours"<<endl;
                        cout<<"4. hourly Wage"<<endl;
                        cout<<"5. Deduction"<<endl;
                        
                        cin>>n;
                        string fName,lName;
                         // using switch case to jump to user choice
                        switch(n)
                        {
                            case 1:
                                cout<<"Enter new firstname "<< E[location].get_Firstname()<<endl;
                                cin>>fName;
                                E[location].set_Firstname(fName);
                                break;
                                
                            case 2:
                                cout<<"Enter new lastname "<< E[location].get_Lastname()<<endl;
                                cin>>lName;
                                E[location].set_Lastname(lName);
                                break;
                                
                            case 3:
                                cout<<"Enter new working hours "<<endl;
                                E[location].set_workinghours();
                                // calculating annualSalary again
                                E[location].get_annualSalary();
                                break;
                            
                            case 4:
                                cout<<"Enter new hourly wage "<<endl;
                                E[location].set_costPerhour();
                                // calculating annualSalary again
                                E[location].get_annualSalary();
                                break;
                                
                            case 5:
                                cout<<"Enter new Deduction amount "<<endl;
                                E[location].set_deduction();
                                // calculating annualSalary again
                                E[location].get_annualSalary();
                                break;
                                
                            default: // using default if user enter number except 1 to 5
                                cout<<"Enter your choice from 1 to 5 "<<endl;
                                break;
                                
                        }
                        // asks if he wants to update something else
                        cout<<"would you like to update another field of employee(Y/N)"<<endl;
                        cin>>YN1;
                        // if no then say updated
                        if (YN1=='N' || YN1=='n')
                        {
                            cout<< "The info of employee " <<E[location].get_Firstname()<<"is updated "<<endl;
                            cont1=false;
                        }
                    }
                    else
                    {
                        break;
                    }
                }
                // ask if he wants to update another employee information
                cout<< "Do you want to repeat update by entering new employee ID (Y/N)"<<endl;
                cin>>YN;
                
                if(YN=='N' || YN=='n')
                {
                    cont=false;
                }
                
            }
            while(cont);
        }
        
};


// making menu function to display menu
void menu()
{
    cout<< "WElCOME TO HUMAN RESOURCE MANAGEMENT PROGRAM"<< endl;
    cout<< "--------------------------------------------"<< endl;
    
    cout<<"{Choose one of the following options}"<<endl;
    
    cout<<"1. Add person"<<endl;
    cout<<"2. Delete person"<<endl;
    cout<<"3. Update information"<<endl;
    cout<<"4. Search for employee"<<endl;
    cout<<"5. Quit"<<endl;
    
    cout<<"---------------------------------------------"<<endl;
    
    cout<<"Enter your choice: "<<endl;
}

// int main function
int main()
{
    HRM hrm; // objectifying hrm to call hrm class
    
    //Employee emp[10];
    ifstream inf;
    inf.open("employee.txt"); // open file
    
    int eid;
    string firstname, lastname;
    float weeklyh, wage, deduc;
   
   while(!inf.eof())
   {
       inf>>eid;          // reading data from file
       inf>>firstname;    // reading data from file
       inf>>lastname;     // reading data from file
       inf>>weeklyh;      // reading data from file
       inf>>wage;         // reading data from file
       inf>>deduc;        // reading data from file
       
       if(inf.eof()) // eof means end of file so if data ends then break
       {
           break;
       }
       
       // calling DataFromFile funtion
       hrm.DataFromFile(firstname,lastname,weeklyh,wage,deduc);
     
       
   }
    inf.close();
    
    bool cont= true;
    char y;
    
     int choice=0; 
     int IDD;
     // using do while loop 
    do
    {
        menu();
        cin>>choice;
        // using switch case to jump to user desired choice
        switch(choice)
        {
            case 1:
            {
                hrm.addEmployee();
            break;
            }
            case 2:
            {
                hrm.DeleteEmployee();
            break;  
            }
            case 3:
            {
                hrm.updateEmployee();
            break;
            }
            case 4:
            {
                bool cont_2=true;
                do{
                    // asking for id
                    cout<<"Please enter employee ID "<< endl;
                    cin>>IDD;
                    // searching
                    int nn=hrm.SearchEmployee(IDD);
                    
                    if(nn!=-5)
                    {
                cout<<"Employee ID First Name Last Name  Salary per year($)"<<endl;
                cout<<"----------- ---------- ---------- ----------------------"<<endl;
                cout<<"  "<<hrm.E[nn].get_empID()<<" /t"<<hrm.E[nn].get_Firstname()<<"/t  "<<hrm.E[nn].get_Lastname()<<"/t "<<hrm.E[nn].get_annualSalary()<<endl;
                    }
                    // ask if wishes to search again
                    cout<< "Would you like to search again (Y/N) "<<endl;
                    cin>>y;
                    
                    if(y=='n' || y=='N')
                    {
                        cont_2=false;
                    }
                }while(cont_2);
                
            break;
            }
            case 5:
            cout<<"Bye!!!"<<endl; // say him bye if  he chosses to quit
            break;
            default: // if any other number then 1 to 5 then go to default
            cout<< "Enter new choice: "<<endl;
            break;
            
        }
    }
    while (choice !=5);
    
}

