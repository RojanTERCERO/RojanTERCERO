# Import necessary libraries/modules
from tkinter import *
import tkinter as tk 
from datetime import datetime as dt
from tkinter import messagebox
import csv
import pandas as pd
from tkinter import scrolledtext

root = tk.Tk()

def number_to_words(number):                       

    if not (-1000000 <= number <= 1000000):
        return "Number out of range (-1,000,000 to 1,000,000 supported)"
 
    ones = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"]
    teens = ["", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"]
    tens = ["", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]

    if -1 <= number < 1:
        return "Zero" if number == 0 else "Negative " + ones[abs(number)]


    result = "Negative " if number < 0 else ""
    number = abs(number)

    if 1 <= number < 10:
        result += ones[number]
    elif 10 < number < 20:
        result += teens[number - 10]
    elif 20 <= number <= 99:
        result += tens[number // 10] + (" " + ones[number % 10] if number % 10 != 0 else "")
    elif 100 <= number <= 999:
        result += ones[number // 100] + " Hundred" + (" and " + number_to_words(number % 100) if number % 100 != 0 else "")
    elif 1000 <= number <= 9999:
        result += ones[number // 1000] + " Thousand" + (" " + number_to_words(number % 1000) if number % 1000 != 0 else "")
    elif 10000 <= number <= 99999:
        result += number_to_words(number // 1000) + " Thousand" + (" " + number_to_words(number % 1000) if number % 1000 != 0 else "")
    elif 100000 <= number <= 999999:
        result += ones[number // 100000] + " Hundred Thousand" + (" " + number_to_words(number % 100000) if number % 100000 != 0 else "")
    elif 1000000 <= number <= 9999999:
        result += number_to_words(number // 1000000) + " Million" + (" " + number_to_words(number % 1000000) if number % 1000000 != 0 else "")

    return result

class PayrollSystem():
    def __init__(self, root):
        self.root = root
        self.root.title("PayrollPro | Developed by InfiniteLoopers")
        self.root.minsize(1000,720)
        self.root.maxsize(1000,720)

        label_main=Frame(self.root,bd=1,relief=GROOVE,bg="black")
        label_main.place(x=1,y=1,width=998,height=720)

        label_1=Frame(label_main,bd=1,relief=RAISED,bg="#b0ceb0")
        label_1.place(x=0,y=0,width=996,height=49)
        payroll_slip = Label(label_1, text="Payroll Slip", font=("minecraft", 15,"bold"), bg="#b0ceb0", fg="black", anchor=W, padx=10).place(x=0, y=5,relwidth=1)        
       
        self.time = Label(label_1, text=dt.now().strftime("%Y-%m-%d %H:%M:%S"), font=("minecraft", 15,"bold"), bg="#b0ceb0")
        self.time.pack(anchor="ne", ipady=5, padx=15)        
        def update_label():
            self.time.config(text=dt.now().strftime("%Y-%m-%d %H:%M:%S"))
            root.after(1000, update_label)
        update_label()

        label_2=Frame(label_main,bd=1,relief=GROOVE,bg="#ecf4e9")
        label_2.place(x=0,y=50,width=498,height=110)
        lbl_name = Label(label_2, text="Name                                                :", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=15,relwidth=1)
        self.name = Entry(label_2, font=("minecraft", 9,), bg="#cfe1cf", fg="black", justify=CENTER)
        self.name.place(x=210, y=15,width=250)
        lbl_employee_Id = Label(label_2, text="Employee ID                               :", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=45,relwidth=1)
        self.employee_Id= Entry(label_2, font=("minecraft", 9,), bg="#cfe1cf", fg="black",justify=CENTER)
        self.employee_Id.place(x=210, y=45,width=250)
        label_3=Frame(label_main,bd=1,relief=GROOVE,bg="#ecf4e9")
        label_3.place(x=498,y=50,width=498,height=110)
        lbl_title = Label(label_3, text="Title                                                     :", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=15,relwidth=1)
        self.title = Entry(label_3, font=("minecraft", 9,), bg="#cfe1cf", fg="black",justify=CENTER)
        self.title.place(x=210, y=15,width=250)

        lbl_bankname = Label(label_3, text="Bank Name                                       :", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=45,relwidth=1)
        self.bankname= Entry(label_3, font=("minecraft", 9,), bg="#cfe1cf", fg="black",justify=CENTER)
        self.bankname.place(x=210, y=45,width=250)
       
        department_options = ["",
                            "Administration",
                            "Finance", "Operations",
                            "Sales and Marketing",
                            "IT Development",
                            "IT Support" ,
                            "Systems Administration",
                            "Research and Development" ,
                            "Customer Support",
                            "Legal Affairs",
                            "Supply Chain",
                            "Quality Control",
                            "Marketing",
                            "Health and Safety",
                            "Training and Development",
                            "Corporate Communications",
                            "Project Management",
                            "Legal Department",
                            "Regulatory Compliance",
                            "Risk Management",
                            "Internal Audit",
                            "General Administration",
                               ]
        selected_option = tk.StringVar()
        self.department_var = StringVar(label_3)
        self.department_var.set(department_options[0])
        lbl_department = Label(label_3, text="Department                                   :", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=75,relwidth=1)
       
        self.department_option_menu = OptionMenu(label_3, self.department_var, *department_options)
        self.department_option_menu.config(font=("minecraft",9), bg="#cfe1cf", fg="black",justify=CENTER,relief=GROOVE)
        self.department_option_menu.place(x=210, y=75, width=250, height=25)

        label_4=Frame(label_main,bd=1,relief=GROOVE,bg="#ecf4e9")
        label_4.place(x=0,y=161,width=498,height=250)
        tag1=Label(label_4, text="Description", font=("minecraft", 10,"bold"), bg="#dae9dc", fg="black", anchor="n", padx=10).place(x=0, y=0,relwidth=1)
        lbl_basic_salary = Label(label_4, text="Basic Salary", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=35,relwidth=1)
        lbl_meal_allowance = Label(label_4, text="Meal Allowance", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=65,relwidth=1)
        lbl_trans_allowance = Label(label_4, text="Transportation Allowance", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=95,relwidth=1)
        lbl_medical_allowance = Label(label_4, text="Medical Allowance", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=125,relwidth=1)
        lbl_retirement_insurance = Label(label_4, text="Retirement Allowance", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=155,relwidth=1)
        lbl_tax = Label(label_4, text="Tax", font=("minecraft", 9,), bg="#ecf4e9", fg="black", anchor="w", padx=10).place(x=0, y=185,relwidth=1)
        label_5=Frame(label_main,bd=1,relief=GROOVE,bg="#ecf4e9")
        label_5.place(x=498,y=161,width=249,height=250)
        tag2=Label(Label(label_5, text="Earnings", font=("minecraft", 10,"bold"), bg="#dae9dc", fg="black", anchor="n", padx=10).place(x=0, y=0,relwidth=1))

        self.basic_salary = Entry(label_5, font=("minecraft",9), bg="#cfe1cf", fg="black",justify=CENTER)
        self.basic_salary.place(x=10, y=35, width=230)
        self.meal_allowance = Entry(label_5, font=("minecraft", 9), bg="#cfe1cf", fg="black",justify=CENTER)
        self.meal_allowance.place(x=10, y=65, width=230)
        self.trans_allowance = Entry(label_5, font=("minecraft", 9), bg="#cfe1cf", fg="black",justify=CENTER)
        self.trans_allowance.place(x=10, y=95, width=230)
        self.medical_allowance = Entry(label_5, font=("minecraft", 9,), bg="#cfe1cf", fg="black",justify=CENTER)
        self.medical_allowance.place(x=10, y=125, width=230)

        label_6 = Frame(label_main, bd=1, relief=GROOVE, bg="#ecf4e9")
        label_6.place(x=747, y=161, width=249, height=250)

        tag2 = Label(Label(label_6, text="Deductions", font=("minecraft", 10, "bold"), bg="#dae9dc", fg="black",anchor="n", padx=10).place(x=0, y=0, relwidth=1))
        self.retirement_insurance = Entry(label_6, font=("minecraft", 10,), bg="#cfe1cf", fg="black")
        self.retirement_insurance.place(x=10, y=155, width=230)
        self.tax = Entry(label_6, font=("minecraft", 9,), bg="#cfe1cf", fg="black")
        self.tax.place(x=10, y=185, width=230)

        label_7 = Frame(label_main, bd=1, relief=GROOVE, bg="#dae9dc")
        label_7.place(x=0, y=412, width=498, height=30)
        tag3 = Label(label_7, text="Total", font=("minecraft", 10, "bold"), bg="#dae9dc", fg="black", anchor="w", padx=10).place(x=0, y=0, relwidth=1)

        label_8 = Frame(label_main, bd=1, relief=GROOVE, bg="#dae9dc")
        label_8.place(x=498, y=412, width=249, height=30)

        label_9 = Frame(label_main, bd=1, relief=GROOVE, bg="#dae9dc")
        label_9.place(x=747, y=412, width=249, height=30)

        label_10 = Frame(label_main, bd=1, relief=GROOVE, bg="#ecf4e9")
        label_10.place(x=0, y=442, width=498, height=250)
        lbl_reciept = Label (label_10, text="Receipt", font=("minecraft", 10, "bold"), bg="#cce0c4", fg="black", anchor="center",bd=5,relief=RIDGE, padx=10).place(
            x=0, y=0, relwidth=1)
        self.receipt_text = Text(label_10, font=("minecraft", 9,), bg="#ecf4e9", fg="black", wrap=WORD)
        self.receipt_text.place(x=0, y=30, width=478, height=190)

        scrollbar = Scrollbar(label_10, command=self.receipt_text.yview)
        scrollbar.pack(side=RIGHT, fill=Y,pady=29)
        self.receipt_text.config(yscrollcommand=scrollbar.set)

        label_11 = Frame(label_main, bd=1, relief=GROOVE, bg="#cce0c4")
        label_11.place(x=498, y=442, width=498, height=250)
        lbl_slip = Label (label_11, text="Net Salary", font=("minecraft", 10, "bold"), bg="#cce0c4", fg="black", anchor="center",bd=5,relief=RIDGE, padx=10).place(
            x=0, y=0, relwidth=1)
       
        self.net_pay_words_label = Entry(label_11, font=("minecraft", 9,), bg="#dae9dc", fg="black", justify=CENTER)
        self.net_pay_words_label.place(x=0, y=78, width=498, height=60)
       
        label_12 = Frame(label_main, bd=2, relief=GROOVE, bg="gray", )
        label_12.place(x=0, y=670, width=1000, height=250)

   # BUTTONS     
        # Button to calculate the net pay
        process_button = Button(label_11, text="Calculate",font=("minecraft", 10, "bold"),bg="#b0ceb0", command=self.calculate)
        process_button.place(x=370, y=170)

        # Button to save all values to CSV file
        process_button = Button(label_11, text="Save",font=("minecraft", 10, "bold"),bg="#b0ceb0", command=self.save)
        process_button.place(x=305, y=170)

        # Button to display the CSV file
        clear_button = Button(label_11, text="Clear", font=("minecraft", 10, "bold"),bg="#b0ceb0", command=self.clear)
        clear_button.place(x=235, y=170)

        # Button to display the CSV file
        display_csv_button = Button(label_12, text="All Employees", font=("minecraft", 10, "bold"),bg="#ecf4e9", command=self.display_csv)
        display_csv_button.place(x=15, y=10)

    # OTHER ENTRIES
     
        self.net_pay_entry = Entry(label_11, font=("minecraft", 9,), bg="lightgray", fg="black", justify=CENTER)
        self.net_pay_entry.place(x=0, y=30, width=498, height=50)
       
        self.earnings = Entry(label_8, text="$", font=("minecraft", 9,), bg="#dae9dc", fg="black",justify=CENTER)
        self.earnings.pack(fill=BOTH, expand=True)

        self.deductions = Entry(label_9, font=("minecraft", 9,), bg="#dae9dc", fg="black",justify=CENTER)
        self.deductions.pack(fill=BOTH, expand=True)


    def display_csv(self):
        csv_file_path = "payroll_details.csv"

        try:
            df = pd.read_csv(csv_file_path)
            display_window = tk.Tk()
            display_window.title("ALL EMPLOYEES")
            text_widget = Text(display_window, wrap=tk.NONE)
            text_widget.pack(fill=tk.BOTH, expand=True)

            scrollbar = Scrollbar(display_window, command=text_widget.yview)
            scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
            text_widget.config(yscrollcommand=scrollbar.set)

            text_widget.insert(tk.END, df.to_string(index=False))
            display_window.mainloop()
        except Exception as e:
            messagebox.showerror(f"An error occurred: {str(e)}")

    def calculate(self):
        name = str(self.name.get())
        employee= str(self.employee_Id.get())
        title = str(self.title.get())
        bank_name = str(self.bankname.get())
        department = str(self.department_var.get())
        data = [(name,
                 employee,
                 title,
                 bank_name,
                 department)]
        for name, employee,title, bank_name, department in data:
            if not name : 
                messagebox.showerror("Error", "Please enter name \n" 
                                     "and this should be alphabetical.")
            elif not employee: 
                messagebox.showerror("Error", "Please enter your employee id")
            elif not title : 
                messagebox.showerror("Error", "Please enter your title \n" 
                                     "and this should be alphabetical.")
            elif not bank_name:
                messagebox.showerror("Error", "Please enter bank name \n" 
                                     "and this should be alphabetical.")
            elif not department :
                messagebox.showerror("Error", "Please enter your department")
                return
        try:
            basic_salary = float(self.basic_salary.get())
            meal_allowance = float(self.meal_allowance.get())
            trans_allowance = float(self.trans_allowance.get())
            medical_allowance = float(self.medical_allowance.get())
            retirement_insurance = float(self.retirement_insurance.get())
            tax = float(self.tax.get())
        except ValueError:
            messagebox.showerror("Error", "Please enter your earnings or deductions.")
            return
        total_earnings = basic_salary + meal_allowance + trans_allowance + medical_allowance
        total_deductions = retirement_insurance + tax
        self.net_pay = total_earnings - total_deductions

        self.earnings.delete(0, tk.END)
        self.earnings.insert(0,f"$ {total_earnings:.2f}")
        self.deductions.delete(0, tk.END)
        self.deductions.insert(0,f"$ {total_deductions:.2f}")
        self.net_pay_entry.delete(0, tk.END)
        self.net_pay_entry.insert(0,f"$ {self.net_pay:.2f}") 
        numbers_to_words = int(self.net_pay)

        # Display the converted net pay value
        self.net_pay_words_label.delete(0, tk.END)
        self.net_pay_words_label.insert(0, number_to_words(numbers_to_words))
       
        current_datetime = dt.now().strftime("%Y-%m-%d %H:%M:%S")
        # Details for receipt
        receipt_details = (
            f"====================================================\n"
            f"Name                              {':':>{60}} {name:>{5}}\n"
            f"Employee                          {':':>{53}} {employee:>{5}}\n"
            f"Title                             {':':>{62}} {title:>{5}}\n"
            f"Bank Name                         {':':>{52}} {bank_name:>{5}}\n"
            f"Department                        {':':>{50}} {department:>{5}}\n"
            f"====================================================\n"
            f"Basic Salary                      {':':>{49}} $ {basic_salary:>{5}.2f}\n"
            f"Meal Allowance                    {':':>{46}} $ {meal_allowance:>{5}.2f}\n"
            f"Transport Allowance               {':':>{36}} $ {trans_allowance:>{5}.2f}\n"
            f"Medical Allowance                 {':':>{42}} $ {medical_allowance:>{5}.2f}\n"
            f"Retirement insurance              {':':>{36}} $ {retirement_insurance:>{5}.2f}\n"
            f"Tax                               {':':>{62}} $ {tax:>{5}.2f}\n"
            f"Total Earnings                    {':':>{46}} $ {total_earnings:>{5}.2f}\n"
            f"Total Deductions                  {':':>{43}} $ {total_deductions:>{5}.2f}\n"
            f"====================================================\n"
            f"Net Pay                           {':':>{57}} $ {self.net_pay:>{5}.2f}\n"
            f"====================================================\n"
            f"Date and Time                     {':':>{49}}  {current_datetime:>{5}}\n"
        )
        
            # Update the receipt text widget
        self.receipt_text.delete("1.0", END)  # Clear previous content
        self.receipt_text.insert(END, receipt_details)
    def save (self):
        name = str(self.name.get())
        employee= str(self.employee_Id.get())
        title = str(self.title.get())
        bank_name = str(self.bankname.get())
        department = str(self.department_var.get())       
        basic_salary = float(self.basic_salary.get())
        meal_allowance = float(self.meal_allowance.get())
        trans_allowance = float(self.trans_allowance.get())
        medical_allowance = float(self.medical_allowance.get())
        retirement_insurance = float(self.retirement_insurance.get())
        tax = float(self.tax.get())     
        self.total_earnings = basic_salary + meal_allowance + trans_allowance + medical_allowance
        total_deductions = retirement_insurance + tax
        self.net_pay = self.total_earnings - total_deductions

        totalearnings = (self.earnings.get())
        totaldeductions = (self.deductions.get())
        netpay = (self.net_pay_entry.get())

        # Convert net pay to words    
        numbers_to_words = int(self.net_pay)

        # Display the converted net pay value
        self.net_pay_words_label.delete(0, tk.END)
        self.net_pay_words_label.insert(0, number_to_words(numbers_to_words))
       
        current_datetime = dt.now().strftime("%Y-%m-%d %H:%M:%S")

             # Save details to a CSV file
        self.save_to_csv(name, employee, title, bank_name, department, basic_salary, meal_allowance,
                trans_allowance, medical_allowance, retirement_insurance, tax, totalearnings,
                totaldeductions, netpay, current_datetime)

    def save_to_csv(self, name, employee, title, bank_name, department, basic_salary, meal_allowance,
                trans_allowance, medical_allowance, retirement_insurance, tax, total_earnings,
                total_deductions, net_pay ,current_datetime):
        csv_file_path = "payroll_details.csv"
        try:    
            with open(csv_file_path, mode='a', newline='') as file:
                writer = csv.writer(file)

                # Write header if the file is empty
                if file.tell() == 0:
                    writer.writerow(["Name", "Employee ID", "Title", "Directorate", "Department",
                                    "Basic Salary", "Meal Allowance", "Transport Allowance",
                                    "Medical Allowance", "Retirement Allowance", "Tax",
                                    "Total Earnings", "Total Deductions", "Net Pay", "Time"])
                # Write data to the CSV file
                writer.writerow([name, employee, title, bank_name, department, basic_salary, meal_allowance,
                                trans_allowance, medical_allowance, retirement_insurance, tax, total_earnings,
                                total_deductions, net_pay,current_datetime])

                messagebox.showinfo("CSV Saved", "Payroll details saved to payroll_details.csv")
        except Exception as e:
            messagebox.showerror("Error", f"An error occurred: {str(e)}")

    def display_csv(self):
    # File path to CSV file
        csv_file_path = "payroll_details.csv"

        try:
            df = pd.read_csv(csv_file_path)
            display_window = tk.Tk()
            display_window.title("PayrollPro | Storage") 

            # Text widget for displaying CSV content
            text_widget = scrolledtext.ScrolledText(display_window, wrap=tk.NONE, width=100, height=10)
            text_widget.pack(expand=tk.YES, fill=tk.BOTH)
            scrollbarX = Scrollbar(display_window, command=text_widget.xview, orient=tk.HORIZONTAL)
            scrollbarX.pack(side=tk.BOTTOM, fill=tk.X)
            text_widget.config(xscrollcommand=scrollbarX.set)
            # Insert CSV content into the Text widget
            text_widget.insert(tk.END, df.to_string(index=False))
            # Run the Tkinter event loop for the new window
            display_window.mainloop()
        except Exception as e:
            # Handle any errors that may occur
            messagebox.showerror(f"An error occurred: {str(e)}")
    def clear (self):
        self.name.delete(0, END)
        self.employee_Id.delete(0, END)
        self.title.delete(0, END)
        self.basic_salary.delete(0,END)
        self.bankname.delete(0, END)
        self.department_var.set("")
        self.meal_allowance.delete(0, END)
        self.medical_allowance.delete(0, END)
        self.trans_allowance.delete(0, END)
        self.retirement_insurance.delete(0, END)
        self.deductions.delete(0, END)
        self.receipt_text.delete(1.0, END)
        self.earnings.delete(0, END)
        self.net_pay_entry.delete(0, END)
        self.net_pay_words_label.delete(0, END)
        self.tax.delete(0, END)
        
# Create an instance of the PayrollSystem class
obj = PayrollSystem(root)
# Start the Tkinter event loop
root.mainloop()
