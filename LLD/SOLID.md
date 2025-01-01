
Single Responsibility Principle (SRP):
○ A class should have only one reason to change, meaning it should have a single responsibility
or job.
○ It is only a guideline for designing.
○ Single Responsibility can be subjective and dependent on the specific context of application.
○ Example - Order Validation can be either a single class’s responsibility or there can be multiple
classes to validate user inputs, generating error messages and checking permissions.

● Open-Closed Principle (OCP):
○ Software entities (classes, modules, functions) should be open for extension but closed for
modification, allowing new functionality to be added without altering existing code.
○ Once code is written and tested, it shouldn’t have to be modified to add new features.
○ Code should be extensible.
○ Example - Logger has Info and Error Levels, we should be able to add Debug Level seamlessly.

● Liskov Substitution Principle (LSP):
○ Subtypes (derived classes) should be substitutable for their base types (parent classes) without
affecting the correctness of the program.
○ Example - We should be able to replace employee with manager or intern seamlessly.

● Interface Segregation Principle (ISP):
○ Clients should not be forced to depend on interfaces they don't use.
○ We should aim for smaller, more specific interfaces.
○ Example - In Swiggy, a customer shouldn't be forced to implement KYC like Delivery Partner
and Restaurant Owner.

● Dependency Inversion Principle (DIP):
○ High-level modules should not depend on low-level modules.
○ Both should depend on abstractions.
○ Abstractions should not depend on details; details should depend on abstractions.
○ High-level order processing modules should depend on an abstract "PaymentGateway"
interface, not on specific payment service implementations like PayPal or CreditCardProcessor