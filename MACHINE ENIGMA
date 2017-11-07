
#PROGRAMMATION DE LA MACHINE ENIGMA



#CONVERSION LETTRE -> NOMBRE:

def conversion_nombre(alphabet,lettre):
    for i in range(len(alphabet)):
        if lettre==alphabet[i]:
            return i

def conversion_nombre_liste(alphabet,texte):
    liste_de_nombres=[]
    for i in texte:
        liste_de_nombres.append(conversion_nombre(alphabet,i))
    return liste_de_nombres

#NOUVEL ALPHABET DU AU TABLEAU DE CONNEXION:

def nouvel_alphabet(alphabet,liste_de_listes_avec_deux_lettres):
    new_alphabet=range(len(alphabet))
    for doublet_de_lettres in liste_de_listes_avec_deux_lettres:
        for i in range(len(alphabet)):
            j=conversion_nombre(alphabet,doublet_de_lettres[0])
            k=conversion_nombre(alphabet,doublet_de_lettres[1])
            if i==j:
                new_alphabet[i]=k
                new_alphabet[k]=i
    return conversion_lettre_liste(alphabet,new_alphabet)

def substitution(alphabet_de_depart,alphabet_de_cryptage,texte):
    n=len(alphabet_de_depart)
    m=len(alphabet_de_cryptage)
    nouveau_texte=[]
    if n!=m:
        return "les deux alphabets n'ont pas la même longueur"
    else:
        for i in range(len(texte)):
            for j in range(n):
                if texte[i]==alphabet_de_depart[j]:
                    nouveau_texte.append(alphabet_de_cryptage[j])
        return nouveau_texte

#LE MESSAGE ARRIVE AUX ROTORS:

