---
layout: post
title: C++ Generic Lazy Loader Implementation

tags: C++,Design Patterns,Lazy Execution,Lazy Loading,Programming
---
<p><a href="http://en.wikipedia.org/wiki/Lazy_loading">Lazy loading</a> is a <a href="http://en.wikipedia.org/wiki/Design_pattern_(computer_science)">software design pattern</a> that delays the initialization of resources until the first time they are to be used inside of an application. Thus, for certain applications that rarely use memory intensive resources, you only need to initialize when there is a guarantee it is to be used. This has obvious performance and efficiency benefits. As a C++ programmer by trade I find it rather irritating that there is not a generic class that automatically handles lazy loading for me. So like any good lazy fuck I decided to spend a few hours and write one of my own. I currently have two use cases for this little tidbit.</p>
<p>When you have available a default construct its use is quite simple and straight forward. This object allocates the class with the default constructor when it is first called directly through any of the accessor <strong>operators</strong>, or directly with the <strong>get</strong> method. In this particular example when loaded it correctly returns the unique identifier.  
<pre lang="cpp">
class Unique
{
public:
    Unique() 
        : m_uuid(boost::uuids::random_generator()())
    {
    }

    const boost::uuids::uuid& uuid()
    {
        return m_uuid;
    }
private:
    boost::uuids::uuid m_uuid;
};

int main(int argc, char* argv[])
{
    thunk::lazy_loader<Unique> loader;

    const boost::uuids::uuid& u = loader->uuid();

    std::cout<<"uuid: "<<boost::lexical_cast<std::string>(u)<<std::endl;    

    return 0;
}
</pre></p>
<p>The second example uses a boost function structure as a factory method, and it is executed instead of the default constructor. The factory method takes a reference to a boost shared pointer and correctly calls the constructor with any obligatory parameters. The boost shared pointer is owned by the lazy loader implementation and is used to maintain a reference counted state.
<pre lang="cpp">

class Unique
{
public:
    Unique() 
        : m_uuid(boost::uuids::random_generator()())
    {
    }

    Unique(const boost::uuids::uuid& u)
        : m_uuid(u)
    {
    }

    const boost::uuids::uuid& uuid()
    {
        return m_uuid;
    }
private:
    boost::uuids::uuid m_uuid;
};

static void factory(boost::shared_ptr<Unique>& impl)
{
    impl = boost::shared_ptr<Unique>(
        new Unique(boost::uuids::nil_uuid()) );
}

int main(int argc, char* argv[])
{
    thunk::lazy_loader<Unique> loader(&factory);

    const boost::uuids::uuid& u = loader->uuid();

    std::cout<<"uuid: "<<boost::lexical_cast<std::string>(u)<<std::endl;    

    return 0;
}
</pre></p>
<p>I am still working on a better method for initializing with a <i>n-argument</i> constructor. I have made my current progress available on my <a href="http://github.com/THUNKbrightly/lazy_loader">Github.com repository</a> available for use with the standard three-clause BSD license. If you have any questions or bugfixes please feel free to submit them through <a href="http://github.com/">Github</a>.</p>
