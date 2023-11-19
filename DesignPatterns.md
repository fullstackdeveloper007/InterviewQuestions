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
    <td>Dependency Injection (DI) Pattern</td>
  </tr>
  </tbody>
</table>

##1. Singleton Pattern

Credit: https://www.youtube.com/watch?v=mFdFYm4RiDw

##2. Adapter Pattern
Adapter pattern is a structural design pattern which works as a bridge between two incompatible interfaces. It also known as a wrapper pattern. It allows the interface of an existing class to be used as another interface. Lets drill down the Adaptor pattern with an example, Suppose we have an export functionality in our application for ExporttoWord and Exporttoexcel like below

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

## 1. Factory Pattern
Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created

<ul>
  <li>
    Use the Factory Method when you don’t know beforehand the exact types and dependencies of the objects your code should work with
  </li>
  <li>
    The Factory Method separates product construction code from the code that actually uses the product. Therefore it’s easier to extend the product construction code independently from the rest of the code.
  </li>
  <li>
     Use the Factory Method when you want to save system resources by reusing existing objects instead of rebuilding them each time
  </li>
</ul>

For example, to add a new product type to the app, you’ll only need to create a new creator subclass and override the factory method in it.

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


