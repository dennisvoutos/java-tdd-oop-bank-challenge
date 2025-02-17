# Bank challenge

## From the user stories below, the domain model will change. The user stories are:


```
1.
As a customer,
So I can safely store use my money,
I want to create a current account.

2.
As a customer,
So I can save for a rainy day,
I want to create a savings account.

3.
As a customer,
So I can keep a record of my finances,
I want to generate bank statements with transaction dates, amounts, and balance at the time of transaction.

4.
As a customer,
So I can use my account,
I want to deposit and withdraw funds.
```
## User story 1

| Class name | Attributes                       | Methods      | Scenarios                           | Outcome                                                                                                          |      
|------------|----------------------------------|--------------|-------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Balance    | int intPart                      |              |                                     |                                                                                                                  |
|            | int decimalPart                  |              |                                     |                                                                                                                  |
|            |                                  |              |                                     |                                                                                                                  |
| Account    | Balance balance                  |              |                                     |                                                                                                                  |
|            |                                  |              |                                     |                                                                                                                  |
| Customer   | Account account                  | setUpAccount | The user wants to create an account | The account attribute is initialized with the users initial deposit. The initial deposit should be more than $5. |
|            | String fullName                  |              |                                     |                                                                                                                  |
|            | String address                   |              |                                     |                                                                                                                  |
|            | String dateOfBirth               |              |                                     |                                                                                                                  |
|            | int taxpayerIdentificationNumber |              |                                     |                                                                                                                  |

### On all classes the getters/setters are implied, except for:
#### The setters for the intPart and decimalPart of the Balance class, and the setters for balance in the Account class
For this user story, the UML diagram is:
![d1.png](d1.png)

## User story 2
### For this user story, we need to create a new class which will be a subclass of Account that is a SavingsAccount. With that in mind, our previous understanding of the account is now changed. Now we should introduce a new Account subclass which will be the CurrentAccount, representing our previous idea of an Account. A user can create both a savings account and a current one. 
#### Now the model looks like this:

| Class name     | Attributes                       | Methods             | Scenarios                                                              | Outcome                                             |      
|----------------|----------------------------------|---------------------|------------------------------------------------------------------------|-----------------------------------------------------|
| Balance        | int intPart                      |                     |                                                                        |                                                     |
|                | int decimalPart                  |                     |                                                                        |                                                     |
|                |                                  |                     |                                                                        |                                                     |
| Account        | Balance balance                  |                     |                                                                        |                                                     |
|                |                                  |                     |                                                                        |                                                     |
| CurrentAccount |                                  |                     |                                                                        |                                                     |
|                |                                  |                     |                                                                        |                                                     |
| SavingsAccount |                                  |                     |                                                                        |                                                     |
|                |                                  |                     |                                                                        |                                                     |
| Customer       | Arraylist<Account> accounts      | setUpCurrentAccount | The user wants to create a current account                             | A new current account is created for the user.      |
|                |                                  | setUpSavingsAccount | The user wants to create a savings account                             | A new savings account is created for the user.      |
|                |                                  | removeNullAccounts  | The user creates an account where the balance is null because of input | The accounts with null in their balance are removed |   
|                | String fullName                  |                     |                                                                        |                                                     |
|                | String address                   |                     |                                                                        |                                                     |
|                | String dateOfBirth               |                     |                                                                        |                                                     |
|                | int taxpayerIdentificationNumber |                     |                                                                        |                                                     |

##### Note: We could have 2 attributes that are both Account objects, one could be named currentAccount and the other savingsAccount, but implementing inheritance will help down the line when the 2 accounts will inevitably want to use behave differently. 
For this user story, the UML diagram is:
![d2.png](d2.png)


## User story 3 and 4
### For the last 2 user stories of the Core requirements ,a customer will want to print statements for each account in his possession. Consequently, that means that a customer should be able to withdraw and deposit money on each of his accounts. Meaning that these methods will accompany the Account class, and if in the future it is needed, they may override the method of their parent.
#### Now the model looks like this:

