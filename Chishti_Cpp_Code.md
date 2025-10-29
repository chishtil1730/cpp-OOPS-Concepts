Test code with all the topics included

```bash
#include <iostream>
#include <iomanip>
using namespace std;

//Inheritance & PolyMorphism
class Father {
public:
    void method() {
        cout << "Hello from father" << endl;
    }
};

class Child : public Father {
public:
    //Inheriting.
    void print() {
        cout << "Child method but inherited from father->";
        method();
    }
    //Method Overriding
    void method(){
        cout << "overridden child";
    }
};


//Templates are nothing but Generics in Java
//For generic classes
template <class T>
class Generic {
    public:
        T data;
        void printData() {
            cout << data << endl;
        }

        T getData() {
            return data;
        }
};

class nonGeneric {
    public:
        int data;
        template <typename T>
        void printStuff(T stuff) {
            cout << stuff << endl;
        }
};

//Object passed as parameter.
class Sum {
    private:
        string name="Chishti";
    public:
        int num=0;
        int sum(Sum &obj) {
            return num + obj.num;
        }
        Sum(int num) {
            this->num = num;
        }
        //Method return class Type or Object of class.
        Sum changeName(Sum &obj) {
            obj.name = "Changed name Chishti";
            return obj;
        }

    string getName() {
            return name;
        }

};


//Static Class

class StExample{
    static string name;
public:

    static void display(string name) {
        cout << name << "\n";
    }
    static void setName(string newName) {
        name = newName;
    }

};


//Friendly functions & InnerClass.
class Box {
private:
    int width;
    const string  Name = "Max";
public:

    class InnerBox {
    public:
        int innerWidth=10;
        InnerBox(int innerWidth) {
            this->innerWidth = innerWidth;
        }
    };

    //Friendly function can access the private data though it is public
    Box() : width(0) {}//Box width is set to 0.(Constructor Initialisation).
    friend void setWidth(Box& b, int w);
    friend string getName(Box &b);

    //Can access here. But if it is written outside, it will not get the access.
    string getName() {
        return Name;
    }

};

void setWidth(Box& b, int w) {
    b.width = w; // Accessing private member
    cout << "Width is set to: " << b.width << endl;
}





//Object Passed as parameter for Copy Constructor.
class Test{
public:
    int roll;
    string name;
    Test(int roll, string name){
        this->roll = roll;
        this->name = name;
    }

    Test(Test &obj){//Copy Constructor.
        this->roll = obj.roll;
        this->name = obj.name;
    }

    //Method overloading.
    void print() const{
        cout<<"Hello "<<name<<endl;
    }
    static void print(string name ) {
        cout<<"Hello "<<name<<endl;
    }
};

int main() {
    //Inheritance & PolyMorphism
    Father father;
    father.method();
    Child child;
    child.method();
    cout<<"\n\n";
    child.print();


    //Generic class and Generic function.
    Generic<int> genObj;
    genObj.data = 10;
    int data = genObj.getData();
    cout <<"Generic class: " <<data << endl;
    Generic<double> genObj2;
    genObj2.data = 10.5;
    double doublevalue = genObj2.getData();
    cout <<"Generic class: "<<doublevalue << "\n\n";

    //Genericfunciton
    nonGeneric nonObj;
    nonObj.data = 10.5;
    nonObj.printStuff("Generic function data\n\n");



    //Static class calling
    //string name = StExample::name; //Like Class.parameter in java
    StExample::display("ChishtiL1730");

    //*********Important**********//
    // "::" is used for calling InnerClasses or methods from static classes.


    Sum sum1(10);
    Sum sum2(20);

    Sum sum3 = sum3.changeName(sum2);
    cout<<"Changed name: "<<sum3.getName()<<endl;


    cout<<"Object passed as parameter sum: "<<sum1.sum(sum2)<<endl;


    // "::" is used for calling InnerClasses or methods from static classes.
    Box::InnerBox innerBoxObj(20);
    cout<<"Width of inner Box is: "<<innerBoxObj.innerWidth<<endl;

    Test *obj = new Test(0,"Max");
    obj->print();

    //Copied Object from Copy Constructor
    Test *obj3(obj);
    obj3->print();

    Test obj2(1,"Verstappen");
    obj2.print();
}

```
