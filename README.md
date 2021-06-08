# Calculator
The Calculator that use tkinter GUI. 


from tkinter import *
import math
global first_num, action, nota_col, rd, AC
action = "none"
first_num = "none"
eq = "none"
num_afteract = "none"
nota = "dec"
nota_col = "Black"
rd = "rad"
AC = "Yes"
sec = "disable"
root = Tk()
root.title("Calculator")

e = Entry(root, width=20, borderwidth=3)
e.grid(row=0, column=0, columnspan=4, padx=10, pady=10)
e.insert(0,"0")

def ins_result(n):
    try:
        result = n
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')

def get_num():
    try:
        a = float(e.get())
        return a
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')

def button_click(num):
    global action, eq, num_afteract, AC
    if num_afteract == "Yes" or eq == "active" or AC == "Yes":
        e.delete(0,END)
        e.insert(0,str(num))
        eq = "none"
        num_afteract = "none"
        AC = "none"
    else:
        a = str(e.get())
        e.delete(0,END)
        e.insert(0, a+str(num))
    

def button_d(dot):
    global action, eq, num_afteract, AC
    if num_afteract == "Yes" or eq == "active" or AC == "Yes":
        e.delete(0,END)
        e.insert(0,str(dot))
        eq = "none"
        num_afteract = "none"
        AC = "none"
    else:
        a = str(e.get())
        e.delete(0,END)
        if a.find(".") == -1:
            e.insert(0, a+".")
        else:
            e.insert(0, a)
    

def clear():
    global first_num, action, eq, num_afteract, AC
    try:
        a = float(e.get())
    except:
        e.insert(0,'ERROR-CLICK"AC"')
    first_num = "none"
    action = "none"
    eq = "none"
    num_afteract = "none"
    e.delete(0, END)
    e.insert(0,"0")
    AC = "Yes"

def sw():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = a*(-1)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    eq = "active"

def percent():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = (a * (0.01))
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    eq = "active"

def devide():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = get_num()
    action = "devide"
    num_afteract = "Yes"

def multiplication():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = get_num()
    action = "multiply"
    num_afteract = "Yes"

def minus():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = get_num()
    action = "minus"
    num_afteract = "Yes"

def addition():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = get_num()
    action = "add"
    num_afteract = "Yes"

def is_integer_num(n):
    if isinstance(n, int):
        return True
    if isinstance(n, float):
        return n.is_integer()
    return False

def equal():
    global first_num, action, eq, nota, nota_col
    eq = "active"
    try:
        second_num = float(e.get())
    except:
        second_num = 'ERROR-CLICK"AC"'
    e.delete(0,END)
    txt = "{:G}"
    try:
        if action == "devide":
            try:
                result = float(first_num)/second_num
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
                action = "none"
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
        elif action == "multiply":
            result = float(first_num)*second_num
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
            action = "none"
        elif action == "minus":
            result = float(first_num)-second_num
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
            action = "none"
        elif action == "add":
            result = float(first_num)+second_num
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
            action = "none"
        elif action == "power_xy":
            try:
                result = pow(float(first_num),second_num)
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
            action = "none"
        elif action == "root_xy":
            try:
                result = float(first_num)**(1/second_num)
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
            action = "none"
        else:
            if is_integer_num(second_num):
                e.insert(0,int(second_num))
            else:
                e.insert(0,second_num)
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')

def power_ten():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = pow(10,a)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def power_e():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = pow(math.e,a)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def power_xy():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = str(e.get())
    action = "power_xy"
    num_afteract = "Yes"

def power_3():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = pow(a,3)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def power_2():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = pow(a,2)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def log_ten():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = math.log(a,10)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def log_e():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = math.log(a)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def root_xy():
    global first_num, action, num_afteract
    if not action == "none" and not num_afteract == "Yes":
        equal()
    first_num = str(e.get())
    action = "root_xy"
    num_afteract = "Yes"


