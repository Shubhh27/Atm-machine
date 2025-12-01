# Atm-machine
It is an working atm machine
import datetime 
now = datetime.datetime.now()
t = now.strftime("%d/%m/%Y - %I:%M %p")
class ATM():
    def __init__(self,account_number,name,balance):
        self.account_number=account_number
        self.name=name
        self.balance=balance

    def check_history(self):
        print("Account number:",self.account_number)
        print("Account holder:",self.name)
        print(f"balance: ₹{record_balance[self.account_number]}")
        print()
        print("Your deposit history:-")
        with open(f"deposit{self.account_number}.txt",encoding="utf-8") as f:
            x=f.read()
            print(x)
        print()
        print("Your withdraw history:-")
        with open(f"withdraw{self.account_number}.txt",encoding="utf-8") as f:
            x=f.read()
            print(x)

class account():
    def __init__(self,account_number,name,balance):
        self.account_number=account_number
        self.name=name
        self.balance=balance


    def deposit(self,amount_deposit):
        self.balance+=amount_deposit
        record_balance[self.account_number]=self.balance
        return self.balance
        

    def withdraw(self,amount_withdraw):
        self.balance-=amount_withdraw
        record_balance[self.account_number]=self.balance
        return self.balance


    def check_balance(self):
        self.balance=record_balance[self.account_number]
        return self.balance

record_name={
    1:"Priyanshu",
    2:"Shruti",
    3:"shreya",
    4:"Anurag",
    5:"Suraj"
}   
record_password={
    1:"0930",
    2:"1619",
    3:"0000",
    4:"1111",
    5:"1212"
}
record_balance={
    1:10000,
    2:7500,
    3:4000,
    4:2000,
    5:3500
}
security_question={
    1:["2007","ranchi"],
    2:["2008","ranchi"],
    3:["2003","daltonganj"],
    4:["2006","mars"],
    5:["2007","moon"]
}
ans=[]
sign_in=input("Want to sign in?(yes/no): ").lower()
while sign_in=="yes":
    account_number=int(input("Enter your account number: "))
    password=input("Enter your passcode:- ")
    if password==record_password[account_number] and len(password)==4:
        name=record_name[account_number].capitalize()
        balance=record_balance[account_number]
        c1=account(account_number,name,balance)
        c2=ATM(account_number,name,balance)
        print("Account_holder:",name)
        print("Account number:",account_number)
        print(f"Balance:₹{balance}")
        print()
        deposit=input("Want to deposit some money?(yes/no): ").lower()
        if deposit=="yes":
                amount_deposit=int(input("Enter your amount you want to deposit: ₹"))
                with open(f"deposit{account_number}.txt","a",encoding="utf-8") as f:
                    f.write(f"\n{t} : ₹{amount_deposit}")
                c1.deposit(amount_deposit)
                print(f"Your updated balance is ₹{record_balance[account_number]}")
        print()
        withdraw=input("Want to withdraw some money?(yes/no): ").lower()
        if withdraw=="yes":
            amount_withdraw=int(input("Enter your amount you want to withdraw: ₹"))
            if amount_withdraw<=record_balance[account_number]:
                with open(f"withdraw{account_number}.txt","a",encoding="utf-8") as f:
                    f.write(f"\n{t} : ₹{amount_withdraw}")
                c1.withdraw(amount_withdraw)
                print(f"Your updated balance is: ₹{record_balance[account_number]}")
            else:
                print("Insuffient balance!!")
        print()
        check_balance=input("Want to check your balance(yes/no): ").lower()
        if check_balance=="yes":
            print(f"Your balance is : ₹{c1.check_balance()}")
        print()
        check_history=input("Want to check your account history(yes/no): ").lower()
        if check_history=="yes":
            c2.check_history()
        print()
        sign_in=input("Want to sign in?(yes/no): ").lower()
    else:
        print("Your Passcode is incorect")
        reset_password=input("Want to reset your passcode?(yes/no):- ").lower()
        if reset_password=="yes":
            ans1=input("In which year you were born?: ").lower()
            ans2=input("where you were born?: ").lower()
            ans.append(ans1)
            ans.append(ans2)
            if ans==security_question[account_number]:
                reset_password=input("Enter your new passcode: ")
                record_password.update({account_number:reset_password})
                print("Your passcode has reset.")
print("ThankYou!!")
