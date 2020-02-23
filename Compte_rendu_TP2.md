**________________________________________________|TP n°2|_________________________________________________**

**Exercice 1:**

*1) Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?*

*printenv PATH*

 -> résultat :

 /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin

*2) Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dansvotre répertoire personnel?*

La variable $home

Il suffit de taper cd $home
 
*3) Explicitez le rôle des variables* **LANG,PWD,OLDPWD,SHELL et_.**

**LANG** -> Détermine le languague utilisé par les logiciels pour communiquer avec l'utilisateur.

**PWD** -> Affiche le répértoire courant ou on se situe.

**OLDPWD** -> (echo $OLDPWD) affiche l'avant dernier chemin ou l'utilisateur est allé, par exemple si on utilise succesivement cd /bin puis cd /dev, le résultat de echo $OLDPWD sera /bin.

**SHELL** -> (echo $SHELL) affiche le chemin du fichier de shell

**_** -> (echo $_) sauvegarde le dérnier argument rentrer par l'utilisateur, par exemple si je tape "adadada" puis que j'éxécute echo _ le résultat sera "adadada".

*4) Créez une variable locale **MY_VAR** (le contenu n’a pas d’importance). Vérifiez que la variable existe.*

**MY_VAR="1" ; printenv MY_VAR
 *puis*
 **echo $MY_VAR**

*5) Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin
de cette question, tapez la commande exit pour revenir dans votre session initiale*

bash -> Elle permet de rentrer dans l'environement bash, la variable MY_VAR n'existe plus car elle existe uniquement pour la session ou elle à été créer .


*6)Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.*

**export MY_VAR="1" ; printenv MY_VAR**
Si on retourne dans *bash* , la variable existe puisque cette fois-ci on à créer une variable d'environement et non une variable locale.

*7)Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.
Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.*

**export NOMS="Défossé Défossé" ; printenv NOMS**

résultat : Défossé Défossé

Donc le résultat est correct.


*8)Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2
sont vos deux noms) en utilisant la variable NOMS.*

**echo "Bonjour à vous deux, $NOMS"**

*9)Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande
unset ?*

*Si on met une valeur vide dans la variable, elle ne contient rien mais elle existe toujour.
Si on unest la variable elle est supprimer.*


*10)Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre
dossier personnel d’après bash)*

**echo '$HOME' = $HOME**


**Programmation Bash**

*Pour mettre le dossier script de maniére permanante dans le PATH il faut :*

*A la fin du fichier bashrc* -> **PATH=$PATH:~/script**

*Puis source* **~/.bashrc**

**Exercice 2. Contrôle de mot de passe**
```bash
*#!/bin/bash

PASSWORD="az12"

read -sp "Saisissez un mot de passe :" mdp

if [ $PASSWORD == $mdp ] ; then

echo "MDP ok"

else

echo "Le mdp Saisi n'est pas le bon"

fi

```
**Exercice 3**
```bash
#!/bin/bash




function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
return 1
else
return 0
fi
}

is_number $1

if [ $? == 1 ]; then

echo "Non"

else
echo "Oui"
fi
```
**Exercice 4**
```bash
#!/bin/bash


if [ -z "$1"  ]; then

echo "Utilisation: $0 nom_utilisateur"


else

     test=$(grep $1 /etc/passwd)
        

       if [ -z "$test" ]; then

           echo "L'utilisateur n'existe pas."
       

       else
        
           echo "L'utilisateur existe."

         
       fi

   
 fi



```

**Exercice 5 **

```bash
#!/bin/bash
res=1

for i in `seq 1 $1`;
do
         
     res=$(($res*$i))

done
echo "le factorielle de $1 est $res"
```
**Exercice 6**

```bash
#!/bin/bash

MAXIMUM=1000
MINIMUM=1
VAL=$((MINIMUM+RANDOM*(1+MAXIMUM-MINIMUM)/32767))
Boucle=0
echo $VAL

read -p "Choisissez une valeur:" maVal

echo $maVal

   while [ $Boucle -eq 0 ]; do

     if [ $maVal -eq $VAL ]; then

        Boucle=1
        echo "T balèze twa"

      elif [ $maVal -lt $VAL ]; then

         echo "La valeur est plus grande! "

         read -p "Choisissez une valeur:" maVal
  
      else

         echo "La valeur est plus petite! "

         read -p "Choisissez une valeur:" maVal

      fi

     done

```

**Exercice 7**
```bash
#!/bin/bash

MIN=$1
MAX=$1
MOY=0
MEM=0

nb_val=$#

for i in $(seq 1 $#)
do
   
    if [[ $1 -gt 100 || $1 -lt "-100" ]]; then
        echo "Mauvais paramètre"
        exit 1
       
    else
   
    if [ $1 -lt $MIN ]; then
   
    MIN=$1;   

    else
   
    MAX=$1;

    fi


    MEM=$(($MEM+$1))
   
    shift
   
    fi
   
done
    moy=$(($MEM/$nb_val))
    echo "Valeur moyenne: "$moy
    echo "Valeur max: "$MAX
    echo "Valeur min: "$MIN
    
    
    ```
    ```bash
Exercice 7 (finis) :

#!/bin/bash

MIN=$1
MAX=$1
MOY=0
MEM=0
bool=1

nb_val=$1

for i in $(seq 1 $1);do

read -p "Choisissez une valeur:" var

    if [[ $var -gt 100 || $var -lt "-100" ]]; then
        echo "Mauvais paramètre"
        exit 1
       
    else
  
    if [ $var -lt $MIN ]; then
   
    MIN=$var;   

    else
   
    MAX=$var;

    fi


    MEM=$(($MEM+$var))

   
    shift
   
    fi
   



done
    moy=$(($MEM/$nb_val))
    echo "Valeur moyenne: "$moy
    echo "Valeur max: "$MAX
    echo "Valeur min: "$MIN
    ```
