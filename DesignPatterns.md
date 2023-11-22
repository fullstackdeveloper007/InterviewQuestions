## Design Patterns

Desin patterns can be categorized as below:

**Creational patterns** provide object creation mechanisms that increase flexibility and reuse of existing code.

**Structural patterns** explain how to assemble objects and classes into larger structures, while keeping these structures flexible and efficient.

**Behavioral patterns** take care of effective communication and the assignment of responsibilities between objects.

<table>
  <tbody>
  <tr>
    <td>1.</td>
    <td>Singleton Pattern</td>
  </tr>
  <tr>
     <td>2.</td>
    <td>Adapter Pattern</td>
  </tr>
  <tr>
     <td>3.</td>
    <td>Factory Pattern</td>
  </tr>
   <tr>
      <td>4.</td>
    <td>Facade</td>
  </tr>
  <tr>
     <td>5.</td>
    <td>Repository Pattern</td>
  </tr>
    <tr>
       <td>6.</td>
    <td>Dependency Injection (DI) Pattern and IOC </td>
  </tr>
  </tbody>
</table>

##1. Singleton Pattern

Credit: https://www.youtube.com/watch?v=mFdFYm4RiDw


##2. Adapter Pattern

Adapter pattern is a structural design pattern which works as a bridge between two incompatible interfaces. It also known as a wrapper pattern. It allows the interface of an existing class to be used as another interface.It is often used to make existing classes work with others without modifying their source code. Lets drill down the Adaptor pattern with an example, Suppose we have an export functionality in our application for ExporttoWord and Exporttoexcel like below

Base inetrface "IExport" is defined with method decalration Save() so that exportToExcel and exporttoWord can make a uniform functionality.

<pre><code>
  public interface IExport{
    void Save();  
  }
</code></pre>

ExportToWord and ExportToExcel functionality is inherrting the generic Interface.

<pre><code>
public class ExportToWord:IExport{
  public void Save(){
    throw new NonImplementationException();    
  }  
}


public class ExportToExcel:IExport{
  public void Save(){
    throw new NonImplementationException();    
  }  
}  
</code></pre>

We can use the Export functioanlity like below.

<pre>
  <code>
  class program{
    static void main(string[] args){
      IExport ex= new ExportToWord();
      ex.Save();

      ex= new ExportToExcel();
      ex.Save();
    }     
  }
  </code>
</pre>

Lets assume, We are using a third party libarary for ExportToPdf and third party library has a method Export() like below not save() as have in Iexport interface.In this case we will not be able to use the generic way of export by calling a save() method for export. In this case we need to define a wrapper/Adapter class so that IExport can work uniformaly with third party libraray as well.

<pre><code>
  // Third party library has export functionality as below. 
  public class TpExportPdf{
    public vois Export(){  
    }
  }
</code></pre>

Now we need to define the wrapper/Adapter class to make the export functionality uniformaly.
<pre>
  <code>
    public class pdfExportAdapter:IExport{
       public void Save(){
          TpExportPdf obj= new TpExportPdf();//
          obj.Export();
        } 
    }    
  </code>
</pre>

 Now after defining the wrapper class. we can make a refrence of interface and initiate the class.

<pre>
  <code>
  class program{
    static void main(string[] args){
      IExport ex= new ExportToWord();
      ex.Save();

      ex= new ExportToExcel();
      ex.Save();

      ex= new pdfExportAdapter();
      ex.save();//through wrapper class we are able to use the same Interface. 
    }     
  }
  </code>
</pre>

## 3. Factory Pattern
Factory Method is a creational design pattern, it abstract the process of object creation and allows the object to be created at run-time when it is required. It basically centralized the object creation. 
Use the Factory Method when you don’t know beforehand the exact types and dependencies of the objects your code should work with
 
Factory allows the consumer to create new objects without having to know the details of how they're created, or what their dependencies are - they only have to give the information they actually want.

The another advantage of factory pattern is decopling of one class from the other. change at one place and reflect at many places.

<div>  
**Pros**  
  <ul>
    <li>
      You avoid tight coupling between the creator and the concrete products.</li>
    <li>
        Single Responsibility Principle You can move the product creation code into one place in the program, making the code easier to support.
    </li>
    <li>
      Open/Closed Principle</em>. You can introduce new types of products into the program without breaking existing client code.
     </li>
  </ul>
</div>
<div>
  
 **Cons**
   
<ul>
<li>
  The code may become more complicated since you need to introduce a lot of new subclasses to implement the pattern. The best case scenario is when you’re introducing the pattern into an existing hierarchy of creator classes.</li>
</ul>
</div>

## Implementation 
<pre><code>  
namespace DesignPattern
{
    public interface Itax {
        void Calculate();    
    }
    public class GstTax : Itax
    {
        public void Calculate()
        {
            throw new NotImplementedException();
        }
    }

    public class VatTax : Itax
    {
        public void Calculate()
        {
            throw new NotImplementedException();
        }
    }

    public class newTax : Itax
    {
        public void Calculate()
        {
            throw new NotImplementedException();
        }
    }

    //Client 
    public class programe
    {
        public static void main()
        {
          //without factory pattern, we are exposing the implemantion and if any 
          //dependency is there we are exposing that as well to the client.
  
            Itax tax = new GstTax();
            tax.Calculate();

            //or 
            tax = new VatTax();
            tax.Calculate();            
        }
    }

    //Factory Pattern Implementation
    public static class Factory {
        public static Itax CreateInstance(int type)
        {
            //In factory pattern we centralize the class initiation and If any dependecies are there we can handle it here only 
            //at a central place and the client need not to know the implementation. 
            //If any new tax type comes up,client implementaion will not change just they will pass new type and we can make instance of 
            //that class type and return type. 
            if (type == 1)
            {                
                return new GstTax();
            }
            else
            {
                return new VatTax();
            }
        }
    }  
}

//After factory pattern, the class initialization is hidden and can be used like below. 
public class programe
{
    public static void main()
    {
        Itax x=Factory.CreateInstance(1);
        x.Calculate();
    }
}
</code></pre>

## DI Injction Pattern
Dependency Injection is one of the subtypes of the IOC principle.

## 2. 
 
### Solid Principle 
https://www.c-sharpcorner.com/UploadFile/damubetha/solid-principles-in-C-Sharp/
SOLID is an acronym for the first 5 principles of object-oriented design:

**SRP** The Single Responsibility Principle: -- a class should have one, and only one, reason to change.

**OCP** The Open Closed Principle: -- you should be able to extend a class's behavior, without modifying it.

**LSP** The Liskov Substitution Principle: -- derived classes must be substitutable for their base classes.

**ISP** The Interface Segregation Principle: -- make fine grained interfaces that are client specific.

**DIP** The Dependency Inversion Principle -- depend on abstractions not on concrete implementations.
 
 <div>
  
**Ref. Links** https://www.dofactory.com/net/design-patterns
  
**Ref. Links** https://refactoring.guru/design-patterns/catalog
  </div>
# Liskov Substitution Principle:
The Liskov Substitution Principle (LSP) states, "you should be able to use any derived class instead of a parent class and have it behave in the same manner without modification.". It ensures that a derived class does not affect the behavior of the parent class; in other words, a derived class must be substitutable for its base class.

This principle is just an extension of the Open Closed Principle, and we must ensure that newly derived classes extend the base classes without changing their behavior. I will explain this with a real-world example that violates LSP.


