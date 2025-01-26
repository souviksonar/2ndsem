## Question 1
![[Unit 1 Notes - Relational Database.pdf#page=2&rect=99,45,533,235&color=red|Unit 1 Notes - Relational Database, p.2]]
#### Solution
> [!PDF|8, 109, 221] [[Unit 1 Notes - Relational Database.pdf#page=3&annotation=1680R|Unit 1 Notes - Relational Database, p.3]]
> > **Cascade**  –  automatically delete “dependent” side rows that correspond with the “parent” side row to be deleted, i.e. delete the associated orders, in which case we lose not only the customer but also the sales history 
> > **Set-to-Null**  –  set the foreign key in the dependent side to null if deleting from the parent side -  an exception that says although an order must have a customer_ID value when the order is created, Customer_ID can become null later if the associated customer is deleted [not allowed for weak entities]




## Mathematical Definition of Functional value Dependency
![[CSC502-ADBMS/media/media/Unit 1 Notes - Relational Database.webp]]
[[Unit 1 Notes - Relational Database.pdf#page=11&rect=79,98,668,462|Unit 1 Notes - Relational Database, p.11]]
