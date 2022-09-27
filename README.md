using System;
public enum Card{
    goldenCard = 0,
    standardCard = 1
};
public enum Sex{
    male = 0,
    female = 1
};
public class Date
{
    public Date(){
        this.day = 0;
        this.month = 0;
        this.year = 0;
    }
    public Date(int day, int month, int year){
        this.day = day;
        this.month = month;
        this.year = year;
    }
    ~Date() {}
    private int day;
    public int Day
    {
        get {return this.day; }
        set {this.day = value;}
    }
    private int month;
    public int Month
    {
        get {return this.month; }
        set {this.month = value;}
    }
    private int year;
    public int Year
    {
        get {return this.year; }
        set {this.year = value;}
    }
}
public class DebitCard {
    public DebitCard(){
        this.debit = 0;
        this.limitedMoney = 0;
    }
    public DebitCard(double limitedMoney){
        this.debit = 0;
        this.limitedMoney = limitedMoney;
    }
    ~DebitCard() {}
    private double debit;
    public double Debit{
        get{ return this.debit;}
        set{ this.debit = value;}
    }
    private double limitedMoney;
    public double LimitedMoney{
        get{ return this.limitedMoney;}
        set{ this.limitedMoney = value;}
    }
    public bool Limited(double expenditure){
        if (expenditure > limitedMoney)
        {
            Console.WriteLine("Your expenditure has been over the limite");
            return false;
        }
        return true;
    }
    public void Shopping(double expenditure)
    {
        this.debit -= expenditure;
    }
}
public class BankAccount
{
    public BankAccount() {}
    public BankAccount(double income){
        if (income > 30000000)
        {
        this.money = 0;
        this.accountNumber = "";
        this.dayOpenCreditCard = new Date(0,0,0);
        this.dayInvalidCreditCard = new Date(0,0,0);}
        else Console.WriteLine("Your income is not enough to create a BankAccount");
    }
    public BankAccount(double income, double money, string accountNumber, Date dayOpenCreditCard, Date dayInvalidCreditCard){
        if (income > 30000000)
        {
        this.money = money;
        this.accountNumber = accountNumber;
        this.dayOpenCreditCard = dayOpenCreditCard;
        this.dayInvalidCreditCard = dayInvalidCreditCard;
        }
        else  Console.WriteLine("Your income is not enough to create a BankAccount");
    }
    public void deposit(double money){
        this.Money += money;
    }
    private int typeOfCard;
    public int TypeOfCard{
        get {return this.typeOfCard;}
        set {this.typeOfCard = value;}
    }
    private string accountNumber;
    public string AccountNumber
    {
        get {return this.accountNumber; }
        set {this.accountNumber = value;}
    }
    private double money;
    public double Money{
        get {return this.money;}
        set {this.money = value;}
    }
    private Date dayOpenCreditCard;
    public Date DayOpenCreditCard{
        get {return this.dayOpenCreditCard;}
        set {this.dayOpenCreditCard = value;}
    }
    private Date dayInvalidCreditCard;
    public Date DayInvalidCreditCard{
        get {return this.dayInvalidCreditCard;}
        set {this.dayInvalidCreditCard = value;}
    }
    public bool Limited(double expenditure){
        if (expenditure > this.money)
        {
            Console.WriteLine("You don't have enough money to pay your expenditure");
            return false;
        }
        else return true;
    }
    public void Expenditure(double expenditure){
        if (Limited(expenditure))
            this.Money -= expenditure;
        else Console.WriteLine("You don't have enough money to pay your expenditure");
    }
    public void ReceivedMoneyFromBanking(double moneyBanking){
        this.money += moneyBanking;
    }
    public void ShoppingWithDiscount(double expenditure){
        if (Limited(expenditure))
            this.Money -= expenditure*0.1;
        else Console.WriteLine("You don't have enough money to pay your shopping");
    }
}
public class BankAccountInfo:  BankAccount
{
    public BankAccountInfo() {
        this.gender = 0;
        this.income = 0;
        this.iD = "";
        this.name = "";
    }
    public BankAccountInfo(int gender, double income,string iD, string name){
        this.gender = gender;
        this.income = income;
        this.iD = iD;
        this.name = name;
    }
    ~BankAccountInfo() {
    }
    private DebitCard dC;
    public DebitCard DC{
        get {return dC;}
        set {dC = value;}
        
    }
    private string name;
    public string Name{
        get {return this.name;}
        set{this.name = value;}
    }
     public void Banking(double expenditure, BankAccount other){
        if (this.Limited(expenditure)){
            this.DC.Debit -= expenditure;
            other.ReceivedMoneyFromBanking(expenditure);
        }
        else Console.WriteLine("Your expenditure on banking has been over the limit");
    }
    private string iD;
    public string ID
    {
        get {return this.iD; }
        set {this.iD = value;}
    }
    private double income;
    public double Income{
        get {return this.income;}
        set{this.income = value;}
    }
    private int gender;
    public int Gender{
        get{return this.gender;}
        set{this.gender = value;}
    }
    public void displayInfo(){
        Console.WriteLine("Name: " + this.Name);
        Console.WriteLine("ID: " + this.ID);
        Console.WriteLine("Income: " + this.Income);
        if (this.Gender == 0)
        Console.WriteLine("Gender: Male");
        else Console.WriteLine("Gender: Female");
        Console.WriteLine("Debit Card");
        Console.WriteLine("Debit: " + this.DC.Debit);
        Console.WriteLine("Limited Debit: " + this.DC.LimitedMoney);
        Console.WriteLine("Day Open Credit Card: " + this.DayOpenCreditCard.Day + "/" + this.DayOpenCreditCard.Month + "/" + this.DayOpenCreditCard.Year);
        Console.WriteLine("Day Open Credit Card: " + this.DayInvalidCreditCard.Day + "/" + this.DayInvalidCreditCard.Month + "/" + this.DayInvalidCreditCard.Year);
        Console.WriteLine("Money: " + this.Money);
        Console.WriteLine("Account Number: " + this.AccountNumber);
    }
    public static void Main(string[] args)
    {
        // Test Constructor
        // 1. Create Infomation for a person by Constructor BankAccountInfo(parameters)
        BankAccountInfo Person1 = new BankAccountInfo((int)Sex.male,20000000, "928384", "Person1");
        Date OpenPerson1 = new Date(2,12,2021);
        Date InvalidPerson1 = new Date(2,12,2029);
        Person1.DayOpenCreditCard = OpenPerson1;
        Person1.DayInvalidCreditCard = InvalidPerson1;
        Person1.DC = new DebitCard(50000000);
        Person1.Money = 1000000000;
        Person1.AccountNumber = "123456789";
        Person1.displayInfo();
        Console.WriteLine("\n");
        // 2. Create a BankAccount for a person by passing income as a double variable to Constructor
        Date OpenPerson2 = new Date(2,12,2022);
        Date InvalidPerson2 = new Date(2,12,2030);
        BankAccount Person2 = new BankAccount(500000000, 2000000000, "13563566132", OpenPerson2, InvalidPerson2 );
        Console.WriteLine("Person2's ");
        Console.WriteLine("Person2's Money: " + Person2.Money);
        Console.WriteLine("Person2's Account Number" + Person2.AccountNumber);
        Console.WriteLine("Person2's Day Open Credit Card: " + Person2.DayOpenCreditCard.Day + "/" + Person2.DayOpenCreditCard.Month + "/" + Person2.DayOpenCreditCard.Year);
        Console.WriteLine("Person2's Day Open Credit Card: " + Person2.DayInvalidCreditCard.Day + "/" + Person2.DayInvalidCreditCard.Month + "/" + Person2.DayInvalidCreditCard.Year);
        Console.WriteLine("\n");
        // 3. Test Method(): Shopping, Banking, Expenditure, ...
        // Test Banking():
        Console.WriteLine("Person1's Money:" + Person1.Money + "\n" + "Person1's Debit: " + Person1.DC.Debit);
        Console.WriteLine("Person2's Money:" + Person2.Money);
        Person1.Banking(10000000, Person2);
        Console.WriteLine("After Banking from Person1 to Person2:");
        Console.WriteLine("Person1's Debit: " + Person1.DC.Debit);
        Console.WriteLine("Person2's Money: " + Person2.Money);
        // Test Deposit():
        Console.WriteLine("After Person1 Deposit 300000");
        Person1.deposit(300000);
        Console.WriteLine("Person1's Money: " + Person1.Money);
        // Test Expenditure and Shopping with LimitedMoney
        Console.WriteLine("Person1 wants to spend 999999999999999 on something (Out of Range)");
        Person1.Expenditure(999999999999999);
        Console.WriteLine("Person1 spends 20000 something");
        Person1.Expenditure(20000);
        Console.WriteLine("Person1's Debit: " + Person1.Money );
        // Test Shopping with Discount
        Console.WriteLine("Person1 spend 50000 on Shopping");
        Person1.ShoppingWithDiscount(500000);
        Console.WriteLine("Person1's Money: " + Person1.Money);
    }
}
