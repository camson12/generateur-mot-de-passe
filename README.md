# generateur-mot-de-passe
import tkinter as tk
from tkinter import messagebox
import random
import string

# Fonction pour générer un mot de passe
def generer_mot_de_passe(longueur, utiliser_majuscules, utiliser_minuscules, utiliser_chiffres, utiliser_speciaux):
    
    types_selectionnes = sum([utiliser_majuscules, utiliser_minuscules, utiliser_chiffres, utiliser_speciaux])
    if types_selectionnes < 4:
        messagebox.showwarning("Erreur", "Veuillez sélectionner au moins 4 types de caractères.")
        return ""

   #
    caracteres = ""
    if utiliser_majuscules:
        caracteres += string.ascii_uppercase  
    if utiliser_minuscules:  
        caracteres += string.ascii_lowercase  
    if utiliser_chiffres:
        caracteres += string.digits  
    if utiliser_speciaux:
        caracteres += string.punctuation  

    #
    mot_de_passe = ''.join(random.choice(caracteres) for _ in range(longueur))
    return mot_de_passe

#
def on_generer_click():
    try:
        longueur = int(entry_longueur.get())  
        if longueur < 8: 
            messagebox.showwarning("Erreur", "La longueur doit être d'au moins 8 caractères.")
            return
    except ValueError:
        messagebox.showwarning("Erreur", "Veuillez entrer une longueur valide.")
        return

   #
    utiliser_majuscules = var_majuscules.get()
    utiliser_minuscules = var_minuscules.get()
    utiliser_chiffres = var_chiffres.get()
    utiliser_speciaux = var_speciaux.get()

#
    mot_de_passe = generer_mot_de_passe(longueur, utiliser_majuscules, utiliser_minuscules, utiliser_chiffres, utiliser_speciaux)
    if mot_de_passe:
        entry_mot_de_passe.delete(0, tk.END) 
        entry_mot_de_passe.insert(0, mot_de_passe)  # Afficher le nouveau mot de passe

#
fenetre = tk.Tk()
fenetre.title("Générateur de mots de passe sécurisés")
fenetre.geometry("400x300") 

# Ajouter une étiquette pour la longueur
label_longueur = tk.Label(fenetre, text="Longueur du mot de passe (min. 8) :")
label_longueur.pack(pady=10)


entry_longueur = tk.Entry(fenetre)
entry_longueur.pack(pady=5)

#
var_majuscules = tk.BooleanVar()
check_majuscules = tk.Checkbutton(fenetre, text="Inclure des lettres majuscules", variable=var_majuscules)
check_majuscules.pack(pady=5)

var_minuscules = tk.BooleanVar()
check_minuscules = tk.Checkbutton(fenetre, text="Inclure des lettres minuscules", variable=var_minuscules)
check_minuscules.pack(pady=5)

var_chiffres = tk.BooleanVar()
check_chiffres = tk.Checkbutton(fenetre, text="Inclure des chiffres", variable=var_chiffres)
check_chiffres.pack(pady=5)

var_speciaux = tk.BooleanVar()
check_speciaux = tk.Checkbutton(fenetre, text="Inclure des caractères spéciaux", variable=var_speciaux)
check_speciaux.pack(pady=5)

#
bouton_generer = tk.Button(fenetre, text="Générer", command=on_generer_click)
bouton_generer.pack(pady=10)


entry_mot_de_passe = tk.Entry(fenetre, font=("Arial", 12), justify="center")
entry_mot_de_passe.pack(pady=10)

# Lancer la boucle principale de Tkinter
fenetre.mainloop()