def passage_rotor(rotor_chiffres,lettre_ie_nombre,indice_de_la_lettre_dans_le_texte,place_du_rotor,nombre_de_rotors):
    r=len(rotor_chiffres)
    return (lettre_ie_nombre+rotor_chiffres[(lettre_ie_nombre+(indice_de_la_lettre_dans_le_texte-1)//(r**(nombre_de_rotors-place_du_rotor)))%r])%r


def fonction_rotor(alphabet,rotor):
    r=len(rotor)
    if r!=len(alphabet):
        return [r,len(alphabet),"tu vois pas que c'est different?"]
    else:
        rotor_chiffre=[]
        for i in range(r):
            rotor_chiffre.append((conversion_nombre(alphabet,rotor[i])-i)%r)
        return rotor_chiffre

def position_initiale_du_rotor(rotor,lettre):
    r=len(rotor)
    nouveau_rotor=[]
    for i in range(r):
        if lettre==rotor[i]:
            for k in range(r):
                nouveau_rotor.append(rotor[(k+i)%r])
    return nouveau_rotor

#ARRIVE LE REFLECTEUR...

def passage_reflecteur(alphabet,reflecteur,lettre_chiffres):
    for element in reflecteur:
        if lettre_chiffres==conversion_nombre(alphabet,element[0]):
            return conversion_nombre(alphabet,element[1])
        elif lettre_chiffres==conversion_nombre(alphabet,element[1]):
            return conversion_nombre(alphabet,element[0])

#ET LE RETOUR DANS LES ROTORS:

def passage_inverse_rotor(rotor_chiffre,lettre_ie_nombre,indice_de_la_lettre_dans_le_texte,place_du_rotor,nombre_de_rotors):
    for i in range(len(rotor_chiffre)):
        if passage_rotor(rotor_chiffre,i,indice_de_la_lettre_dans_le_texte,place_du_rotor,nombre_de_rotors)==lettre_ie_nombre:
            return i

#ENFIN LA RECONVERSION NOMBRE->LETTRE:

def conversion_lettre(alphabet,nombre):
    return alphabet[nombre%len(alphabet)]

def conversion_lettre_liste(alphabet,liste):
    new_liste=[]
    for i in liste:
        new_liste.append(conversion_lettre(alphabet,i))
    return new_liste

#FINALEMENT, LA MACHINE ENIGMA:

def Machine_Enigma(alphabet,tableau_de_connexion,liste_de_rotors,reflecteur,texte):
    n=len(texte)
    m=len(liste_de_rotors)
    texte_chiffre=[]
    nouveau_texte=conversion_nombre_liste(alphabet,substitution(alphabet,nouvel_alphabet(alphabet,tableau_de_connexion),texte))
    for i in range(n):
        for j in range(m):
            nouveau_texte[i]=passage_rotor(fonction_rotor(alphabet,liste_de_rotors[j]),nouveau_texte[i],i+1,j+1,m)
        nouveau_texte[i]=passage_reflecteur(alphabet,reflecteur,nouveau_texte[i])
        for k in range(m):
            nouveau_texte[i]=passage_inverse_rotor(fonction_rotor(alphabet,liste_de_rotors[m-k-1]),nouveau_texte[i],i+1,m-k,m)
        texte_chiffre.append(nouveau_texte[i])
    return substitution(nouvel_alphabet(alphabet,tableau_de_connexion),alphabet,conversion_lettre_liste(alphabet,texte_chiffre))



#EXEMPLE 0: Machine_Enigma(alphabet_0,tableau_de_connexion_0,[rotor1_0,rotor2_0,rotor3_0],reflecteur_0,phrase_0)

reflecteur_0=[["A","B"],["C","F"],["D","E"]]
alphabet_0="ABCDEF"
rotor1_0="BECDFA"
rotor2_0="ACEBDF"
rotor3_0="CDABEF"
tableau_de_connexion_0=[["A","B"]]
phrase_0="BAC"

#EXEMPLE 1: Machine_Enigma(alphabet_1,tableau_de_connexion_1,[rotor1_1,rotor2_1,position_initiale_du_rotor(rotor1_1,"T")],reflecteur_1,phrase_1)

reflecteur_1=["AB","CD","EF","GH","IJ","KL","MN","OP","QR","ST","UV","WX","YZ"]
alphabet_1="ABCDEFGHIJKLMNOPQRSTUVWXYZ"
rotor1_1="AZERTYUIOPQSDFGHJKLMWXCVBN"
rotor2_1="ALEZJVISRUTONPHQMDBCGFKWXY"
tableau_de_connexion_1=[["A","K"],["T","E"],["L","C"],["O","M"]]
phrase_1="CRYPTONSCETTEPHRASEAVECLAMACHINEENIGMA"

#EXEMPLE 2: Machine_Enigma(alphabet_2,tableau_de_connexion_2,[rotor1_2,rotor2_2,rotor3_2],reflecteur_2,phrase_2)

reflecteur_2=[["A","B"],["C","D"],["E","F"],["G","H"],["I","J"],["K","L"],["M","N"],["O","P"],["Q","R"],["S","T"],["U","V"],["W","X"],["Y","Z"],["a","b"],["c","d"],["e","f"],["g","h"],["i","j"],["k","l"],["m","n"],["o","p"],["q","r"],["s","t"],["u","v"],["w","x"],["y","z"]]
alphabet_2="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"
rotor1_2="AaZzEeRrTtYyUuIiOoPpQqSsDdFfGgHhJjKkLlMmWwXxCcVvBbNn"
rotor2_2="AcLExZJvawVIbqSRznsUTOdeNPfHrQgMtDhBjCGkylFmKpuoWXiY"
rotor3_2="azerqsNHYTGBVFREDCXdfwxcvtyghbnjuikMPOLKIUJSZAQWolpm"
tableau_de_connexion_2=[["A","K"],["t","E"],["L","k"],["O","M"]]
phrase_2="PourFinirCeTIPEComplexifionsEncoreUnPeuPlusMaMachineEnigmaEnPrenantUnAlphabetDeCinquanteDeuxCaracteres"