def root_3():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = a**(1/3)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def root_2():
    global eq
    a = get_num()
    e.delete(0,END)
    try:
        result = a**(1/2)
        txt = "{:G}"
        if is_integer_num(result):
            e.insert(0,int(result))
        else:
            e.insert(0,txt.format(result))
    except:
        clear()
        e.delete(0,END)
        e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def sin():
    global eq, rd, sec
    a = get_num()
    if sec == "disable":
        if rd == "rad":
            a = a
        else:
            a = ((a/180)*math.pi)
        e.delete(0,END)
        try:
            result = math.sin(a)
            txt = "{:G}"
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
        except:
            clear()
            e.delete(0,END)
            e.insert(0,'ERROR-CLICK"AC"')
    else:
        e.delete(0,END)
        if rd == "rad":
            try:
                result = math.asin(a)
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
        else:
            try:
                result = (math.asin(a)/math.pi)*180
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def cos():
    global eq, rd, sec
    a = get_num()
    if sec == "disable":
        if rd == "rad":
            a = a
        else:
            a = ((a/180)*math.pi)
        e.delete(0,END)
        try:
            result = math.cos(a)
            txt = "{:G}"
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
        except:
            clear()
            e.delete(0,END)
            e.insert(0,'ERROR-CLICK"AC"')
    else:
        e.delete(0,END)
        if rd == "rad":
            try:
                result = math.acos(a)
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
        else:
            try:
                result = (math.acos(a)/math.pi)*180
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def tan():
    global eq, rd, sec
    a = get_num()
    if sec == "disable":
        if rd == "rad":
            a = a
        else:
            a = ((a/180)*math.pi)
        e.delete(0,END)
        try:
            result = math.tan(a)
            txt = "{:G}"
            if is_integer_num(result):
                e.insert(0,int(result))
            else:
                e.insert(0,txt.format(result))
        except:
            clear()
            e.delete(0,END)
            e.insert(0,'ERROR-CLICK"AC"')
    else:
        e.delete(0,END)
        if rd == "rad":
            try:
                result = math.atan(a)
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
        else:
            try:
                result = (math.atan(a)/math.pi)*180
                txt = "{:G}"
                if is_integer_num(result):
                    e.insert(0,int(result))
                else:
                    e.insert(0,txt.format(result))
            except:
                clear()
                e.delete(0,END)
                e.insert(0,'ERROR-CLICK"AC"')
    action = "none"
    eq = "active"

def factorial():
    global eq,num_afteract
    a = get_num()
    e.delete(0,END)
    if is_integer_num(a):
        result = math.factorial(a)
        e.insert(0,result)
    else:
        e.insert(0,"ERROR")
        num_afteract = "Yes"
    action = "none"
    eq = "active"

def reverse():
    global eq, num_afteract
    a = get_num()
    e.delete(0,END)
    if a == 0:
        clear()
        e.delete(0,END)
        e.insert(0,"ERROR")
        num_afteract = "Yes"
    else:
        a = a
    ins_result(1/a)
    action = "none"
    eq = "active"

def degrad():
    global rd
    if button_DegRad["text"] == "Rad":
        button_DegRad["text"] = "Deg"
        rd = "deg"
    else:
        button_DegRad["text"] = "Rad"
        rd = "rad"

def pi():
    global eq
    clear()
    e.delete(0,END)
    e.insert(0,math.pi)
    eq = "active"

def natural_e():
    global eq
    clear()
    e.delete(0,END)
    e.insert(0,math.e)
    eq = "active"
    
def secondary():
    global sec
    if button_secondary["fg"] == "Black":
        button_secondary["fg"] = "Red"
        button_sin["text"] = "sin^-1"
        button_cos["text"] = "cos^-1"
        button_tan["text"] = "tan^-1"
        sec = "enable"
    else:
        button_secondary["fg"] = "Black"
        button_sin["text"] = "sin"
        button_cos["text"] = "cos"
        button_tan["text"] = "tan"
        sec = "disable"
    

 

button_AC = Button(root, text="AC", padx=26, pady=25, command=clear)
button_sw = Button(root, text="+/-", padx=25, pady=25, command=sw)
button_percent = Button(root, text="%", padx=29, pady=25, command=percent)
button_7 = Button(root, text="7", padx=30, pady=25, command=lambda: button_click(7))
button_8 = Button(root, text="8", padx=30, pady=25, command=lambda: button_click(8))
button_9 = Button(root, text="9", padx=30, pady=25, command=lambda: button_click(9))
button_4 = Button(root, text="4", padx=30, pady=25, command=lambda: button_click(4))
button_5 = Button(root, text="5", padx=30, pady=25, command=lambda: button_click(5))
button_6 = Button(root, text="6", padx=30, pady=25, command=lambda: button_click(6))
button_1 = Button(root, text="1", padx=30, pady=25, command=lambda: button_click(1))
button_2 = Button(root, text="2", padx=30, pady=25, command=lambda: button_click(2))
button_3 = Button(root, text="3", padx=30, pady=25, command=lambda: button_click(3))
button_0 = Button(root, text="0", padx=67, pady=25, command=lambda: button_click(0))
button_dot = Button(root, text=".", padx=32, pady=25, command=lambda: button_d("."))

