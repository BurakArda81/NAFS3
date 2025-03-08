# NAFS3

using System;

// Çalışan sınıfı (Base Class)
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public double Salary { get; set; }
    public string Department { get; set; }

    public Employee(int id, string name, double salary, string department)
    {
        Id = id;
        Name = name;
        Salary = salary;
        Department = department;
    }

    public virtual double CalculateBonus()
    {
        return 0;
    }
}

// Yönetici sınıfı (Derived Class)
public class Manager : Employee
{
    public int TeamSize { get; set; }

    public Manager(int id, string name, double salary, string department, int teamSize)
        : base(id, name, salary, department)
    {
        TeamSize = teamSize;
    }

    public override double CalculateBonus()
    {
        return Salary * 0.2;
    }
}

// Geliştirici sınıfı (Derived Class)
public class Developer : Employee
{
    public string About { get; set; }

    public Developer(int id, string name, double salary, string department, string about)
        : base(id, name, salary, department)
    {
        About = about;
    }

    public override double CalculateBonus()
    {
        return Salary * 0.1;
    }
}

// Banka Hesabı sınıfı
public class BankAccount
{
    public string AccountHolder { get; set; }
    public double Balance { get; set; }

    public BankAccount(string accountHolder, double balance)
    {
        AccountHolder = accountHolder;
        Balance = balance;
    }

    public virtual void CalculateInterest()
    {
        
    }
}

// Vadeli Hesap (Derived Class)
public class SavingsAccount : BankAccount
{
    public SavingsAccount(string accountHolder, double balance) : base(accountHolder, balance) { }

    public override void CalculateInterest()
    {
        double interest = Balance * 0.05;
        Console.WriteLine($"Interest earned: {interest}");
    }
}

// Vadesiz Hesap (Derived Class)
public class CheckingAccount : BankAccount
{
    public CheckingAccount(string accountHolder, double balance) : base(accountHolder, balance) { }

    public override void CalculateInterest()
    {
        Console.WriteLine("Checking accounts do not earn interest.");
    }
}

// Angular ile API Controller (ASP.NET Core Web API)
using Microsoft.AspNetCore.Mvc;

[Route("api/[controller]")]
[ApiController]
public class EmployeeController : ControllerBase
{
    [HttpGet]
    public IActionResult GetEmployees()
    {
        var employees = new List<Employee>
        {
            new Manager(1, "Ahmet Yılmaz", 10000, "IT", 5),
            new Developer(2, "Mehmet Kaya", 8000, "Software", "Backend Developer")
        };
        return Ok(employees);
    }
}

// Angular Service (TypeScript)
/* 
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class EmployeeService {
  private apiUrl = 'http://localhost:5000/api/employee';

  constructor(private http: HttpClient) { }

  getEmployees(): Observable<Employee[]> {
    return this.http.get<Employee[]>(this.apiUrl);
  }
}
*/

// Ana Program (Main Method)
class Program
{
    static void Main()
    {
        // Çalışanlar
        Manager mgr = new Manager(1, "Ahmet Yılmaz", 10000, "IT", 5);
        Developer dev = new Developer(2, "Mehmet Kaya", 8000, "Software", "Backend Developer");

        Console.WriteLine(mgr.Name + " bonus: " + mgr.CalculateBonus());
        Console.WriteLine(dev.Name + " bonus: " + dev.CalculateBonus());

        // Banka hesapları
        SavingsAccount savings = new SavingsAccount("Ali Veli", 20000);
        CheckingAccount checking = new CheckingAccount("Ayşe Demir", 5000);

        savings.CalculateInterest();
        checking.CalculateInterest();
    }
}
