# C#

<table>
  <tbody>
  <tr>
    <td>      1    </td>
     <td> Accessibility Levels in C#  </td>
  </tr>
  <tr>
    <td>     2    </td>
     <td>  Diff btwn Partiall class and Extension method    </td>
  </tr>
   <tr>
    <td>     3    </td>
     <td>   </td>
  </tr>
  
  </tbody>
</table>

### 1. Accessibility Levels in C#

- **public**:
  - The type or member can be accessed by any other code in the same assembly or another assembly that references it.
  - The accessibility level of public members of a type is controlled by the accessibility level of the type itself.

- **private**:
  - The type or member can be accessed only by code in the same class or struct.

- **protected**:
  - The type or member can be accessed only by code in the same class, or in a class that is derived from that class.

- **internal**:
  - The type or member can be accessed by any code in the same assembly, but not from another assembly. In other words, internal types or members can be accessed from code that is part of the same compilation.

- **protected internal**:
  - The type or member can be accessed by any code in the assembly in which it's declared, or from within a derived class in another assembly.

- **private protected**:
  - The type or member can be accessed by types derived from the class that are declared within its containing assembly.

### 2. Diff btwn Partiall class and Extension method


