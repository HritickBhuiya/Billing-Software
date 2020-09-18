# Billing-Software


from tkinter import*
import math,random,os
from tkinter import messagebox
class Bill_App:
    def __init__(self,root):
        self.root=root
        self.root.geometry("1350x700+0+0")
        self.root.title('Billing Software')
        bg_colour="#074463"
        title=Label(self.root,text="Billing Software",bd=12,relief=GROOVE,bg=bg_colour,fg="white",font=('times new roman',30,'bold'),pady=2).pack(fill=X)
        #============================variables####################################################

        ####################Cosmetic==================
        self.soap=IntVar()
        self.face_cream=IntVar()
        self.face_wash=IntVar()
        self.gel=IntVar()
        self.lotion=IntVar()
        #[[[[[[[[[[[[[[[[[[[[[[[[[     Grocery    ]]]]]]]]]]]]]]]]]]]]]]]]]
        self.rice=IntVar()
        self.daal=IntVar()
        self.wheat=IntVar()
        self.sugar=IntVar()
        self.tea=IntVar()
        #((((((((((((((((((((((((((((      colddrinks              ))))))))))))))))))))))))))))
        self.maza=IntVar()
        self.pepsi=IntVar()
        self.coke=IntVar()
        self.beer=IntVar()
        self.sprite=IntVar()
        #$$$$$$$$$$$$$$$$$  Total product price and tax variables $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
        self.cosmetic_price=StringVar()
        self.grocery_price=StringVar()
        self.cold_drinks_price=StringVar()

        self.cosmetic_tax=StringVar()
        self.grocery_tax=StringVar()
        self.cold_drinks_tax=StringVar()
        #############%%%%%%%%%%%%%%     Customers   %%%%%%%%%%%%%%%%%%%%
        self.c_name=StringVar()
        self.c_phn=StringVar()
        
        self.bill_no=StringVar()
        x=random.randint(1000,9999)
        self.bill_no.set(str(x))
        self.search_bill=StringVar()

        #####################customer detail frame########################################

        F1=LabelFrame(self.root,bd=10,relief=GROOVE,text='Customer details',font=('times new roman',15,'bold'),fg='gold',bg=bg_colour)
        F1.place(x=0,y=80,relwidth=1)


        cname_lbl=Label(F1,text="Customer Name",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=0,column=0,padx=20,pady=5)
        cname_txt=Entry(F1,width=23,font="arial,15",textvariable=self.c_name,bd=7,relief=SUNKEN).grid(row=0,column=1,pady=5,padx=10)



        cphn_lbl=Label(F1,text="Phone No.",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=0,column=2,padx=20,pady=5)
        cphn_txt=Entry(F1,width=23,font="arial,15",textvariable=self.c_phn,bd=7,relief=SUNKEN).grid(row=0,column=3,pady=5,padx=10)

        cbill_lbl=Label(F1,text="Bill No.",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=0,column=4,padx=20,pady=5)
        cbill_txt=Entry(F1,width=23,font="arial,15",textvariable=self.search_bill,bd=7,relief=SUNKEN).grid(row=0,column=5,pady=5,padx=10)

        bill_btn=Button(F1,text='Search',command=self.find_bill,width=8,bd=4,fg='red',font='ROGFonts-Regular 13').grid(row=0,column=6,pady=5,padx=45)
        #==============COSMETICS FRAME ===================================
        F2=LabelFrame(self.root,bd=10,relief=GROOVE,text='Cosmetics',font=('times new roman',15,'bold'),fg='gold',bg=bg_colour)
        F2.place(x=5,y=170,width=378,height=400)

        bath_lbl=Label(F2,text="Bath soap",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=1,column=0,padx=10,pady=10,sticky="w")
        bath_txt=Entry(F2,width=18,font="arial,15",textvariable=self.soap,bd=7,relief=SUNKEN).grid(row=1,column=1,pady=15,padx=8)

        cream_lbl=Label(F2,text="Face cream",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=2,column=0,padx=10,pady=10,sticky="w")
        cream_txt=Entry(F2,width=18,font="arial,15",textvariable=self.face_cream,bd=7,relief=SUNKEN).grid(row=2,column=1,pady=15,padx=8)

        wash_lbl=Label(F2,text="Face wash",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=3,column=0,padx=10,pady=10,sticky="w")
        wash_txt=Entry(F2,width=18,font="arial,15",textvariable=self.face_wash,bd=7,relief=SUNKEN).grid(row=3,column=1,pady=15,padx=8)

        gel_lbl=Label(F2,text="Hair gel",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=4,column=0,padx=10,pady=10,sticky="w")
        gel_txt=Entry(F2,width=18,font="arial,15",textvariable=self.gel,bd=7,relief=SUNKEN).grid(row=4,column=1,pady=15,padx=8)

        ltn_lbl=Label(F2,text="Body lotion",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=5,column=0,padx=10,pady=10,sticky="w")
        ltn_txt=Entry(F2,width=18,font="arial,15",textvariable=self.lotion,bd=7,relief=SUNKEN).grid(row=5,column=1,pady=15,padx=8)


        #==============GROCERY FRAME ===================================
        F3=LabelFrame(self.root,bd=10,relief=GROOVE,text='Grocery',font=('times new roman',15,'bold'),fg='gold',bg=bg_colour)
        F3.place(x=400,y=170,width=350,height=400)

        g1_lbl=Label(F3,text="Rice",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=1,column=0,padx=10,pady=10,sticky="w")
        g1_txt=Entry(F3,width=19,font="arial,15",textvariable=self.rice,bd=7,relief=SUNKEN).grid(row=1,column=1,pady=15,padx=8)

        g2_lbl=Label(F3,text="Daal",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=2,column=0,padx=10,pady=10,sticky="w")
        g2_txt=Entry(F3,width=19,font="arial,15",textvariable=self.daal,bd=7,relief=SUNKEN).grid(row=2,column=1,pady=15,padx=8)

        g3_lbl=Label(F3,text="Wheat",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=3,column=0,padx=10,pady=10,sticky="w")
        g3_txt=Entry(F3,width=19,font="arial,15",textvariable=self.wheat,bd=7,relief=SUNKEN).grid(row=3,column=1,pady=15,padx=8)

        g4_lbl=Label(F3,text="Sugar",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=4,column=0,padx=10,pady=10,sticky="w")
        g4_txt=Entry(F3,width=19,font="arial,15",textvariable=self.sugar,bd=7,relief=SUNKEN).grid(row=4,column=1,pady=15,padx=8)

        g5_lbl=Label(F3,text="Tea",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=5,column=0,padx=10,pady=10,sticky="w")
        g5_txt=Entry(F3,width=19,font="arial,15",textvariable=self.tea,bd=7,relief=SUNKEN).grid(row=5,column=1,pady=15,padx=8)

        #++++++++++++++++++++++++ COLD DRINKS +++++++++++++++++++++++++++++++++++

        F4=LabelFrame(self.root,bd=10,relief=GROOVE,text='Cold Drinks',font=('times new roman',15,'bold'),fg='gold',bg=bg_colour)
        F4.place(x=765,y=170,width=350,height=400)

        c1_lbl=Label(F4,text="Maza",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=1,column=0,padx=10,pady=10,sticky="w")
        c1_txt=Entry(F4,width=20,font="arial,15",textvariable=self.maza,bd=7,relief=SUNKEN).grid(row=1,column=1,pady=15,padx=8)

        c2_lbl=Label(F4,text="Pepsi",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=2,column=0,padx=10,pady=10,sticky="w")
        c2_txt=Entry(F4,width=20,font="arial,15",textvariable=self.pepsi,bd=7,relief=SUNKEN).grid(row=2,column=1,pady=15,padx=8)

        c3_lbl=Label(F4,text="Coke",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=3,column=0,padx=10,pady=10,sticky="w")
        c3_txt=Entry(F4,width=20,font="arial,15",textvariable=self.coke,bd=7,relief=SUNKEN).grid(row=3,column=1,pady=15,padx=8)

        c4_lbl=Label(F4,text="Beer",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=4,column=0,padx=10,pady=10,sticky="w")
        c4_txt=Entry(F4,width=20,font="arial,15",textvariable=self.beer,bd=7,relief=SUNKEN).grid(row=4,column=1,pady=15,padx=8)

        c5_lbl=Label(F4,text="Sprite",bg=bg_colour,fg="lightgreen",font=('times new roman',15,"bold")).grid(row=5,column=0,padx=10,pady=10,sticky="w")
        c5_txt=Entry(F4,width=20,font="arial,15",textvariable=self.sprite,bd=7,relief=SUNKEN).grid(row=5,column=1,pady=15,padx=8)

        ############## Bill Area #######################################################
        
        F5=LabelFrame(self.root,bd=10,relief=GROOVE)
        F5.place(x=1150,y=170,width=350,height=400)
        bill_title=Label(F5,text="Bill Area",font="arial 18 bold",bd=7,relief=GROOVE).pack(fill=X)
        scrol_y=Scrollbar(F5,orient=VERTICAL)
        self.txtarea=Text(F5,yscrollcommand=scrol_y.set)
        scrol_y.pack(side=RIGHT,fill=Y)
        scrol_y.config(command=self.txtarea.yview)
        self.txtarea.pack(fill=BOTH,expand=1)

        #++++++++++++++++++++++++++BUTTON FRAME+++++++++++++++++++++++++++++++++++++
        F6=LabelFrame(self.root,bd=10,relief=GROOVE,text='Bill Menu',font=('times new roman',15,'bold'),fg='gold',bg=bg_colour)
        F6.place(x=0,y=570,relwidth=1,height=210)
        m1_lbl=Label(F6,text="Total Cosmetics Price",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=0,column=0,padx=10,pady=1,sticky="w")
        m1_txt=Entry(F6,width=17,font="arial,13",textvariable=self.cosmetic_price,bd=5,relief=SUNKEN).grid(row=0,column=1,pady=10,padx=8)
        m2_lbl=Label(F6,text="Total Groceries Price",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=1,column=0,padx=10,pady=1,sticky="w")
        m2_txt=Entry(F6,width=17,font="arial,13",textvariable=self.grocery_price,bd=5,relief=SUNKEN).grid(row=1,column=1,pady=10,padx=8)
        m3_lbl=Label(F6,text="Total Cold Drinks Price",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=2,column=0,padx=10,pady=1,sticky="w")
        m3_txt=Entry(F6,width=17,font="arial,13",textvariable=self.cold_drinks_price,bd=5,relief=SUNKEN).grid(row=2,column=1,pady=10,padx=8)

        c1_lbl=Label(F6,text=" Cosmetics Tax",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=0,column=2,padx=10,pady=10,sticky="w")
        c1_txt=Entry(F6,width=17,font="arial,13",textvariable=self.cosmetic_tax,bd=5,relief=SUNKEN).grid(row=0,column=3,pady=10,padx=8)
        c2_lbl=Label(F6,text="Groceries Tax",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=1,column=2,padx=10,pady=10,sticky="w")
        c2_txt=Entry(F6,width=17,font="arial,13",textvariable=self.grocery_tax,bd=5,relief=SUNKEN).grid(row=1,column=3,pady=10,padx=8)
        c3_lbl=Label(F6,text="Cold Drinks Tax",bg=bg_colour,fg="white",font=('times new roman',15,"bold")).grid(row=2,column=2,padx=10,pady=10,sticky="w")
        c3_txt=Entry(F6,width=17,font="arial,13",textvariable=self.cold_drinks_tax,bd=5,relief=SUNKEN).grid(row=2,column=3,pady=10,padx=8)

        btn_F=Frame(F6,bd=7,relief=GROOVE,padx=25,pady=15)
        btn_F.place(x=830,width=670,height=150)

        total_btn=Button(btn_F,command=self.total,text='Tota l',bg='green',fg="white",bd=5,font='ROGFonts-Regular 13',pady=25,padx=5).grid(row=0,column=0,padx=10)
        gbill_btn=Button(btn_F,text='Generate Bill',command=self.bill_area,bg='green',fg="white",bd=5,font='ROGFonts-Regular 13',pady=25,padx=5).grid(row=0,column=1,padx=5)
        clear_btn=Button(btn_F,text='Clear',command=self.clear_data,bg='green',fg="white",bd=5,font='ROGFonts-Regular 13',pady=25,padx=5).grid(row=0,column=2,padx=5)
        exit_btn=Button(btn_F,text='Exit',command=self.Exit_app,bg='green',fg="white",bd=5,font='ROGFonts-Regular 13',pady=25,padx=15).grid(row=0,column=3,padx=5)
        self.welcome_bill()
    def total(self):
        self.c_s_p=self.soap.get()*25
        self.c_fc_p=self.face_cream.get()*150
        self.c_fw_p=self.face_wash.get()*90
        self.c_g_p=self.gel.get()*50
        self.c_l_p=self.lotion.get()*200
        self.total_cosmetic_price=float(
                                    self.c_s_p+
                                    self.c_fc_p+
                                    self.c_fw_p+
                                    self.c_g_p+
                                    self.c_l_p
                                    )
        self.cosmetic_price.set("Rs. "+str(self.total_cosmetic_price)) 
        self.c_tax=round((self.total_cosmetic_price*0.05),2)
        self.cosmetic_tax.set('Rs. '+str(self.c_tax))

        self.g_r_p=self.rice.get()*55
        self.g_d_p=self.daal.get()*80
        self.g_w_p=self.wheat.get()*70
        self.g_s_p=self.sugar.get()*30
        self.g_t_p=self.tea.get()*150



        self.total_grocery_price=float(
                                    self.g_r_p+
                                    self.g_d_p+
                                    self.g_w_p+
                                    self.g_s_p+
                                    self.g_t_p
                                    )
        self.grocery_price.set("Rs. "+str(self.total_grocery_price))   
        self.g_tax=round((self.total_grocery_price*0.06),2)                 
        self.grocery_tax.set('Rs. '+str(self.g_tax))       

        self.cd_m_p=self.maza.get()*35
        self.cd_p_p=self.pepsi.get()*40
        self.cd_c_p=self.coke.get()*25
        self.cd_b_p=self.beer.get()*135
        self.cd_s_p=self.sprite.get()*40

        self.total_cold_drinks_price=float(
                                    self.cd_m_p+
                                    self.cd_p_p+
                                    self.cd_c_p+
                                    self.cd_b_p+
                                    self.cd_s_p
                                    )
        self.cold_drinks_price.set("Rs. "+str(self.total_cold_drinks_price))
        self.cd_tax=round((self.total_cold_drinks_price*0.09),2)
        self.cold_drinks_tax.set('Rs. '+str(self.cd_tax)) 

        self.Total_bill = float(self.total_cosmetic_price+self.total_grocery_price+self.total_cold_drinks_price+self.c_tax+self.g_tax+self.cd_tax)

    def welcome_bill(self):
        self.txtarea.delete('1.0',END)
        self.txtarea.insert(END,'\tWelcome Webcode Retail\n')
        self.txtarea.insert(END,f'\n Bill Number : {self.bill_no.get()}')
        self.txtarea.insert(END,f'\n Customer Name : {self.c_name.get()}')
        self.txtarea.insert(END,f'\n Phone No. : {self.c_phn.get()}')
        self.txtarea.insert(END,f'\n======================================')
        self.txtarea.insert(END,f'\n PRODUCT\t\tQTY\t\tPRICE')
        self.txtarea.insert(END,f'\n======================================')
        
    def bill_area(self):
        if self.c_name.get()=="" or self.c_phn.get()=='':
            messagebox.showerror("Error","Customer Details are must")
        elif self.cosmetic_price.get()=='Rs. 0.0' and self.grocery_price.get()=='Rs. 0.0' and self.cold_drinks_price.get()=='Rs. 0.0':
             messagebox.showerror("Error","No Product Purchased")
        else:
            self.welcome_bill()
            #++++++++++++COSMETIC++++++++++++
            if self.soap.get()!=0:
                self.txtarea.insert(END,f'\n Bath Soap\t\t{self.soap.get()}\t\t{self.c_s_p}')
            if self.face_cream.get()!=0:
                self.txtarea.insert(END,f'\n Face Cream\t\t{self.face_cream.get()}\t\t{self.c_fc_p}')
            if self.face_wash.get()!=0:
                self.txtarea.insert(END,f'\n Fcae Wash\t\t{self.face_wash.get()}\t\t{self.c_fw_p}')
            if self.gel.get()!=0:
                self.txtarea.insert(END,f'\n Hair Gel\t\t{self.gel.get()}\t\t{self.c_g_p}')
            if self.lotion.get()!=0:
                self.txtarea.insert(END,f'\n Body Lotion\t\t{self.lotion.get()}\t\t{self.c_l_p}')

            #++++++++++++GROCERY++++++++++++
            if self.rice.get()!=0:
                self.txtarea.insert(END,f'\n Rice\t\t{self.rice.get()}\t\t{self.g_r_p}')
            if self.daal.get()!=0:
                self.txtarea.insert(END,f'\n Daal\t\t{self.daal.get()}\t\t{self.g_d_p}')
            if self.wheat.get()!=0:
                self.txtarea.insert(END,f'\n Wheat\t\t{self.wheat.get()}\t\t{self.g_w_p}')
            if self.sugar.get()!=0:
                self.txtarea.insert(END,f'\n Sugar\t\t{self.sugar.get()}\t\t{self.g_s_p}')
            if self.tea.get()!=0:
                self.txtarea.insert(END,f'\n Tea\t\t{self.tea.get()}\t\t{self.g_t_p}')

            #++++++++++++COLD DRINKS++++++++++++
            if self.maza.get()!=0:
                self.txtarea.insert(END,f'\n Maza\t\t{self.maza.get()}\t\t{self.cd_m_p}')
            if self.pepsi.get()!=0:
                self.txtarea.insert(END,f'\n Pepsi\t\t{self.pepsi.get()}\t\t{self.cd_p_p}')
            if self.coke.get()!=0:
                self.txtarea.insert(END,f'\n Coke\t\t{self.coke.get()}\t\t{self.cd_c_p}')
            if self.beer.get()!=0:
                self.txtarea.insert(END,f'\n Beer\t\t{self.beer.get()}\t\t{self.cd_b_p}')
            if self.sprite.get()!=0:
                self.txtarea.insert(END,f'\n Sprite\t\t{self.sprite.get()}\t\t{self.cd_s_p}')
            
            self.txtarea.insert(END,f'\n--------------------------------------')
            
            if self.cosmetic_tax.get()!="Rs. 0.0":
                self.txtarea.insert(END,f'\n Cosmetic Tax:\t\t{self.cosmetic_tax.get()}')
            
            if self.grocery_tax.get()!="Rs. 0.0":
                self.txtarea.insert(END,f'\n Grocery Tax:\t\t{self.grocery_tax.get()}')
            
            if self.cold_drinks_tax.get()!="Rs. 0.0":
                self.txtarea.insert(END,f'\n Cold Drinks Tax:\t\t{self.cold_drinks_tax.get()}')
            
            self.txtarea.insert(END,f'\n--------------------------------------')
            self.txtarea.insert(END,f'\n Total Bill:\t\tRs. {self.Total_bill}')
            self.txtarea.insert(END,f'\n~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~')
            self.save_bill()


    def save_bill(self):
        op=messagebox.askyesno('Save Bill',"Do You Want To Save The Bill ?")
        if op>0:
            self.bill_data=self.txtarea.get('1.0',END)
            f1=open('Bills/'+str(self.bill_no.get())+".txt","w")
            f1.write(self.bill_data)
            f1.close()
            messagebox.showinfo("Saved",f'Bill No. : {self.bill_no.get()} saved successfully')
        else:
            return

    def find_bill(self):
        present='no'
        for i in os.listdir("Bills/"):
            if i.split('.')[0]==self.search_bill.get():
                f1=open(f'Bills/{i}','r')
                self.txtarea.delete('1.0',END)
            for d in f1:
                self.txtarea.insert(END,d)
                f1.close()
                present='yes'
        if present=='no':
            messagebox.showerror('Error','Invalid Bill No.')
            

    def clear_data(self):
        op=messagebox.askyesno('Clear','Do you want to clear?')
        if op>0:
            ####################Cosmetic==================
            self.soap.set(0)
            self.face_cream.set(0)
            self.face_wash.set(0)
            self.gel.set(0)
            self.lotion.set(0)
            #[[[[[[[[[[[[[[[[[[[[[[[[[     Grocery    ]]]]]]]]]]]]]]]]]]]]]]]]]
            self.rice.set(0)
            self.daal.set(0)
            self.wheat.set(0)
            self.sugar.set(0)
            self.tea.set(0)
            #((((((((((((((((((((((((((((      colddrinks              ))))))))))))))))))))))))))))
            self.maza.set(0)
            self.pepsi.set(0)
            self.coke.set(0)
            self.beer.set(0)
            self.sprite.set(0)
            #$$$$$$$$$$$$$$$$$  Total product price and tax variables $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
            self.cosmetic_price.set('')
            self.grocery_price.set('')
            self.cold_drinks_price.set('')

            self.cosmetic_tax.set('')
            self.grocery_tax.set('')
            self.cold_drinks_tax.set('')
            #############%%%%%%%%%%%%%%     Customers   %%%%%%%%%%%%%%%%%%%%
            self.c_name.set('')
            self.c_phn.set('')
            
            self.bill_no.set('')
            x=random.randint(1000,9999)
            self.bill_no.set(str(x))
            self.search_bill.set('')
            self.welcome_bill()

    def Exit_app(self):
        op=messagebox.askyesno('Exit','Do you want to exit?')
        if op>0:
            self.root.destroy()

                
            
root=Tk()
obj = Bill_App(root)
root.mainloop()
