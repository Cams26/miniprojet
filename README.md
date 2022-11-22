# miniprojet
# cette fonction permet d'afficher la carte initiale
def display_map(m,d):
    for i in m:
        for j in i:
            if j in d:
                print (d[j], end="")
        print ()
    print("\n")
    return

#2.2 création d'un personnage
def create_perso(depart):
    dic={}
    dic["repr"]="o" #\U0001f412
    dic["x"]=depart[0]
    dic["y"]=depart[1]
    return dic
    

# permet  d'afficher la carte et la position du personnage
def display_map_and_char(m,d,p):
    for i in range (len(m)):
        for j in range (len(m[i])):
            if i==p['x'] and j==p['y']:
                print (p['repr'], end='')
            elif m[i][j] in d:
                print (d[m[i][j]], end='')
        print ()
    return


def update(letter, perso):
    letter= input
    if letter=='s':
        perso['x']+=1
    elif letter=='q':
        perso['y']-=1
    elif letter=='z':
        perso['x']-=1
    elif letter=='d':        
        perso['y']+=1


mat=[[0, 0, 0, 1, 0, 0, 0],
[0, 1, 0, 0, 0, 0, 0],
[0, 1, 0, 0, 1, 0, 0],
[0, 0, 1, 0, 0, 0, 0]]
dicco={0:'_', 1: '#'}

#display_map(mat, dicco)

perso=create_perso((0,0))

#print(perso)


mat_indice_xmax =len(mat)-1
mat_indice_ymax =len(mat[1])-1


#on modifie notre update de base afin de pouvoir monter(resp.descendre) que lorsqu'il y a une échelle

def  update_p(mat,letter,perso):
     n,m=perso['x'],perso['y']
     if letter=='s' and perso['x'] < mat_indice_xmax and mat[n+1][m]==1:
         perso['x']+=1
     elif letter=='q' and perso['y'] > 0 :
         perso['y']-=1
     elif letter=='z'  and perso['x'] > 0 and mat[n-1][m]==1:
         perso['x']-=1
     elif letter=='d' and perso['y'] < mat_indice_ymax: 
        perso['y']+=1
     else:
         print("\nerror, position ou lettre invalide")

while True:
    # affichage de la matrice 
    display_map_and_char(mat, dicco, perso)
    # deplacement du personnage
    letter=input("\nquel deplacement ?")
    if letter=='E':
        #  saved in file
        break
    else:
        update_p(mat, letter, perso)


#3.4 objets à récolter
#3.4.1 création des objets

def create_objects(nb_objects,mat):
   l=[]
   x=len(mat)-1
   y=len(mat[1])-1
   if nb_objects>(x+1)*(y+1):
      print("\nerror, nombre d'objets trop grand")
   else:
       while (len(l)<(nb_objects)):
            xprime=random.randint(0,x)
            yprime=random.randint(0,y)
            if (xprime,yprime) not in l:
               l.append((xprime,yprime))
       return l
create_objects(nb_objects, mat)
