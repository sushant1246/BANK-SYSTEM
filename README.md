# BANK-SYSTEM
I CREATE A SIMPLE BANK SYSTEM WHER YOU CAN CREATE ACCOUNT,DEPOSIT MONEY,WITHDRTAW MONEY,CHECK BALANCE,CHECK TRANSACTION HISTORYAND ADMIN CONTROL PANNEL WHERE YOU COULD VIEW ACCOUNTS AND DELETE ACCOUNTS.

                                                    -------------------------------------- BANK SYSTEM --------------------------------------
                                                             

import random
import os
import time
import shutil

time1 = time.strftime("%H:%M:%S")

if not os.path.exists("ACCOUNTS"):
 os.mkdir("ACCOUNTS")

if not os.path.exists("ACCOUNTS/admin"):
 os.makedirs("ACCOUNTS/admin")
else:
 with open("ACCOUNTS/admin/details.txt","w") as f:
     f.write("admin23 admin1234")


class Bank:

    def deposit(self):
        name = input("ENTER YOUR NAME :")
        acc_no = input("ENTER THE ACC NO :")
        filename = name+acc_no
        path = f"ACCOUNTS/{filename}/details.txt"
        if os.path.exists(path):
         with open(path,"r+") as f:
          a = f.readlines()
          length = len(a)-1
          data = a[length].split()
          file_acc_no = data[0]
          file_name = data[1]
          file_pin = data[2]
          file_balance = float(data[3])


          if acc_no == file_acc_no:
              pin = input("ENTER YOUR PIN :")
              if pin == file_pin:
                  amount= float(input("ENTER THE AMOUNT :"))
                  file_balance+=amount
                  f.write(f"\n{file_acc_no}\t\t{file_name}\t\t{file_pin}\t\t{file_balance}\t\t{time1}")
                  print("DEPOSITED SUCCESSFULLY")
                  with open(f"ACCOUNTS/{filename}/transactions.txt", "a") as f:
                      f.write(f"\n{file_acc_no}:\t{amount}\thas\tbeen\tdeposited\tsuccessfully\tat\t\t{time1}\n")


              else:
                  raise ValueError("INVALID PIN TRY AGAIN")

          else:
              raise ValueError("WRONG ACCOUNT NO")

        else:
            raise ValueError("ACCOUNT DOES NOT EXIST")

    def withdraw(self):
        name = input("ENTER YOUR NAME :")
        acc_no = input("ENTER YOUR ACCOUNT NO :")
        filename = name + acc_no
        path = f"ACCOUNTS/{filename}/details.txt"
        if os.path.exists(path):
            with open(path, "r+") as f:
                a = f.readlines()
                length = len(a)-1
                data = a[length].split()
                file_acc_no = data[0]
                file_name = data[1]
                file_pin = data[2]
                file_balance = float(data[3])

                if acc_no == file_acc_no:
                    pin = input("ENTER YOUR PIN :")
                    if pin == file_pin:
                        amount = float(input("ENTER THE AMOUNT :"))
                        file_balance -= amount
                        f.write(f"\n{file_acc_no}\t\t{file_name}\t\t{file_pin}\t\t{file_balance}\t\t{time1}")
                        print("WITHDRAWN SUCCESSFULLY")
                        with open(f"ACCOUNTS/{filename}/transactions.txt","a")as g:
                            g.write(f"\n{file_acc_no}:\t{amount}\thas\tbeen\twithdrawn\tsuccessfully\tat\t\t{time1}\n")


                    else:
                        raise ValueError("INVALID PIN TRY AGAIN")

                else:
                    raise ValueError("WRONG ACCOUNT NO")

        else:
             raise ValueError("ACCOUNT DOES NOT EXIST")

    def balance_check(self):
         name = input("ENTER YOUR NAME :")
         acc_no = input("ENTER YOUR ACCOUNT NO :")
         file_name = name + acc_no
         path = f"ACCOUNTS/{file_name}/details.txt"
         if os.path.exists(path):
             with open(path, "r") as f:
                 a = f.readlines()
                 length = len(a) - 1
                 data = a[length].split()
                 file_acc_no = data[0]
                 file_name = data[1]
                 file_pin = data[2]
                 file_balance = float(data[3])

                 if acc_no == file_acc_no:
                     pin = input("ENTER YOUR PIN :")
                     if pin == file_pin:
                        print(f"BALANCE:{file_balance}")

                     else:
                         raise ValueError("INVALID PIN TRY AGAIN")

                 else:
                     raise ValueError("WRONG ACCOUNT NO")

         else:
             raise ValueError("ACCOUNT DOES NOT EXIST")

    def transactions(self):
        name = input("ENTER YOUR NAME :")
        acc_no = input("ENTER YOUR ACCOUNT NO :")
        filename = name + acc_no
        path = f"ACCOUNTS/{filename}/details.txt"
        if os.path.exists(path):
            with open(path, "r") as f:
                a = f.readlines()
                length = len(a) - 1
                data = a[length].split()
                file_acc_no = data[0]
                file_name = data[1]
                file_pin = data[2]
                file_balance = float(data[3])

                if acc_no == file_acc_no:
                    pin = input("ENTER YOUR PIN :")
                    if pin == file_pin:
                       f= open (f"ACCOUNTS/{filename}/transactions.txt","r")
                       print(f.read())
                       f.close()

                    else:
                        raise ValueError("INVALID PIN TRY AGAIN")

                else:
                    raise ValueError("WRONG ACCOUNT NO")

        else:
            raise ValueError("ACCOUNT DOES NOT EXIST")


