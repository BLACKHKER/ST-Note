```c++
#include <iostream>
#include <string>

class Entity 
{
public:
    int x;
public:
    void Print() const
    {
        std::cout << "Hello" << std::endl;
    }
};

class ScopedPtr
{
private:
    Entity* m_Obj;
public:
    ScopedPtr(Entity* entity) 
        :m_Obj(entity)
    {

    }

    ~ScopedPtr()
    {
        delete m_Obj;
    }
};

int main()
{
    ScopedPtr ptr = new Entity();
    
}
```

