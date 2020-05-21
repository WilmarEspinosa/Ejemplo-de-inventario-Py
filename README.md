# Ejemplo-de-inventario-Py
Breve inventario en PYTHON
import tkinter as tk
import matplotlib.pyplot as plt

some_list=[]

with open("Lista de mercado.txt","w+") as f: 
    for line in f:
       some_list.append(line.strip().split(" "))
       
print(some_list)       
       
calc=tk.Tk()
calc.title("lista de mercado")

frame1 = tk.Frame(calc)
frame2 = tk.Frame(calc)
frame3 = tk.Frame(calc)

listadetiquetas=["Articulo","Cantidad","Peso","Fecha de compra","Vencimiento estimado"]
listadevariables=["a","b","c","d","e"]

for i in range(len(listadetiquetas)):
    exec('label%d=tk.Label(frame2,text="%s")\nlabel%d.grid(row=i,column=1)' % (i,listadetiquetas[i],i))
    exec('e%d=tk.Entry(frame2)\ne%d.grid(row=i,column=2)' % (i,i))

for i in range(len(listadevariables)):
   exec('%s=0' % (listadevariables[i]))   

def graficar():
    lista=[]
    listb=[]
    for i in range(len(some_list)):
     lista.append(some_list[i][0])
     listb.append(some_list[i][1])
    plt.plot(lista,listb,'r-')
    plt.savefig('books_read.png')   

def ingreso_articulo():
     listadearticulos=[]
     for i in range(len(listadevariables)):
       exec("try:\n global %s\n %s=(e%d.get())\n listadearticulos.append(%s)\nexcept(ValueError):\n pass"%(listadevariables[i],listadevariables[i],i,listadevariables[i]))
     global some_list
     some_list.append(listadearticulos)   
     print(some_list)
     
def escribir():
  for line in range(len(some_list)):
   for ele in range(5):
    L=str(some_list[line][ele])  
    if ele<4:
     f.write("%s " %(L))
    else:
     f.write("%s\n" % (L))
        
b1=tk.Button(frame1,text="Ingresar",fg="blue",command=ingreso_articulo)
b1.grid(row=0,column=0)
b2=tk.Button(frame1,text="imprimir",fg='red',command=escribir)
b2.grid(row=1,column=0)
b3=tk.Button(frame1,text="Graficar",fg='brown',command=graficar)
b3.grid(row=2,column=0)

img=tk.PhotoImage(file='books_read.png')
Labelim=tk.Label(frame3,image=img)
Labelim.grid(row=50,column=51)  

frame1.grid(row=1,column=0,padx=0,pady=0)
frame2.grid(row=1,column=50,padx=50,pady=0)
frame3.grid(row=1,column=100,padx=100,pady=100)

calc.mainloop()