| Class name     | Attributes                       | Methods                          | Scenarios                                                                                               | Outcome                                             |      
|----------------|----------------------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| Balance        | int intPart                      | void interact(Balance)           | You want to remove or add to a Balance object                                                           |                                                     |
|                | int decimalPart                  |                                  |                                                                                                         |                                                     |
|                |                                  |                                  |                                                                                                         |                                                     |
| Account        | Balance balance                  | boolean deposit(Balance)         | The user wants to deposit a valid amount of money(i.e Balance)                                          | Returns true                                        |
|                | String statements                |                                  | The user wants to deposit an invalid amount of money                                                    | Returns false                                       |
|                |                                  | boolean withdraw(Balance)        | The user wants to withdraw a valid amount of money(valid Balance and has enough money for the withdraw) | Returns true                                        |
|                |                                  |                                  | The user wants to withdraw an invalid amount of money(invalid Balance or does not have enough money     | Returns false                                       |
|                |                                  | String showStatements()          | The user wants to see their statements for a specified account                                          | Returns the String of statements                    |
|                |                                  | void addToStatements()           | Add a transaction info to the statements String.                                                        |                                                     |
|                |                                  | void convertEpochTimeToDateTime  | Make the currentTimeInMillis to a normal Date and Time.                                                 |                                                     |
| CurrentAccount |                                  |                                  |                                                                                                         |                                                     |
|                |                                  |                                  |                                                                                                         |                                                     |
| SavingsAccount |                                  |                                  |                                                                                                         |                                                     |
|                |                                  |                                  |                                                                                                         |                                                     |
| Customer       | Arraylist<Account> accounts      | void setUpCurrentAccount()       | The user wants to create a current account                                                              | A new current account is created for the user.      |
|                |                                  | void setUpSavingsAccount()       | The user wants to create a savings account                                                              | A new savings account is created for the user.      |
|                |                                  | void removeNullAccounts()        | The user creates an account where the balance is null because of input                                  | The accounts with null in their balance are removed |   
|                | String fullName                  |                                  |                                                                                                         |                                                     |
|                | String address                   |                                  |                                                                                                         |                                                     |
|                | String dateOfBirth               |                                  |                                                                                                         |                                                     |
|                | int taxpayerIdentificationNumber |                                  |                                                                                                         |                                                     |
For this user story, the UML diagram is:
![d3+4.png](d3%2B4.png)

# Extensions

```
5.
As an engineer,
So I don't need to keep track of state,
I want account balances to be calculated based on transaction history instead of stored in memory.

6.
As a bank manager,
So I can expand,
I want accounts to be associated with specific branches.

7.
As a customer,
So I have an emergency fund,
I want to be able to request an overdraft on my account.

8.
As a bank manager,
So I can safeguard our funds,
I want to approve or reject overdraft requests.

9.
As a customer,
So I can stay up to date,
I want statements to be sent as messages to my phone.
```

## User story 5.
### For this user story, we want the balance of an account to be calculated by the statements and not by any other means. What this means is that now the balance attribute of an account will not be changed directly when withdrawing or depositing, and when asked for it it will be given through the statements.

| Class name     | Attributes                       | Methods                          | Scenarios                                                                                               | Outcome                                                                  |      
|----------------|----------------------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Balance        | int intPart                      | void interact(Balance)           | You want to remove or add to a Balance object                                                           |                                                                          |
|                | int decimalPart                  |                                  |                                                                                                         |                                                                          |
|                |                                  |                                  |                                                                                                         |                                                                          |
| Account        | Balance balance                  | boolean deposit(Balance)         | The user wants to deposit a valid amount of money(i.e Balance)                                          | Returns true                                                             |
|                | String statements                |                                  | The user wants to deposit an invalid amount of money                                                    | Returns false                                                            |
|                |                                  | boolean withdraw(Balance)        | The user wants to withdraw a valid amount of money(valid Balance and has enough money for the withdraw) | Returns true                                                             |
|                |                                  |                                  | The user wants to withdraw an invalid amount of money(invalid Balance or does not have enough money     | Returns false                                                            |
|                |                                  | String showStatements()          | The user wants to see their statements for a specified account                                          | Returns the String of statements                                         |
|                |                                  | void addToStatements()           | Add a transaction info to the statements String.                                                        |                                                                          |
|                |                                  | void convertEpochTimeToDateTime  | Make the currentTimeInMillis to a normal Date and Time.                                                 |                                                                          |
|                |                                  | Balance getBalance()             | The logic now is different for the getter of Balance.                                                   | Returns the balance of the account calculated by the transaction history |
|                |                                  | Balance getBalanceByStatements() |                                                                                                         |                                                                          |
| CurrentAccount |                                  |                                  |                                                                                                         |                                                                          |
|                |                                  |                                  |                                                                                                         |                                                                          |
| SavingsAccount |                                  |                                  |                                                                                                         |                                                                          |
|                |                                  |                                  |                                                                                                         |                                                                          |
| Customer       | Arraylist<Account> accounts      | void setUpCurrentAccount()       | The user wants to create a current account                                                              | A new current account is created for the user.                           |
|                |                                  | void setUpSavingsAccount()       | The user wants to create a savings account                                                              | A new savings account is created for the user.                           |
|                |                                  | void removeNullAccounts()        | The user creates an account where the balance is null because of input                                  | The accounts with null in their balance are removed                      |   
|                | String fullName                  |                                  |                                                                                                         |                                                                          |
|                | String address                   |                                  |                                                                                                         |                                                                          |
|                | String dateOfBirth               |                                  |                                                                                                         |                                                                          |
|                | int taxpayerIdentificationNumber |                                  |                                                                                                         |                                                                          |
#### The UML diagram will be the same as before, this time the only difference is the getBalance method of Account:
![d5.png](d5.png)

## User story 6.
### For this user story, I believe that the idea of a Branch class is needed.A simple way to associate an account with a specific branch is to have an attribute called "branch", whose value will be the Branch that the Account was created at.


| Class name     | Attributes                          | Methods                                   | Scenarios                                                                                               | Outcome                                                                  |      
|----------------|-------------------------------------|-------------------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Balance        | int intPart                         | void interact(Balance)                    | You want to remove or add to a Balance object                                                           |                                                                          |
|                | int decimalPart                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Account        | Balance balance                     | boolean deposit(Balance)                  | The user wants to deposit a valid amount of money(i.e Balance)                                          | Returns true                                                             |
|                | String statements                   |                                           | The user wants to deposit an invalid amount of money                                                    | Returns false                                                            |
|                |                                     | boolean withdraw(Balance)                 | The user wants to withdraw a valid amount of money(valid Balance and has enough money for the withdraw) | Returns true                                                             |
|                |                                     |                                           | The user wants to withdraw an invalid amount of money(invalid Balance or does not have enough money     | Returns false                                                            |
|                |                                     | String showStatements()                   | The user wants to see their statements for a specified account                                          | Returns the String of statements                                         |
|                |                                     | void addToStatements()                    | Add a transaction info to the statements String.                                                        |                                                                          |
|                |                                     | void convertEpochTimeToDateTime           | Make the currentTimeInMillis to a normal Date and Time.                                                 |                                                                          |
|                |                                     | Balance getBalance()                      | The logic now is different for the getter of Balance.                                                   | Returns the balance of the account calculated by the transaction history |
|                |                                     | Balance getBalanceByStatements()          |                                                                                                         |                                                                          |
| CurrentAccount |                                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| SavingsAccount |                                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Customer       | Arraylist<Account> accounts         | void setUpCurrentAccount(Branch, Balance) | The user wants to create a current account in a specified branch                                        | A new current account is created for the user.                           |
|                |                                     | void setUpSavingsAccount(Branch, Balance) | The user wants to create a savings account  in a specified branch                                       | A new savings account is created for the user.                           |
|                |                                     | void removeNullAccounts()                 | The user creates an account where the balance is null because of input                                  | The accounts with null in their balance are removed                      |   
|                | String fullName                     |                                           |                                                                                                         |                                                                          |
|                | String address                      |                                           |                                                                                                         |                                                                          |
|                | String dateOfBirth                  |                                           |                                                                                                         |                                                                          |
|                | int taxpayerIdentificationNumber    |                                           |                                                                                                         |                                                                          |
| Branch         | String address                      |                                           |                                                                                                         |                                                                          |
|                | int identificationCode              |                                           |                                                                                                         |                                                                          |
|                | int numberOfEmployees               |                                           |                                                                                                         |                                                                          |
| BranchList     | Arraylist<Branch> availableBranches |                                           | Contains all available branches of the bank                                                             |                                                                          |
#### In the branch class i decided to add a few attributes that could represent a potential branch of a Bank.
#### Also, when setting up an account, a Branch is needed now, and that Branch is the Branch where the account is created. Also, that same account that is added in the user object is also added in the Branch's arraylist.
#### The UML diagram will be the same as before, this time the only difference is the getBalance method of Account:
![d6.png](d6.png)

## User story 9
### Moving on from the next 2 User stories, I'll first implement this one. Instead of using twilio, I will write the statement in a file in the computer called statement.txt, simulating the SMS.

| Class name     | Attributes                          | Methods                                   | Scenarios                                                                                               | Outcome                                                                  |      
|----------------|-------------------------------------|-------------------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Balance        | int intPart                         | void interact(Balance)                    | You want to remove or add to a Balance object                                                           |                                                                          |
|                | int decimalPart                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Account        | Balance balance                     | boolean deposit(Balance)                  | The user wants to deposit a valid amount of money(i.e Balance)                                          | Returns true                                                             |
|                | String statements                   |                                           | The user wants to deposit an invalid amount of money                                                    | Returns false                                                            |
|                |                                     | boolean withdraw(Balance)                 | The user wants to withdraw a valid amount of money(valid Balance and has enough money for the withdraw) | Returns true                                                             |
|                |                                     |                                           | The user wants to withdraw an invalid amount of money(invalid Balance or does not have enough money     | Returns false                                                            |
|                |                                     | String showStatements()                   | The user wants to see their statements for a specified account                                          | Returns the String of statements                                         |
|                |                                     | void addToStatements()                    | Add a transaction info to the statements String.                                                        |                                                                          |
|                |                                     | void convertEpochTimeToDateTime           | Make the currentTimeInMillis to a normal Date and Time.                                                 |                                                                          |
|                |                                     | Balance getBalance()                      | The logic now is different for the getter of Balance.                                                   | Returns the balance of the account calculated by the transaction history |
|                |                                     | void writeStatements(String)              | Write the statements in a file (instead of a text)                                                      |                                                                          |
| CurrentAccount |                                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| SavingsAccount |                                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Customer       | Arraylist<Account> accounts         | void setUpCurrentAccount(Branch, Balance) | The user wants to create a current account                                                              | A new current account is created for the user.                           |
|                |                                     | void setUpSavingsAccount(Branch, Balance) | The user wants to create a savings account                                                              | A new savings account is created for the user.                           |
|                |                                     | void removeNullAccounts()                 | The user creates an account where the balance is null because of input                                  | The accounts with null in their balance are removed                      |   
|                | String fullName                     |                                           |                                                                                                         |                                                                          |
|                | String address                      |                                           |                                                                                                         |                                                                          |
|                | String dateOfBirth                  |                                           |                                                                                                         |                                                                          |
|                | int taxpayerIdentificationNumber    |                                           |                                                                                                         |                                                                          |
| Branch         | String address                      |                                           |                                                                                                         |                                                                          |
|                | int identificationCode              |                                           |                                                                                                         |                                                                          |
|                | int numberOfEmployees               |                                           |                                                                                                         |                                                                          |
| BranchList     | Arraylist<Branch> availableBranches |                                           | Contains all available branches of the bank                                                             |                                                                          |

#### The UML diagram will be the same as before, this time the only difference is the getBalance method of Account:
![d9.png](d9.png)

## User story 7 & 8
### Finally, we have the final 2 User stories. The customer can request an overdraft on his current account and a manager is needed for that
| Class name     | Attributes                          | Methods                                   | Scenarios                                                                                               | Outcome                                                                  |      
|----------------|-------------------------------------|-------------------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Balance        | int intPart                         | void interact(Balance)                    | You want to remove or add to a Balance object                                                           |                                                                          |
|                | int decimalPart                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Account        | Balance balance                     | boolean deposit(Balance)                  | The user wants to deposit a valid amount of money(i.e Balance)                                          | Returns true                                                             |
|                | String statements                   |                                           | The user wants to deposit an invalid amount of money                                                    | Returns false                                                            |
|                | boolean canOverdraft                | boolean withdraw(Balance)                 | The user wants to withdraw a valid amount of money(valid Balance and has enough money for the withdraw) | Returns true                                                             |
|                |                                     |                                           | The user wants to withdraw an invalid amount of money(invalid Balance or does not have enough money     | Returns false                                                            |
|                |                                     | String showStatements()                   | The user wants to see their statements for a specified account                                          | Returns the String of statements                                         |
|                |                                     | void addToStatements()                    | Add a transaction info to the statements String.                                                        |                                                                          |
|                |                                     | void convertEpochTimeToDateTime           | Make the currentTimeInMillis to a normal Date and Time.                                                 |                                                                          |
|                |                                     | Balance getBalance()                      | The logic now is different for the getter of Balance.                                                   | Returns the balance of the account calculated by the transaction history |
|                |                                     | void writeStatements(String)              | Write the statements in a file (instead of a text)                                                      |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| CurrentAccount |                                     | void requestOverdraft(Manager)            | Change weather an account can get an overdraft request.                                                 |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| SavingsAccount |                                     |                                           |                                                                                                         |                                                                          |
|                |                                     |                                           |                                                                                                         |                                                                          |
| Customer       | Arraylist<Account> accounts         | void setUpCurrentAccount(Branch, Balance) | The user wants to create a current account                                                              | A new current account is created for the user.                           |
|                |                                     | void setUpSavingsAccount(Branch, Balance) | The user wants to create a savings account                                                              | A new savings account is created for the user.                           |
|                |                                     | void removeNullAccounts()                 | The user creates an account where the balance is null because of input                                  | The accounts with null in their balance are removed                      |   
|                | String fullName                     |                                           |                                                                                                         |                                                                          |
|                | String address                      |                                           |                                                                                                         |                                                                          |
|                | String dateOfBirth                  |                                           |                                                                                                         |                                                                          |
|                | int taxpayerIdentificationNumber    |                                           |                                                                                                         |                                                                          |
| Branch         | String address                      |                                           |                                                                                                         |                                                                          |
|                | int identificationCode              |                                           |                                                                                                         |                                                                          |
|                | int numberOfEmployees               |                                           |                                                                                                         |                                                                          |
| BranchList     | Arraylist<Branch> availableBranches |                                           | Contains all available branches of the bank                                                             |                                                                          |
| Manager        | boolean canOverdraft                |                                           |                                                                                                         |                                                                          |

#### The UML diagram will be:
![d7+8.png](d7%2B8.png)