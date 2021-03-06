# Java Programming Language

## Java Quick reference
 * null, true, false are not keywords in java, they are literals
 * every local variable needs to be initialized, otherwise compiler says: variable `<variable_name>` might not have been initialized
 * equals() and == are different. == compares object references and equals() compares contents. If you overried equals() you sould also override hashCode().
 * keywords: strictfp, native
 * hiding or shadowing of of class data members
 * import package.* imports only all the classes in the package and not the sub-packages
 * Throwable is the base of Exception, RuntimeException and Error classes
 * 'marker interface': an interface such as Cloneable with no member definitions.
 * Error class is base class for errors generated by the JVM - such as OutOfMemoryError
 * Serializable interface provides default implementation for serialization of the objects.
 * Externalizable interface provides full control to the programmer for reading and writing objects into stream.
 * input/output streams are for byte streams. reader/writer streams are for character streams.
 * Runtime class provides methods to interact with garbage collector in JVM.
 * co-variant data is more specific type of the base type - a derived class from a base class. contra-variant is the opposite of co-variant.
 * finalize() can make an unreachable object rechable again. this is called by JVM garbage collector
 * static factory methods often require classes to have private constructors. such classes cannot be subclassed.
 * java.lang.String is a final class. it cannot be extended or sub-classed. same goes for other final classes.
 * byte data type is of 1 byte ( range -128 to 127 ).
 * char data type is of 2 bytes ( range 0 to 65535 )
 * static initialization block is called on first class reference
 * instance initialization block is called before constructor for every object that is being constructed
 * java allows only integral types to be used in switch statement - byte, short, char, int, Enum. long and float cant be used
 * static variables can't be declared inside a static method
 * if left operator of instanceof is null, the result is false
 * static methods in java can not be overridden, but they can be overloaded.
 * Static members of a class are resolved at compile-time. Calling a static method on an variable with null value will not result in a NullPointerException.
 * catch block can be ommitted for a try block if finally block is provided. finally block is executed regardless of whether an exception orccurred or not.

What is final, finalize and finally? 

A:

 * final - http://en.wikipedia.org/wiki/Final_(Java)
 * finalize - http://www.janeg.ca/scjp/gc/finalize.html
 * finally - http://download.oracle.com/javase/tutorial/essential/exceptions/finally.html

## Java Max Heap Size

In java 1.6.0_21 or later, or so...

    $ java -XX:+PrintFlagsFinal -version 2>&1 | grep MaxHeapSize
    uintx MaxHeapSize                         := 12660904960      {product}

## Java Concurrency

<http://www.vogella.com/articles/JavaConcurrency/article.html>
