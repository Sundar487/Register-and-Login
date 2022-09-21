import re
regex =r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
reg = "^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*^#?&])[A-Za-z\d@$!#%*?&]{6,20}$"

def check(email):
    if (re.fullmatch(regex, email)):
        print("success")
    else:
        print("Invalid Email")
        register()

def checkpassword(password):
    if (re.fullmatch(reg,password )):
        print("success")
    else:
        print("Invalid Email")



def register():
    db = open("database.txt", "r")
    Username = input("Enter a username:")
    check(Username)

    Password = input("Create password:")
    checkpassword(Password)
    Password1 = input("Confirm Password:")

    d = []
    f = []
    for i in db:
        a,b = i.split(", ")
        b = b.strip()
        d.append(a)
        f.append(b)
    data = dict(zip(d,f))

    if Password != Password1:
        print("Passwords don't match,restart")
        register()
    else:
        if Username in d:
            print("username exists")
            register()
        else:
            db = open("database.txt", "a")
            db.write(Username+", "+Password+"\n")
            print("Success")



def gainAccess():
    Username = input("Enter your username:")
    Password = input("Enter your Password:")

    if not len(Username or Password) < 1:
        if True:
            db = open("database.txt", "r")
            d = []
            f = []
            for i in db:
                a, b = i.split(",")
                b = b.strip()
                c = a, b
                d.append(a)
                f.append(b)
                data = dict(zip(d, f))
            try:
               if data[Username]:
                   try:
                       if Password == data[Username]:
                           print("Login success")
                           print("Hi", Username)
                       else:
                           print("Password or Username incorrect")
                   except:
                       print("incorrect password or username")
               else:
                   print("Username or password doesn't exist")
            except:
                print("Username or password doesn't exist")
        else:
            print("Please enter a value")


def home(option=None):
    option = input("Login | Signup:")

    if option == "Login":
        gainAccess()
    elif option == "Signup":
        register()
    else:
        print("Please enter a valid parameter, this is case-sensitive")

home()
