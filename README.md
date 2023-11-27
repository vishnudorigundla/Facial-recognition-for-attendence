# Facial-recognition-for-attendence

This mini project aims to develop a facial recognition system for attendance and convert the attendance information to an Excel file. The system will use a camera to capture the faces of students and match them with a database
of known faces to identify the students. Once the students have been identified, their attendance will be recorded in an Excel file. The system will be developedusing the following technologies
like open-cv,tensorflow,pandas etc.

## Features :
The development of a facial recognition system for attendance requires careful consideration of various features to ensure its effectiveness and accuracy. Here's a comprehensive overview of the key features to consider:

### Face Detection:
Real-time face detection: The system should be able to detect faces in real-time, even in crowded environments and under varying lighting conditions.
High-precision face bounding boxes: The system should accurately identify the location and size of each face, providing precise boundaries for feature extraction and recognition.
### Face Recognition:
Accurate face recognition: The system should be able to correctly match captured faces to the enrolled faces in the database.
Robustness against variations: The system should be robust to variations in facial expressions, hairstyles, accessories, and lighting conditions.
High recognition rate: The system should achieve a high recognition rate, minimizing false positives and false negatives.
### Face Enrollment:
Simple and secure enrollment process: The system should provide a user-friendly enrollment process that captures high-quality face images and ensures data security.
Face image quality assessment: The system should assess the quality of captured face images and provide feedback or guidance to improve the enrollment process.
Multi-angle face capture: The system should capture multiple facial images from different angles to enhance recognition accuracy.
### Attendance Management:
Attendance records and reports: The system should generate detailed attendance records, including timestamps, attendance status, and attendance summary reports.
Integration with existing systems: The system should be able to integrate with existing attendance management systems to streamline data exchange.
Real-time attendance updates: The system should provide real-time attendance updates to instructors or administrators for immediate monitoring.

## Software used :
python 3.7 installation,vs code, installation of library's like open cv, face recognition,face detection etc.

## Diagram :
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/5e93eea9-5086-4b51-af26-07953bda2ece)
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/a131d734-cd23-4407-b413-7b92a0231720)

