# Leistungsbeurteilung 01 - Ammad Mushtaq

# Inhaltsverzeichnis

1. [Persönlicher Wissenstand](#pW)
2. [Music Browser](#musicbrowser)
2. [K1](#K1)
3. [K2](#K2)
4. [K3](#K3)
5. [K4](#K4)
6. [K5](#K5)

## Persönlicher Wissenstand

| Technologie      | Beschreibung                                                 |
| ---------------- | ------------------------------------------------------------ |
| Linux            | Da ich bisher noch nie in einem Unix/Linux Team war, habe ich nur die Grundkenntnisse von der Schule |
| Virtualisierung  | Ich habe bereits viele virtuelle Maschinen mit einem Hypervisor wie VirtualBox/ VMWare Workstation, Hyper-V aufgesetzt. Privat sowohl auch in der Schule |
| Vagrant          | Vagrant habe ich im Modul 300 neu kennengelernt. Ich verstehe das Prinzip von Vagrant. |
| Git(hub)         | Weil ich Linux kenne, kenne ich auch Git bzw. die Github-Plattform |
| Markdown         | Ich schreibe zum ersten mal Dokumentationen mit Markdown |
| Systemsicherheit | Einen SSH-Key habe ich im diesen Modul erstellt und kennengelernt. |


### Music Browser

#### Beschreibung
Der Music Browser ist nichts anderes als ein **Streaming-Server**, welcher die auf dem Server gespeicherte Musik bequem im lokalen Netzwerk **(LAN)** oder auch über das Internet verteilt. Zum abspielen kann fast jeder beliebige Audio-Player benutzt werden. Falls kein Audio-Player zur Verfügung steht, ist in der Weboberfläche ein Flash-basierter JW Player integriert. Dieser Player ist aber nur bei nicht-kommerzieller Nutzung kostenlos - andere Nutzungsarten erfordern den Kauf einer Lizenz.

#### Netzwerkplan

<a href="https://imgur.com/VLfNuar"><img src="https://imgur.com/VLfNuar.png" title="source: imgur.com" /></a>

#### Vagrant File Shell Code

    $ sudo apt-get update
    $ sudo apt-get -y install apache2
    $ sudo apt-get -y install php libapache2-mod-php
    $ sudo systemctl restart apache2
    $ sudo apt-get -y install unzip
    $ sudo mkdir /musicbrowser
    $ cd /musicbrowser
    $ sudo apt-get -y install git
    $ sudo git clone git://github.com/henrik242/musicbrowser.git
    $ cd /var/www
    $ sudo wget https://github.com/henrik242/musicbrowser/archive/master.zip
    $ sudo unzip master.zip
    $ cd musicbrowser-master/src
    $ sudo cp /tmp/index.php .
    $ cd ..
    $ cd ..
    $ cd ..
    $ cd ..
    $ cd /musicbrowser
    $ sudo cp /tmp/Spaceship.mp3 .
    $ cd ..
    #Sicherheitsaspekte
    $ sudo apt-get install ufw
    $ sudo ufw enable
    $ sudo ufw allow 80/tcp
    $ sudo apt-get install libapache2-mod-proxy-html
    $ sudo apt-get -y install libxml2-de
    $ sudo systemctl restart apache2
    $ sudo a2enmod proxy
    $ sudo systemctl restart apache2
    $ sudo a2enmod proxy_html
    $ sudo systemctl restart apache2
    $ sudo a2enmod proxy_http


# K1

Willkommen zu meiner Markdown über das Modul 300. Hier steht meine Vorgehensweise und meine Prozesse über die LBs im Modul.  Folgende Anleitungen / Links wurden für die Realisierung des LB01s gebraucht:

> https://github.com/ammadope/M300-TBZ <-- my repo
>
> http://iotkit.mc-b.ch/tbz/M300V3/html/10-Installation/
>
> https://github.com/mc-b/M300/tree/master/vagrant/mmdb
>
> https://app.vagrantup.com/boxes/search
>
> https://github.com/mc-b/M300/tree/master/20-Infrastruktur#-02---infrastructure-as-code
>
> https://github.com/mc-b/M300/tree/master/10-Toolumgebung

## Umgebung auf eigenem Notebook eingerichtet und funktionsfähig

VirtualBox wurde auf meiner Windows Maschine (HP-250 G5) installiert. Eine Ubuntu Desktop Maschine wurde ebenfalls erfolgreich installiert.

### Vagrant

> http://iotkit.mc-b.ch/tbz/M300V3/html/10-Installation/40-Vagrant.html

Die Installation erfolgte problemlos.

### Visualstudio-Code

Da ich dieses Programm schon auf meinem Computer installiert habe, war keine zusätzliche Installation nötig. Jedoch habe ich die zwei Extensions dazu installiert.

> Vagrant Extension von Marco Stanzi
>
> vscode-pdf Extension von tomiko1207

### Git-Client

Der Git-Client wurde erfolgreich auf meinem Computer installiert. Ein repo wurde von meinem Github Account erfolgreich geklont.

> https://github.com/ammadope/M300-TBZ

### SSH-Key für Client erstellt

Terminal (*Bash*) öffnen

Folgenden Befehl mit der Account-E-Mail von GitHub einfügen:

```bash
  $  ssh-keygen -t rsa -b 4096 -C "ural.erkut1@gmail.com"
```

Neuer SSH-Key wird erstellt:

```bash
  Generating public/private rsa key pair.
```

Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taste drücken (für Standard):

```bash
  Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
```

Nun kann ein Passwort für den Key festgelegt werden. Ich empfehle dieses zu setzen und anschliessend dem SSH-Agent zu hinterlegen, sodass keine erneute Eingabe (z.B. beim Pushen) notwendig ist:

```bash
  Enter passphrase (empty for no passphrase): [Passwort]
  Enter same passphrase again: [Passwort wiederholen]
```

#### SSH-Key dem SSH-Agent hinzufügen

**Windows und Linux**

Datei %HOME%/.ssh/id_rsa.pub oder $HOME/.ssh/id_rsa.pub in Zwischenablage kopieren.

**macOS**

Terminal (*Bash*) öffnen

SSH-Agent starten:

```
  $ eval "$(ssh-agent -s)"
  Agent pid 931
```

Ab Version macOS High Sierra 10.12.2 muss das



```
~/.ssh/config
```



File angepasst werden, damit SSH-Keys automatisch dem SSH-Agent hinzugefügt werden:

```
  $ sudo nano ~/.ssh/config

  Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Nun muss der Schlüssel dem Agent nur noch hinzugefügt werden:

```
  $ ssh-add -K ~/.ssh/id_rsa
```

Der SSH-Key muss nun nur noch kopiert und anschliessend dem GitHub-Account hinzugefügt werden (siehe "SSH-Key hinzufügen"):

```
  $ pbcopy < ~/.ssh/id_rsa.pub
  # Kopiert den Inhalt der id_rsa.pub Datei in die Zwischenablage
```

### SSH-Key hinzufügen (Github)

------

Anmelden unter [www.github.com](http://www.github.com/)

Auf Benutzerkonto klicken (oben rechts) und den Punkt **Settings** aufrufen

Unter den Menübereichen auf der linken Seite zum Abschnitt **SSH und GPG keys** wechseln

Auf **New SSH key** klicken

Im Formular unter **Title** eine Bezeichnung vergeben (z.B. MB SSH-Key)

Den zuvor kopierten Key mit *CTRL + V* einfügen und auf **Add SSH key** klicken

Der Schlüssel (SSH-Key) sollte nun in der übergeordneten Liste auftauchen

```bash
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCsybLPmHh/P+I1yhzvK+JvqT1Q6ZZyuscPVmoe8fLWwvSKI5jwZ6MttWfitqkfCqmnVw87KDY3p9vuUhu5V8IFBIYmfRASom65jMkq18TpYLtqG9IwsN9aqfCWVk73d0WQdJAVaU6PQUcl0NZUd8jBqVHZb0AOfPaEmER0Jnyz+D4Wy5LtszojjsW8oFnpx60ZI9d/h9FF+TxNuhTPuHm67Cn31IdNIRIVPlESo2WdKlAshwnLW0v/c1pxkDIjHWcKsEuYc4kQGfynCmkQH+UTU2ZMp/xhShX0vJqgjjmxy9PyRxmyNkpHuNd4EupjSWhD6JbgpctU/1ep+JSHykhc7sq9RVVNEvJAvu/l2AgblxI2lXd5xXpEGlffZJZCVnOlHbIyD6r9WZTKW7uNYffXmj1V9nT8RCmhWWmFbSnAmgaPZiot7XLD09cpLU0d9YwkDWKQ4rc5exa47ts3N10PKYXs0h21l0geUDTjgtmZE7KZ73KJCm+w5cVJYeKGTpcZVVH6G5/mS2sYgdcufumEMHNwZUc1w4Sw4BSce8YGcZEFvBxrwojdVPEZRHZUiFA0VlAeucxotR+1U3CTL9lqhRVLEQXuFmrrwtWpUPW3nBuGcBBJGLtkGPUCahlpDMX75vN2ok+MtEUCnYoeuD1gIHTxy/PfNYsbYwLpNbuu6Q== ural.erkut1@gmail.com
```

![1552595015951](C:\Users\urale\AppData\Roaming\Typora\typora-user-images\1552595015951.png)

<a href="https://imgur.com/s8CJJdJ"><img src="https://i.imgur.com/s8CJJdJ.png" title="source: imgur.com" /></a>






> Weiter Infos zu SSH-Keys in Zusammenhang mit GitHub und dem SSH-Agent findet man unter:

> **GitHub-Help:** <https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/>

> **Wikipedia:** <https://en.wikipedia.org/wiki/Ssh-agent>

# K2

## Eigene Lernumgebung (PLE) ist eingerichtet

### GitHub oder Gitlab-Account ist erstellt

Ein GitHub-Account konnte ich problemlos erstellen.



### Git-Client wurde verwendet



Mein Git-Client ist aktiv und mein repo wurde auch geklont.

![Capture](C:\Users\urale\OneDrive - TBZ\Dokumente Modul 300\Capture.PNG)

<a href="https://imgur.com/dFzVv9T"><img src="https://i.imgur.com/dFzVv9T.png" title="source: imgur.com" /></a>


### Dokumentation ist als Markdown vorhanden, Editor ausgewählt und eingerichtet, strukturiert

Mein .md wurde mit Atom geschrieben, eingerichtet und strukturiert.

### Persönlicher Wissenstand im Bezug auf die wichtigsten Themen sind dokumentiert (Linux, VM, Vagrant, Git, .md, Sicherheit)

- Linux:

  Da ich Ubuntu Server 18.04 für die LB01 verwende, heisst das auch, dass ich Erfahrungen in Ubuntu (oder generell Linux) habe.

- VM:

  Zuhause verwende ich die VMware Workstation (betrieben mit Kali Linux). Bezüglich VMs, habe ich genügend Erfahrung für die Realisierung der Lernbeurteilungen dieses Modules.

- Vagrant:

  Vagrant kannte ich vorher nicht. Hier sind die wichtigsten Befehle (für den bash Terminal) aufgelistet:

```bash
$ vagrant ssh. #SSH into virtual machine.
$ vagrant up. #Start virtual machine.
$ vagrant share. #Share your virtual machine to the world via a temporary and unique url.
$ vagrant halt. #Halt virtual machine.
$ vagrant destroy. #Destroy your virtual machine. ...
$ vagrant provision. #Reconfigure the virtual machine after a source code change.
$ vagrant reload. #Reload the virtual machine. Useful when you need to change network or synced folder settings.

#Genauere und mehrere Infos, findet man unter der offizielen Dokumentation: https://www.vagrantup.com/docs/cli/
```

- Git, .md, Sicherheit:

  Ich habe in der vorherigen Modulen noch nie mit Markdown gearbeitet.

  # K3

  ## Vagrant (Kriterien)

  ### Bestehende VM aus Vagrant-Cloud einrichten

  Ich habe die trusty64 Box genommen und kreiert. Für meinen Musicbrowser habe ich dann jedoch ubuntu-18.04-desktop genommen.

  ### Kennt die Vagrant-Befehle

  Die Basics kenne ich, jedoch habe ich ein "cheat sheet" in .md und werfe ab und zu meine Blicke dort drauf.

  Diese .md-Datei habe ich ebenfalls in meinem repo hochgeladen.

| Command           | Beschreibung                                                 |
  | ----------------- | ------------------------------------------------------------ |
  | vagrant up        | Startet virtuelle Maschine                                   |
  | vagrant halt      | Stoppt virtuelle Maschine                                    |
  | vagrant destroy   | Zerstört die virtuelle Maschine. Der Source Code und der Inhalt des Data-Verzeichnisses bleiben unverändert. Nur die VirtualBox Maschinen-Instanz wird zerstört. |
  | vagrant provision | Neukonfiguration der virtuellen Maschine nach einer Source Code Änderung. |
  | vagrant reload    | Neuladen der virtuellen Maschine. Nützlich, wenn man die Einstellungen zu dem Netzwerk oder einen synchronisierten Ordner ändern will. |






# K4



  ## Sicherheitsaspekte sind implementiert

  ### Umgebung

  ### Firewall eingerichtet inkl. Rules und Reverse Proxy
Die Firewall ist aktiv


    sudo apt-get install ufw
    sudo ufw enable
    sudo ufw allow 80/tcp
    sudo apt-get install libapache2-mod-proxy-html
    sudo apt-get -y install libxml2-de
    sudo systemctl restart apache2
    sudo a2enmod proxy
    sudo systemctl restart apache2
    sudo a2enmod proxy_html
    sudo systemctl restart apache2
    sudo a2enmod proxy_http

  ### SSH-Tunnel wurde abgesichtert (pw auth.)

    Kontrollieren ob PasswordAuthentication auf yes ist in...

    ```bash
    root@dhcp:~# cd /etc/ssh
    root@dhcp:/etc/ssh# sudo nano sshd_config
    root@dhcp:/etc/ssh#

    ```




 # K5

  ## Zusätzliche Bewertungspunkte

  ### Testfälle

  | Testfall                                                 | Resultat                                                     |
    | -------------------------------------------------------- | ------------------------------------------------------------ |
    | Vom Client (Host PC) auf http://localhost:8080 zugreifen | Funktioniert.Jedoch wird das PHP File als Code angezeigt |
    | vagrant ssh ammad, sudo -i                                | Funktioniert                                                 |
    | ufw status (Firewall und die Rules abchecken)            | root@ammad:~# ufw status
<br/>Status: active
To                         Action      From
--                         ------      ----
22                            ALLOW       10.0.2.2

80/tcp                      ALLOW       Anywhere

Apache                    ALLOW       Anywhere

80/tcp (v6)                ALLOW       Anywhere (v6)

Apache (v6)              ALLOW       Anywhere (v6) |

  #### Vorgehensweise
  Ich habe jeweils bevor ich die Befehle in das Vagrant File eingab, diese in einer Test-VM manuell eingegeben. So stellte sich zum Beispiel heraus, dass man später,  nach der Befehlseingabe beispielweise aufgeworded wurde, Ja/Nein einzugeben. So konnte man die Befehle im Vagrantfile entsprechend anpassen. Ausserdem tauchten auch weitere Befehle wie zum Beispiel das Installieren von Tools, Neustarten von Services etc. auf, welche in den normalen Anleitungen nicht zu finden waren und man diese so im Vagrant File hinzufügen konnte. Das gleiche galt für die Konfigurationsdateien: Während man sich durch die Installation und Konfiguration durchkämpfte, stiess man oft auf Files, welche angepasst werden mussten. Diese habe ich jeweils lokal auf dem Host-System vorbereitet und dann im Vagrant File mit einem Copy Befehl ersetzt.


  ### Reflexion

  Ich fand die LB01 äusserst spannend. Da "clouding" gerade aktuell in der Welt der Informatiker ist, ist das Modul 300 ein guter Einstieg in das Thema.
  Persönlich hatte ich viele Steine im Wege und die meisten konnte ich wegräumen.#### Reflexion
  Zu Beginn stellte ich mir unter dem Begriff "Music Browser" einen lokalen Service vor, welcher zwischen den Musikdateien auf dem Server browsen und abspielen kann. Während der Installation und dem genaueren lesen wurden mir die Zusammenhänge klar.
