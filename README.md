# Bank-on-it

##Pseudocode

INTERFACE HasMenu
    METHOD menu() RETURNS string
    METHOD start()

CLASS CheckingAccount IMPLEMENTS HasMenu
    VARIABLE balance AS double

    METHOD CheckingAccount()
        SET balance TO 0.0

    METHOD CheckingAccount(balance)
        SET this.balance TO balance

    METHOD getBalance() RETURNS double
        RETURN balance

    METHOD getBalanceString() RETURNS string
        RETURN formatted balance as "$x.xx"

    METHOD setBalance(newBalance)
        SET balance TO newBalance

    METHOD checkBalance()
        PRINT current balance

    METHOD getDouble() RETURNS double
        TRY to read user input as double
        IF invalid THEN RETURN 0

    METHOD makeDeposit()
        ASK user for deposit amount
        CALL getDouble()
        ADD amount to balance
        PRINT new balance

    METHOD makeWithdrawal()
        ASK user for withdrawal amount
        CALL getDouble()
        SUBTRACT amount from balance
        PRINT new balance

    METHOD menu() RETURNS string
        RETURN options: check balance, deposit, withdraw, quit

    METHOD start()
        LOOP until user selects quit
            DISPLAY menu
            GET user choice
            CALL corresponding method

CLASS SavingsAccount EXTENDS CheckingAccount
    VARIABLE interestRate AS double

    METHOD SavingsAccount()
        CALL super()
        SET interestRate TO 0.0

    METHOD SavingsAccount(balance, rate)
        CALL super(balance)
        SET interestRate TO rate

    METHOD setInterestRate(rate)
        SET interestRate TO rate

    METHOD getInterestRate() RETURNS double
        RETURN interestRate

    METHOD calcInterest()
        CALCULATE interest = balance * interestRate
        ADD interest to balance

ABSTRACT CLASS User IMPLEMENTS HasMenu
    VARIABLE userName AS string
    VARIABLE PIN AS string

    METHOD login() RETURNS boolean
        PROMPT user for name and PIN
        RETURN login(name, PIN)

    METHOD login(name, PIN) RETURNS boolean
        RETURN true if name and PIN match object's data

    METHOD setUserName(name)
        SET userName TO name

    METHOD getUserName() RETURNS string
        RETURN userName

    METHOD setPIN(PIN)
        SET this.PIN TO PIN

    METHOD getPIN() RETURNS string
        RETURN PIN

    ABSTRACT METHOD getReport() RETURNS string

CLASS Customer EXTENDS User
    VARIABLE checking AS CheckingAccount
    VARIABLE savings AS SavingsAccount

    METHOD Customer()
        SET userName TO "Alice"
        SET PIN TO "0000"
        INITIALIZE checking and savings accounts

    METHOD Customer(name, PIN)
        SET userName and PIN
        INITIALIZE checking and savings accounts

    METHOD getReport() RETURNS string
        RETURN formatted string with account balances

    METHOD changePin()
        ASK user for new PIN
        SET PIN

    METHOD menu() RETURNS string
        RETURN options: manage checking, savings, change PIN, quit

    METHOD start()
        LOOP until user selects exit
            DISPLAY menu
            GET user choice
            IF checking THEN call checking.start()
            IF savings THEN call savings.start()
            IF change PIN THEN call changePin()

FUNCTION main()
    CREATE a new Customer object
    IF login is successful
        CALL customer.start()
    ELSE
        PRINT login failed
