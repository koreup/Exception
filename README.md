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
7.demonstrate try catch block and throw
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
