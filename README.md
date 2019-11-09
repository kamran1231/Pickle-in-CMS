# Pickle-in-CMS



import pickle


class Customer:
    listCus = []

    def __init__(self):
        self.id = 0
        self.name = ""
        self.age = 0
        self.mob = ""

    @staticmethod
    def saveCustomerinFile():
        fs = open("CusMgt.txt", "wb")
        pickle.dump(Customer.listCus, fs)

    @staticmethod
    def loadCustomerfromFile():
        fs = open("CusMgt.txt", "rb")
        Customer.listCus = pickle.load(fs)

    def addCustomer(self):
        Customer.listCus.append(self)

    def searchCustomer(self, id):
        for i in range(len(Customer.listCus)):
            if (id == Customer.listCus[i].id):
                self.name = Customer.listCus[i].name
                self.age = Customer.listCus[i].age
                self.mob = Customer.listCus[i].mob
                return 1
        return 0

    def modifyCustomer(self):
        for i in range(len(Customer.listCus)):
            if (self.id == Customer.listCus[i].id):
                Customer.listCus[i] = self
                return 1
        return 0

    def deleteCustomer(self, id):
        for i in range(len(Customer.listCus)):
            if (id == Customer.listCus[i].id):
                Customer.listCus.pop(i)
                return 1
        return 0

    @staticmethod
    def showAllCustomer():

        import tkinter
        top = tkinter.Tk()
        top.title("SHOW-DATA")
        top.minsize(200, 200)

        tkinter.Label(top, text="ID", width=12, bg="skyblue",font=16).grid(row=0, column=0)
        tkinter.Label(top, text="Name", width=12, bg="green",font=16).grid(row=0, column=1)
        tkinter.Label(top, text="Age", width=12, bg="gray",font=16).grid(row=0, column=2)
        tkinter.Label(top, text="Mobile", width=12, bg="pink",font=16).grid(row=0, column=3)

        for i in range(len(Customer.listCus)):
            for k in range(4):
                if k == 0:
                    lblvalueid = tkinter.Label(top, text=Customer.listCus[i].id, width=12,font=12)
                    lblvalueid.grid(row=i + 1, column=k)
                elif k == 1:
                    lblvaluename = tkinter.Label(top, text=Customer.listCus[i].name, width=12,font=12)
                    lblvaluename.grid(row=i + 1, column=k)
                elif k == 2:
                    lblvalueage = tkinter.Label(top, text=Customer.listCus[i].age, width=12,font=12)
                    lblvalueage.grid(row=i + 1, column=k)
                elif k == 3:
                    lblvaluemob = tkinter.Label(top, text=Customer.listCus[i].mob, width=12,font=12)
                    lblvaluemob.grid(row=i + 1, column=k)

        top.mainloop()


# BLL END

import tkinter
import tkinter.messagebox


def btnAdd_Click():
    cus = Customer()
    cus.id = txtId.get()
    cus.name = txtName.get()
    cus.age = txtAge.get()
    cus.mob = txtMob.get()
    cus.addCustomer()
    mes = len(Customer.listCus), "Customer Added Sucessfully"
    tkinter.messagebox.showinfo("Added", mes)


def btnDelete_Click():
    id = txtId.get()
    cus = Customer()
    flag=cus.deleteCustomer(id)
    if(flag==1):
        tkinter.messagebox.showinfo("Sucess", "Customer Deleted Sucessfully")
    else:
        tkinter.messagebox.showinfo("Failed", "Customer with given ID Not Found")


def btnSearch_Click():
    id = txtId.get()
    cus = Customer()
    flag=cus.searchCustomer(id)
    if (flag == 1):
        varName.set(cus.name)
        varAge.set(cus.age)
        varMob.set(cus.mob)
    else:
        tkinter.messagebox.showinfo("Failed", "Customer with given ID Not Found")



def btnModify_Click():
    cus = Customer()
    cus.id = txtId.get()
    cus.name = txtName.get()
    cus.age = txtAge.get()
    cus.mob = txtMob.get()
    flag=cus.modifyCustomer()
    if(flag==1):
        tkinter.messagebox.showinfo("Success", "Customer Modified Successfully")
    else:
        tkinter.messagebox.showinfo("Failed", "Customer with given ID Not Found")


