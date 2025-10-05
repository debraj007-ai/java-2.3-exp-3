import java.util.*;
import java.util.stream.*;

class Employee { String name; int age; double salary; Employee(String n,int a,double s){name=n;age=a;salary=s;} public String toString(){return name+" | "+age+" | "+salary;} }
class Student { String name; double marks; Student(String n,double m){name=n;marks=m;} }
class Product { String name; double price; String category; Product(String n,double p,String c){name=n;price=p;category=c;} public String toString(){return name+"("+price+")";} }

public class Main {
    public static void main(String[] args) {

        List<Employee> emp = Arrays.asList(new Employee("Alice",30,55000), new Employee("Bob",25,60000),
                                           new Employee("Charlie",35,50000), new Employee("Diana",28,65000));
        emp.stream().sorted((a,b)->a.name.compareToIgnoreCase(b.name)).forEach(System.out::println);
        System.out.println();
        emp.stream().sorted(Comparator.comparingInt(e->e.age)).forEach(System.out::println);
        System.out.println();
        emp.stream().sorted((a,b)->Double.compare(b.salary,a.salary)).forEach(System.out::println);

      
        List<Student> stu = Arrays.asList(new Student("Alice",82.5), new Student("Bob",68.0),
                                          new Student("Charlie",91.0), new Student("Diana",74.5), new Student("Ethan",88.0));
        System.out.println("\nStudents >75 marks:");
        stu.stream().filter(s->s.marks>75).sorted(Comparator.comparingDouble(s->s.marks))
           .map(s->s.name).forEach(System.out::println);


        List<Product> pro = Arrays.asList(new Product("Laptop",1200,"Electronics"), new Product("Smartphone",800,"Electronics"),
                                         new Product("Headphones",150,"Electronics"), new Product("T-Shirt",25,"Clothing"),
                                         new Product("Jeans",60,"Clothing"), new Product("Blender",100,"Home Appliances"),
                                         new Product("Microwave",200,"Home Appliances"));

        System.out.println("\nProducts grouped by category:");
        pro.stream().collect(Collectors.groupingBy(p->p.category)).forEach((c,l)->System.out.println(c+": "+l));

        System.out.println("\nMost expensive per category:");
        pro.stream().collect(Collectors.groupingBy(p->p.category,Collectors.maxBy(Comparator.comparingDouble(p->p.price))))
           .forEach((c,p)->System.out.println(c+": "+p.get()));

        double avg = pro.stream().collect(Collectors.averagingDouble(p->p.price));
        System.out.println("\nAverage price: "+avg);
    }
}
