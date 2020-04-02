from tkinter import *
import os

# Designing window for registration of new Faculty

def register():
    global register_screen
    register_screen = Toplevel(main_screen)
    register_screen.title("Register")
    register_screen.geometry("300x250")

    global username
    global password
    global username_entry
    global password_entry
    username = StringVar()
    password = StringVar()

    Label(register_screen, text="Staff Login", bg="orange").pack()
    Label(register_screen, text="").pack()
    username_lable = Label(register_screen, text="Username * ")
    username_lable.pack()
    username_entry = Entry(register_screen, textvariable=username)
    username_entry.pack()
    password_lable = Label(register_screen, text="Password * ")
    password_lable.pack()
    password_entry = Entry(register_screen, textvariable=password, show='*')
    password_entry.pack()
    Label(register_screen, text="").pack()
    Button(register_screen, text="Register", width=10, height=1, bg="yellow", command=register_user).pack()


# Designing window for  login

def login():
    global login_screen
    login_screen = Toplevel(main_screen)
    login_screen.title(" Staff Login")
    login_screen.geometry("300x250")
    Label(login_screen, text="Please enter your Details ").pack()
    Label(login_screen, text="").pack()

    global username_verify
    global password_verify

    username_verify = StringVar()
    password_verify = StringVar()

    global username_login_entry
    global password_login_entry

    Label(login_screen, text="Username * ").pack()
    username_login_entry = Entry(login_screen, textvariable=username_verify)
    username_login_entry.pack()
    Label(login_screen, text="").pack()
    Label(login_screen, text="Password * ").pack()
    password_login_entry = Entry(login_screen, textvariable=password_verify, show='*')
    password_login_entry.pack()
    Label(login_screen, text="").pack()
    Button(login_screen, text="Login", width=10, height=1, command=login_verify).pack()


# Implementing event on register button

def register_user():
    username_info = username.get()
    password_info = password.get()

    file = open(username_info, "w")
    file.write(username_info + "\n")
    file.write(password_info)
    file.close()

    username_entry.delete(0, END)
    password_entry.delete(0, END)

    Label(register_screen, text="Registration Success", fg="green", font=("calibri", 11)).pack()


# Implementing event on login button

def login_verify():
    username1 = username_verify.get()
    password1 = password_verify.get()
    username_login_entry.delete(0, END)
    password_login_entry.delete(0, END)

    list_of_files = os.listdir()
    if username1 in list_of_files:
        file1 = open(username1, "r")
        verify = file1.read().splitlines()
        if password1 in verify:
            login_sucess()

        else:
            password_not_recognised()

    else:
        user_not_found()


# Designing popup for login success

def login_sucess():
    global login_success_screen
    global delete_login_success_screen
    
    login_success_screen = Toplevel(login_screen)
    login_success_screen.title("Welcome to Faculty page")
    login_success_screen.geometry("300x250")
    Label(login_success_screen,text="Enter the  Subject and Department",bg="orange",width="300",height="2",font=("Calibri",13)).pack()
    Label(login_success_screen,text="").pack()
    Button(login_success_screen,text="Department", height="2", width="30", command=generate_time_table).pack()
    Label(login_success_screen,text="").pack()
    Button(login_success_screen,text="Subjects", height="2", width="30", command=generate_time_table).pack()

# Designing popup for login invalid password

def password_not_recognised():
    global password_not_recog_screen
    password_not_recog_screen = Toplevel(login_screen)
    password_not_recog_screen.title("Success")
    password_not_recog_screen.geometry("150x100")
    Label(password_not_recog_screen, text="Invalid Password ").pack()
    Button(password_not_recog_screen, text="OK", command=delete_password_not_recognised).pack()


# Designing popup for user not found

def user_not_found():
    global user_not_found_screen
    user_not_found_screen = Toplevel(login_screen)
    user_not_found_screen.title("Success")
    user_not_found_screen.geometry("150x100")
    Label(user_not_found_screen, text="User Not Found").pack()
    Button(user_not_found_screen, text="OK", command=delete_user_not_found_screen).pack()

# Generating time table    

def generate_time_table():
    global generate_time_table
    global delete_generate_time_table
    generate_time_table=Toplevel(login_screen)
    generate_time_table.title("Time table Generator")
    generate_time_table.geometry("600x300")
    Label(generate_time_table, text="Enter the details below as per the slots given").pack()
    Button(generate_time_table, text="Submit",command=delete_generate_time_table).pack()


# Deleting popups

def delete_login_success():
    login_success_screen.destroy()
    
def delete_password_not_recognised():
    password_not_recog_screen.destroy()


def delete_user_not_found_screen():
    user_not_found_screen.destroy()

def delete_generate_time_table():
    generate_time_table.destroy()
    

# Designing Main(first) window

def main_account_screen():
    global main_screen
    main_screen = Tk()
    main_screen.geometry("300x250")
    main_screen.title("Account Login")
    Label(text="Intelligent Time Table Maker", bg="blue", width="300", height="2", font=("Calibri", 13)).pack()
    Button(text="Faculty Login", height="2", width="30",command=login).pack()
    Button(text="Student Time Table", height="2", width="30",command=delete_login_success).pack()    
    Button(text="Register new ID Login", height="2", width="30",command=register).pack()
    main_screen.mainloop()


main_account_screen()