def showCustomerByIndex(i):
    varID.set(Customer.listCus[i].id)
    varName.set(Customer.listCus[i].name)
    varAge.set(Customer.listCus[i].age)
    varMob.set(Customer.listCus[i].mob)


index = 0


def btnPrev_Click():
    global index
    if (index > 0):
        index = index - 1
    showCustomerByIndex(index)


def btnNext_Click():
    global index
    if (index < len(Customer.listCus) - 1):
        index = index + 1
    showCustomerByIndex(index)


def btnLast_Click():
    index = len(Customer.listCus) - 1
    showCustomerByIndex(index)


def btnLoad_Click():
    Customer.loadCustomerfromFile()
    tkinter.messagebox.showinfo("Successes", "Customer Loaded Successfully")


def btnSave_Click():
    Customer.saveCustomerinFile()
    tkinter.messagebox.showinfo("Successes", "Customer Saved Successfully")


def btnShowall_click():
    Customer.showAllCustomer()


root = tkinter.Tk()
root.title("CMS")
lblId = tkinter.Label(root, text="ID", width=12,height=2,font=16)
lblId.grid(row=0, column=0, columnspan=2)

lblName = tkinter.Label(root, text="Name", width=12,height=2,font=16)
lblName.grid(row=1, column=0, columnspan=2)

lblAge = tkinter.Label(root, text="Age", width=12,height=2,font=16)
lblAge.grid(row=2, column=0, columnspan=2)

lblMob = tkinter.Label(root, text="Mobile No", width=12,height=2,font=16)
lblMob.grid(row=3, column=0, columnspan=2)
varID = tkinter.IntVar()
txtId = tkinter.Entry(root, text="ID", width=12, textvariable=varID,font=16)
txtId.grid(row=0, column=2, columnspan=2)

varName = tkinter.StringVar()
txtName = tkinter.Entry(root, text="Name", width=12, textvariable=varName,font=16)
txtName.grid(row=1, column=2, columnspan=2)

varAge = tkinter.IntVar()
txtAge = tkinter.Entry(root, text="Age", width=12, textvariable=varAge,font=16)
txtAge.grid(row=2, column=2, columnspan=2)

varMob = tkinter.StringVar()
txtMob = tkinter.Entry(root, text="Mobile No", width=12, textvariable=varMob,font=16)
txtMob.grid(row=3, column=2, columnspan=2)

btnAdd = tkinter.Button(root, text="Add", width=10, command=btnAdd_Click,height=2,font=16)
btnAdd.grid(row=4, column=0)

btnSearch = tkinter.Button(root, text="Search", width=10, command=btnSearch_Click,height=2,font=16)
btnSearch.grid(row=4, column=1)

btnDelete = tkinter.Button(root, text="Delete", width=10, command=btnDelete_Click,height=2,font=16)
btnDelete.grid(row=4, column=2)

btnModify = tkinter.Button(root, text="Modify", width=10, command=btnModify_Click,height=2,font=16)
btnModify.grid(row=4, column=3)

btnFirst = tkinter.Button(root, text="First", width=10,height=2,font=16)
btnFirst.grid(row=5, column=0)

btnPrev = tkinter.Button(root, text="Previous", width=10, command=btnPrev_Click,height=2,font=16)
btnPrev.grid(row=5, column=1)

btnNext = tkinter.Button(root, text="Next", width=10, command=btnNext_Click,height=2,font=16)
btnNext.grid(row=5, column=2)

btnLast = tkinter.Button(root, text="Last", width=10, command=btnLast_Click,height=2,font=16)
btnLast.grid(row=5, column=3)

btnLoad = tkinter.Button(root, text="Load Customer", width=21, command=btnLoad_Click,height=2,font=16)
btnLoad.grid(row=6, column=0, columnspan=2)

btnSave = tkinter.Button(root, text="Save Customer", width=21, command=btnSave_Click,height=2,font=16)
btnSave.grid(row=6, column=2, columnspan=2)

btnShowall = tkinter.Button(root, text="Show All", width=21, command=btnShowall_click,height=2,font=16)
btnShowall.grid(row=7, column=0, columnspan=5)

root.mainloop()
