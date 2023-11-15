## In below code we are using two for loop to assign the departemnts to students. Can we optimize the code
<pre><code>
class Department
{
    public string DepartmentName { get; set; }
}

class Student
{
    public string StudentName { get; set; }
    public string DepartmentName { get; set; }
    public Department Dept { get; set; }
}

class Program
{
    static void Match(List<Department> lstDept, List<Student> lstStd)
    {
        foreach (Student std in lstStd)
        {
            var dept = lstDept.FirstOrDefault(d => d.DepartmentName == std.DepartmentName);
            if (dept != null)
            {
                std.Dept = dept;
            }
        }
    }
}
</code></pre>

## 1. Try below.
<pre><code>
class Department
{
    public string DepartmentName { get; set; }
}

class Student
{
    public string StudentName { get; set; }
    public string DepartmentName { get; set; }
    public Department Dept { get; set; }
}

class Program
{
    static void Match(List<Department> lstDept, List<Student> lstStd)
    {
        var deptDictionary = lstDept.ToDictionary(d => d.DepartmentName, d => d);

        foreach (Student std in lstStd)
        {
            if (deptDictionary.TryGetValue(std.DepartmentName, out var dept))
            {
                std.Dept = dept;
            }
            else
            {
                std.Dept = null; // Set to null if department not found
            }
        }
    }
}
</code></pre>

## 2. Try Below
<pre><code>
class Department
{
    public string DepartmentName { get; set; }
}

class Student
{
    public string StudentName { get; set; }
    public string DepartmentName { get; set; }
    public Department Dept { get; set; }
}

class Program
{
    static void Match(List<Department> lstDept, List<Student> lstStd)
    {
        lstDept.Sort((d1, d2) => d1.DepartmentName.CompareTo(d2.DepartmentName));

        foreach (Student std in lstStd)
        {
            var index = BinarySearchDepartment(lstDept, std.DepartmentName);
            if (index >= 0)
            {
                std.Dept = lstDept[index];
            }
        }
    }

    static int BinarySearchDepartment(List<Department> lstDept, string departmentName)
    {
        int left = 0;
        int right = lstDept.Count - 1;

        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            int comparison = lstDept[mid].DepartmentName.CompareTo(departmentName);

            if (comparison == 0)
            {
                return mid; // Match found
            }
            else if (comparison < 0)
            {
                left = mid + 1; // Search in the right half
            }
            else
            {
                right = mid - 1; // Search in the left half
            }
        }

        return -1; // No match found
    }
}  
</code></pre>
