# Tuto-Install-X-Debug
Installation de X-debug sur Windows/VSCode

Voici les étapes que j'ai suivi pour installer X-debug sous windows avec VSCode.

# 1. Installation de X-debug

- Suivre les instructions fournis sur le site : 
[https://xdebug.org/docs/install#windows](https://xdebug.org/docs/install#windows)

- A la fin de cette étape vérifier que tout s'est bien passé avec la commande :

```
php -v
```

>PHP 8.1.0 (cli) (built: Nov 23 2021 21:48:28) (ZTS Visual C++ 2019 x64)
>Copyright (c) The PHP Group
>Zend Engine v4.1.0, Copyright (c) Zend Technologies
>    with Xdebug v3.1.4, Copyright (c) 2002-2022, by Derick Rethans
 
# 2. Ajout dans le fichier php.ini

- Là où est localisé l'installation de php ( avec wamp, par exmple, ça ressemble à ça : *C:\wamp64\bin\php\php8.1.0*), ouvrez le fichier **php.ini**

- Vérifier bien que vous étes dans le dossier de la version que vous faites tourner sur votre pc ;)

- A la fin du fichier (plus facile pour le retrouver, mais pas d'obligation) ajouter :

>[XDebug]
>zend_extension = xdebug <--- ajouter lors de l'installation de X debug
>
>xdebug.remote_enable = 1
>xdebug.remote_autostart = 1
>
>xdebug.start_with_request=yes
>xdebug.client_host=127.0.0.1
>xdebug.mode=debug;


- La dernière ligne peut ralentir (beaucoup) l'exécution de php, si cela pose un problème, ajouter un *;* en début de ligne pour désactiver l'option.

(Mon mentor m'a expliqué qu'avec symfony, on pouvait déclarer un fichier php.ini qui surcharge l'origininal. Mon mentor écrit cette dernière ligne (*xdebug.mode=debug;*) dans le php.ini de chacun de ses projets et peut rapidement activer ou désactivé l'option. 

# 3. Installation de l'extension et initialisation d'un projet dans VSCode

- Dans VSCode, installer l'extension : **PHP Debug**

- un fois l'extension activé, ouvrez un projet si ce n'est pas déjà fait.

- Dans les icônes latérales à gauche dans VSCode, vous devriez voir l'icone *Executer et deboguer* (le triangle de lecteur avec un petit cafard), cliquez dessus.

- la fenêtre latérale vous propose : *Pour personnaliser Exécuter et Déboguer __créer un fichier launch.json__* 

- Cliquez dessus et choisir php dans les choix proposés. Il génère automatiquement le fichier de config

** Ca marche maintenant !! **

# 4. Pour tester

- Revenez dans le menu *Executer et deboguer* (le triangle de lecteur avec un petit cafard) demarer le débogage avec le triangle vert en haut de la fenêtre (ou appuyer sur F5).
- Votre barre de tache de VSCode change de couleur à ce moment. 
- Mettez un point d'arret à la ligne de votre code à vérifier.
- lancez votre code et vous devriez voir votre code s'arrêter.

>Pour aide : voici un tuto avec une technique un peu differente (laragon) mais il explique le fonctionnement de l'outil X-debug... si ça peut aider... https://youtu.be/So0CWpu0Rf8

Ce tuto est la version alpha, chacun pourrait l'enrichir afin d'en faire un veritable tuto ;)

Info avec Laragon (de Lam's):

Xdebug => Laragon => VSCODE Résolu

Pour ceux qui galère à installer xdebug voici, si il est bien installer mais qu'il ne marche pas sur VSCode voici la config à avoir dans php.ini

zend_extension=C:\laragon\bin\php\php-8.1.9-Win32-vs16-x64\ext\php_xdebug.dll
xdebug.mode = debug
xdebug.client_host = 127.0.0.1
xdebug.client_port = 9003
xdebug.start_with_request=yes
xdebug.idekey = VSCODE
xdebug.discover_client_host=false

Xdebug et en v3 mais le client possède la config de la v2 alors il faut rajouter des paramètres

tips et faq :

php.ini (php8.1.0 windows) :
```[XDebug]
xdebug.idekey=PHPSTORM
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.1
xdebug.file_link_format="phpstorm://open?file=%f&line=%l"


[sendmail]
SMTP=smtp.gmail.com
smtp_port=587
sendmail_from = sebzz13test@gmail.com
sendmail_path = "\"C:\wamp64\sendmail\sendmail.exe\" -t"
```

php.ini du projet :

```xdebug.start_with_request=yes
xdebug.mode=debug
xdebug.log_level=3
xdebug.discover_client_host = 1
```