## Program :
```
# Import
import tkinter as tk
from tkinter import *
from PIL import ImageTk,Image
import sqlite3
import os
# FRAME
def quit(*args):
root.destroy()
root = Tk()
root.attributes("-fullscreen", True)
root.configure(background='black')
root.bind("<Escape>", quit)
root.bind("x", quit)
#==============================METHODS=================
=======================
def Database():
global conn, cursor
conn = sqlite3.connect("facedb.db")
cursor = conn.cursor()
cursor.execute("CREATE TABLE IF NOT EXISTS `member` (mem_id
INTEGER NOT NULL PRIMARY KEY
AUTOINCREMENT, username TEXT, password TEXT)")
cursor.execute("SELECT * FROM `member` WHERE `username` = 'rishabh'
AND `password` = '1705'")

if cursor.fetchone() is None:
cursor.execute("INSERT INTO `member` (username, password)
VALUES('rishabh', '1705')")
conn.commit()
label=Label(root)
label.pack()
# Login Page
def Login(event=None):
Database()
if USERNAME.get() == "" or PASSWORD.get() == "":
lbl_text.config(text="Please complete the required field!", fg="red")
else:
cursor.execute("SELECT * FROM `member` WHERE `username` = ? AND
`password` = ?", (USERNAME.get(),
PASSWORD.get()))
if cursor.fetchone() is not None:
HomeWindow0()
USERNAME.set("")
PASSWORD.set("")

lbl_text.config(text="")
else:
lbl_text.config(text="Invalid username or password", fg="red")
USERNAME.set("")
PASSWORD.set("")
cursor.close()
conn.close()
# First Pop up
def HomeWindow0():
global Home
root.withdraw()
Home = Toplevel()
Home.title("FaceCam")
Home.configure(background='black')
Home.bind("<Escape>", quit)
Home.bind("x", quit)
Home.attributes("-fullscreen", True)
lbl_home=Button(Home, text="Successful Login!", command=HomeWindow1,
bd=20, bg="black",

fg="green",
font=('times new roman', 20),relief=RIDGE).pack(fill=BOTH, expand=1)
btn_back = Button(Home, text='Back', command=Back).pack(pady=20)
# def call():
# os.system('python one.py')
# Second Pop up
def HomeWindow1():
global Home1
Home.withdraw()
Home1 = Toplevel()
Home1.attributes("-fullscreen", True)
Home1.configure(background='black')
Home1.bind("<Escape>", quit)
Home1.bind("x", quit)
a=Label(Home1,text="Did you think that was enough??", bg="black",
fg="green",
font=('comic sans ms', 30)).pack(ipady=50)
#Image
path = "./5.png"

img = ImageTk.PhotoImage(Image.open(path))
panel = Label(Home1, image=img)
panel.photo = img
panel.pack()
b=Label(Home1,text="Now the real test begins...",bg="black",
fg="red",font=('comic sans ms',
30)).pack(ipady=50)
c=Button(Home1, text="Authenticate yourself", command=quit,bd=20,
bg="black", fg="red",
font=('times new roman', 20),relief=RIDGE).pack()
g =Button(Home1, text='Back', command=HomeWindow0).pack(pady=20)
# Face Recognition
# def Facec1():
# global facec1
# Home1.withdraw()
# facec1= Toplevel()
# Back Button
def Back():
Home.destroy()

root.deiconify()
#==============================VARIABLES================
======================
USERNAME = StringVar()
PASSWORD = StringVar()
#==============================FRAMES===================
======================
Top = Frame(root, bd=10, relief=RIDGE)
Top.pack(side=TOP, fill=X)
Faltu=Frame(root, height=500, relief=RIDGE)
Faltu.pack(side=TOP, fill=X, ipady=50, ipadx=200)
Form = Frame(root, height=50, bd=30)
Form.pack(side=TOP, pady=20)
#==============================LABELS===================
======================
lbl_title = Label(Top, text = "Welcome to Smart College", bg="black",
fg="green", font=('Helvetica', 64))
lbl_title.pack(fill=BOTH,expand=1)
lb_title = Label(Top, text = "FaceCam", bg="black", fg="green",
font=('Helvetica', 64))

lb_title.pack(fill=BOTH,expand=1)
cre=Label(Faltu, text= "Enter your credentials: ", fg="green", bg="black",
font=('Verdana',20))
cre.pack(fill=BOTH, expand=1)
lbl_username = Label(Form, text = "Username:", font=('arial', 14), bd=15)
lbl_username.grid(row=0, sticky="e")
lbl_password = Label(Form, text = "Password:", font=('arial', 14), bd=15)
lbl_password.grid(row=1, sticky="e")
lbl_text = Label(Form)
lbl_text.grid(row=2, columnspan=2)
#==============================ENTRY
WIDGETS==================================
username = Entry(Form, textvariable=USERNAME, font=(14))
username.grid(row=0, column=1)
password = Entry(Form, textvariable=PASSWORD, show="*", font=(14))
password.grid(row=1, column=1)
#==============================BUTTON
WIDGETS=================================
btn_login = Button(Form, text="Login", width=45, command=Login)
btn_login.grid(pady=25, row=3, columnspan=2)
btn_login.bind("<Return>", Login)
#==============================INITIALIATION=============
=====================
# if __name__ == '__main__':
root.mainloop()
# # Facial_Recog
#In[ ]:

```
## Output :
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/b3cf4d76-e3f4-4823-90a5-7f0802f1d39d)

![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/d5606923-8335-49a1-89a1-fc94ad10e86a)
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/8462312f-2dd0-4d1b-821b-d363741c4948)
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/c5fa68d2-13b6-4360-9dd6-239708101a43)
![image](https://github.com/vishnudorigundla/Facial-recognition-for-attendence/assets/94175324/5573013c-616e-4817-991f-938b5eaf6b1d)

## Result :

Therefore the development of the facial detection system for attendence is detecting the face and it store the essential information of a particular student like name,reg.no,date & time etc in the exel sheet is executed successfully.