button_devide = Button(root, text="/", padx=30, pady=25,fg="Blue", command=devide)
button_multiply = Button(root, text="*", padx=29, pady=25, fg="Blue", command=multiplication)
button_minus = Button(root, text="-", padx=29, pady=25, fg="Blue", command=minus)
button_add = Button(root, text="+", padx=29, pady=25, fg="Blue", command=addition)
button_equal = Button(root, text="=", padx=29, pady=25, fg="Blue", command=equal)

button_power_10 = Button(root, text="10^x", padx=25, pady=25, fg="Red", command=power_ten)
button_power_e = Button(root, text="e^x", padx=25, pady=25, fg="Red", command=power_e)
button_power_xy = Button(root, text="x^y", padx=25, pady=25, fg="Red", command=power_xy)
button_power_3 = Button(root, text="x^3", padx=25, pady=25, fg="Red", command=power_3)
button_power_2 = Button(root, text="x^2", padx=25, pady=25, fg="Red", command=power_2)

button_log_10 = Button(root, text="log10(x)", padx=15, pady=25, fg="Red", command=log_ten)
button_log_e = Button(root, text="ln(x)", padx=25, pady=25, fg="Red", command=log_e)
button_root_xy = Button(root, text="y√x", padx=25, pady=25, fg="Red", command=root_xy)
button_root_3 = Button(root, text="3√x", padx=25, pady=25, fg="Red", command=root_3)
button_root_2 = Button(root, text="√x", padx=25, pady=25, fg="Red", command=root_2)

button_sin = Button(root, text="sin", padx=25, pady=25, fg="Red", command=sin)
button_cos = Button(root, text="cos", padx=25, pady=25, fg="Red", command=cos)
button_tan = Button(root, text="tan", padx=25, pady=25, fg="Red", command=tan)
button_factorial = Button(root, text="x!", padx=25, pady=25, fg="Red", command=factorial)
button_reverse = Button(root, text="1/x", padx=25, pady=25, fg="Red", command=reverse)

button_DegRad = Button(root, text="Rad", padx=20, pady=10, fg="Blue", command=degrad)

button_pi = Button(root, text="π", padx=25, pady=10, fg="Blue", command=pi)
button_e = Button(root, text="e", padx=25, pady=10, fg="Blue", command=natural_e)

button_secondary = Button(root, text="2nd", padx=20, pady=10, fg="Black", command=secondary)



button_AC.grid(row=1, column=0)
button_sw.grid(row=1, column=1)
button_percent.grid(row=1, column=2)
button_7.grid(row=2, column=0)
button_8.grid(row=2, column=1)
button_9.grid(row=2, column=2)
button_4.grid(row=3, column=0)
button_5.grid(row=3, column=1)
button_6.grid(row=3, column=2)
button_1.grid(row=4, column=0)
button_2.grid(row=4, column=1)
button_3.grid(row=4, column=2)
button_0.grid(row=5, column=0, columnspan=2)
button_dot.grid(row=5, column=2)
button_devide.grid(row=1, column=3)
button_multiply.grid(row=2, column=3)
button_minus.grid(row=3, column=3)
button_add.grid(row=4, column=3)
button_equal.grid(row=5, column=3)

button_power_10.grid(row=1, column=4)
button_power_e.grid(row=1, column=5)
button_power_xy.grid(row=1, column=6)
button_power_3.grid(row=1, column=7)
button_power_2.grid(row=1, column=8)
button_log_10.grid(row=2, column=4)
button_log_e.grid(row=2, column=5)
button_root_xy.grid(row=2, column=6)
button_root_3.grid(row=2, column=7)
button_root_2.grid(row=2, column=8)
button_sin.grid(row=3, column=4)
button_cos.grid(row=3, column=5)
button_tan.grid(row=3, column=6)
button_factorial.grid(row=3, column=7)
button_reverse.grid(row=3, column=8)

button_DegRad.grid(row=4, column=8)
button_pi.grid(row=4, column=7)
button_e.grid(row=4, column=6)
button_secondary.grid(row=4, column=5)

#button_notation.grid(row=6, column=3)


root.mainloop()
