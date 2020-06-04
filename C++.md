# C++ Notes
## 线程安全
### 线程安全的对象构造
唯一的要求是在构造期间是在构造期间不要泄露this指针，即
* 不要在构造函数中注册任何回调
* 也不要在构造函数中把this传给跨线程的对象
* 即使在构造函数的最后一行也不行
### 线程安全的析构：智能指针
* shared_ptr
* weak_ptr
* scoped_ptr
* boost::noncopyable
* boost::enable_shared_from_this  
* MutexLock MutexLockGuard
### 线程同步的四项原则
* 首要原则是尽量最低限度地共享地共享对象，减少需要同步的场合。优先考虑immutable对象
* 其次是使用高级的并发编程构件，如TaskQueue、Producer-Consumer Queue、CountDownLatch等
* 最后不得已必须使用底层同步原语时，只用非递归的互斥器和条件变量， 慎用读写锁， 不要用信号量。
* 除了使用atomic整数外，不自己编写lock-free代码，也不要使用内核级同步原语。
### 线程安全的Singleton
```C++
template<typename T>
class Singleton : boost::noncopyable
{
    public:
        static T& instance()
        {
            pthread_once(&ponce_, &Singleton::init);
            return *value_;
        }
    private:
        Singleton();
        ~Singleton();

        static void init()
        {
            value_ = new T();
        }

        static pthread_once_t ponce_;
        static T* value_;
};

template<typename T>
pthread_once_t Singleton<T>::ponce_ = PTHREAD_ONCE_INIT;
template<typename T>
T* Singleton<T>::value_ = NULL;


Foo& foo = Singleton<Foo>::instance();
```