class create_acc1(Bank):

    def create_acc(self):
        name = input("ENTER YOUR NAME : ")
        pin = int(input("SETUP A PIN (4-DIGITS): "))
        balance = float(input("ENTER YOUR INITIAL DEPOSIT:"))
        acc_no = str(random.randint(100000, 9999999))
        print("ACCOUNT CREATED SUCCESSFULLY\n")
        print(f"ACCOUNT NO :{acc_no}")
        filename = name+acc_no
        os.makedirs(f"ACCOUNTS/{filename}")
        f = open(f"ACCOUNTS/{filename}/details.txt", "w")
        f.write(f"ACCOUNT NO\t\tNAME\t\tPIN\t\tBALANCE\t\tTIME")
        f.write(f"\n{acc_no}\t\t{name}\t\t{pin}\t\t{balance}\t\t{time1}")
        f.close()
        f = open(f"ACCOUNTS/{filename}/transactions.txt", "a")
        f.close()



class Admin:
     def login(self):
         name = input("ENTER YOUR USERNAME :")
         pass_word = input("ENTER YOUR PASSWORD :")
         with open("ACCOUNTS/admin/details.txt", "r") as f:
             data = f.readlines()[0].split()
             return data[0]==name and data[1]==pass_word

     def view_accounts(self):
         name = input("ENTER THE USER'S NAME :")
         acc_no =input("ENTER ACCOUNT NO :")
         filename = name+acc_no
         path = f"ACCOUNTS/{filename}"
         if path:
             with open( f"ACCOUNTS/{filename}/details.txt","r")as f:
                 print(f.read())
         else:
             print("ACCOUNT DOES NOT EXIST")

     def delete_accounts(self):
         name = input("ENTER THE USER'S NAME :")
         acc_no = input("ENTER ACCOUNT NO :")
         filename = name + acc_no
         path = f"ACCOUNTS/{filename}"
         if path:
             shutil.rmtree(path)
             print("DELETED SUCCESSFULLY")
         else :
             print("ACCOUNT DOES NOT EXIST")



person1 = create_acc1()
bank1 = Bank()
admin = Admin()
#MAIN PROGRAM


while True:
 print("\n  WELCOME TO INFINITY BANK ")
 print(" 1.CREATE ACCOUNT ")
 print(" 2.DEPOSIT")
 print(" 3.WITHDRAW")
 print(" 4.BALANCE CHECK")
 print(" 5.TRANSACTIONS HISTORY")
 print(" 6.ADMIN LOGIN")
 print(" 7.EXIT")

 choice = input("\nENTER YOUR CHOICE:")

 if choice == "1":
     person1.create_acc()
 elif choice == "2":
     bank1.deposit()

 elif choice == "3":
     bank1.withdraw()

 elif choice == "4":
     bank1.balance_check()

 elif choice == "5":
     bank1.transactions()

 elif choice == "6":
     if admin.login():
         while True:
             print("\n--- ADMIN PANEL ---")
             print("1. View Accounts")
             print("2. Delete Accounts")
             print("3. Logout")

             a = input("Choose: ")
             if a == "1":
                 admin.view_accounts()
             elif a == "2":
                 admin.delete_accounts()
             elif a == "3":
                 break
     else:
         print("Invalid admin login!")

 elif choice == "7":
    print("THANK YOU FOR VISITING THE BANK")
    break

 else :
    raise ValueError("INVALID CHOICE")
