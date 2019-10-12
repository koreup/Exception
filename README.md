# Exception




1. understand, recognize and appreciate the value of using exceptions 
```javascript
    try{
        // code to be tested
	throw exception;
    }catch(type exception){
        // code to be executed 
    }

```



2. understand the types of errors and exceptions
3. identify types of exceptions and their occurrences
4. understand throwing an exception 
7. demonstrate try catch block and throw
```javascript
#include <iostream>
#include<string> 
using namespace std;
void errCreator(){
    bool intError =false;
    bool strError =false;
    bool strObjError=true;
    if(intError){
        throw 110; // when error type is int 
    }
    if(strError){
        throw "string"; //when error type is string  
    }if(strObjError){
        throw string("string object!"); //when error type is string object created by string class
    }
}
 
int main()
{
    try{
        errCreator();
    }catch(int e){
        cout<<"Error message for type int: "<<e<<endl;
    }catch(char const * e){ // if type of error is string, we need to catch it w/ char const *(pointer) 
        cout<<"Error message for type string: "<<e<<endl;
    }catch(string &e){ // catch an object with reference symbol "&"
        cout<<"Error message for type string object: "<<e<<endl;
    }
    return 0;
}

```

5. create few example types of  exceptions; ex. you can try array out of bounds exception, file not found and more
```javascript
 
#include <iostream.h>

int main () {
  char myarray[10];
  try
  {
    for (int n=0; n<=10; n++)
    {
      if (n>9) throw "Out of range";
      myarray[n]='z';
    }
  }
  catch (char * str)
  {
    cout << "Exception: " << str << endl;
  }
  return 0;
}

```

6. identify Exception-Safe Implementation Techniques such as try block and ‘‘resource acquisition is initialization’’ technique ( RAII)
7. demonstrate try catch block and throw
8. demonstrate RAII
```javascript
#include <iostream>
#include <exception>
#include <memory> //unique_ptr: if only one obj needs access to the underlying pointer  (smart pointer)


class Speaker{
    private:
        std::string name;
    public:
        Speaker(){
            std::cout<< "Default constructing \"\""<<std::endl;   
        }
        Speaker(std::string n) : name(n){
            std::cout<<" constructing \""<<name<<"\""<<std::endl;// constructor acquires resorce
        }
        ~Speaker(){
            std::cout<<"Destructing \""<<name<<"\""<<std::endl; //Destructor releases resource
        }
    
};

void RAIIexample()
{
    try{
        Speaker spk("Hey");
        // Speaker* pt{new Speaker{"dynamically allocated an obj in the heap"}};      //raw pointer doesn't have a destructor, so manual deletion is required
        std::unique_ptr<Speaker> pt{new Speaker{"dynamically allocated an obj in the heap"}}; // unique pointer comes with a destructor, so we don't need to manually delete it
        throw (std::exception{"Throw a message plz!"});
        // delete pt;
    }catch(const std::exception& e){
        std::cout <<"Exception caught: "<< e.what()<<std::endl;
    }
}

int main()
{
    // Speaker nonamehere;
    // Speaker spk("Spiderman");
    
    RAIIexample();
    return 0;
}

```


9. write your own exception by extending std::exception class
```javascript
#include <iostream>
#include <exception> // what()
using namespace std;

class MyException: public exception{
    public:
        virtual const char* what() const throw(){
            return "Oops, something went wrong!";
        }
};

class Test{
    public:
        void somethingWentWrong(){
            throw MyException();
        }
};

int main () {
  Test test;
  try{
      test.somethingWentWrong();
  }
  catch(MyException &e){
      cout << e.what() <<endl; 
  }
  return 0;
}
```
