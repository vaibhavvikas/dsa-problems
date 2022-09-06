## Max Experience in an Organization

Given a list of employees experience, and the list of their managers. You're supposed to invite employees to a party such that if one employee is invited, you can't invite their direct manager and delegate.

Find the max experience that you can get by inviting employees to such a party.

```bash
Example:

Input:
employees_exp = [5, 8, 7, 5, 4, 6, 5, 9]
employee_name = ["Alex", "Bob", "Charlie", "John", "Doe", "Riri", "Harley", "Sia"]
employee_manager = [None, "Alex", "Alex", "Alex", "Bob", "Sia", "Sia", "Bob"]

Output: 31
```

```
Demonstration:
           5
     /     |     \
    8      7      5
  /  \
 4    6
     /  \
    6     5

Employees: 8, 7, 5, 6, 5
```
### Approach
We start from the main manager or say CEO,
Now with each employee we have two options
Take or Not-Take

If an employee is take
that means we can take it or not take.

Based on that, we can use the Dynamic Programming with each child

```bash
TC: O(h*h*2)
SC: O(h*k*2)

let "h" be the height and
"k" be the max child no. of tree
```

### Solution
```python
from collections import defaultdict
from typing import List


class Employee:
    def __init__(self, name, exp):
        self.name = name
        self.exp = exp

    def __str__(self):
        return f"{self.name}: {self.exp}"


class Organization:
    def __init__(self):
        self.employees = dict()
        self.heirarchy = defaultdict(list)

    def add_ceo(self, ceo: Employee):
        self.employees[ceo.name] = ceo
        self.ceo = ceo

    def add_delegates(self, manager, employee: Employee):
        self.employees[employee.name] = employee
        self.heirarchy[manager].append(employee.name)

    def get_ceo(self):
        return self.ceo

    def get_employee(self, employee_name):
        return self.employees[employee_name]

    def get_delegates(self, employee) -> List[Employee]:
        res = []
        for each in self.heirarchy[employee]:
            res.append(self.employees[each])
        return res

    def __str__(self):
        employee = "Employees:\n"
        employee_info = "Employee Info:\n"
        for each in self.heirarchy:
            employee += each + ": " + " ".join(self.heirarchy[each]) + "\n"

        for each in self.employees:
            employee_info += str(self.employees[each]) + "\n"

        return employee + "\n" + employee_info


def find_max_exp(organization: Organization):

    ceo = organization.get_ceo()
    dp = {}

    def max_total_exp(employee: Employee, can_invite: bool):
        if (employee, can_invite) in dp:
            return dp[(employee, can_invite)]

        delegates = organization.get_delegates(employee.name)

        include = 0
        if can_invite:
            include += employee.exp
            for each in delegates:
                include += max_total_exp(each, False)

        not_include = 0
        for each in delegates:
            not_include += max_total_exp(each, True)

        dp[(employee, can_invite)] = max(include, not_include)

        return dp[(employee, can_invite)]

    return max_total_exp(ceo, True)


def main():
    xyz = Organization()

    bob = Employee("Alex", 5)
    xyz.add_ceo(bob)

    employees_exp = [8, 7, 5, 4, 6, 5, 9]
    employee_name = ["Bob", "Charlie", "John", "Doe", "Riri", "Harley", "Sia"]
    employee_manager = ["Alex", "Alex", "Alex", "Bob", "Sia", "Sia", "Bob"]

    for i in range(len(employees_exp)):
        employee = Employee(employee_name[i], employees_exp[i])
        xyz.add_delegates(employee_manager[i], employee)

    print(xyz)
    print(find_max_exp(xyz))


if __name__ == "__main__":
    main()
```