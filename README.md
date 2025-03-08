# Denumirea lucrării de laborator: Utilizarea containerelor ca medii de execuție

## Scopul lucrării: Această lucrare de laborator are ca scop familiarizarea cu comenzile de bază ale OS Debian/Ubuntu. De asemenea, aceasta va permite să vă familiarizați cu Docker și comenzile sale de bază.

## Sarcina: Pornind de la imaginea oficială a sistemului de operare Ubuntu, să se creeze un container care să conțină un server web Apache. Să se creeze o pagină web care să conțină textul "Hello, World!" și să se afișeze într-un browser.

## Descrierea executării lucrării cu răspunsuri la întrebări:
   **1. Pregătire**: 
Am descărcat și instalat Docker Desktop. 
   **2. Executare**:
Am creat un repository nou, denumit containers04, pe care l-am clonat pe calculatorul meu. În directorul containers04, am creat un fișier README.md în care am documentat pas cu pas.
 **3. Pornire și testare**:
În directorul containers04, am pus urmatoarea comanda si
astfel am obținut un terminal interactiv în interiorul containerului, pornind de la imaginea Ubuntu:
```bash
docker run -ti -p 8000:80 --name containers04 ubuntu bash

```
Explicație:
   * docker run: Pornește un nou container.
   * -ti: Alocă un terminal interactiv pentru a putea lucra în container.
   * -p 8000:80: Mapează portul 8000 al sistemului gazdă la portul 80 al containerului, astfel încât să pot accesa serverul web prin browser.
   * --name containers04: Atribuie numele „containers04” containerului pentru identificare ușoară.
   * ubuntu: Specifică imaginea de bază folosită (oficiala Ubuntu).
   * bash: Rulează un shell Bash în container.

 
Această comandă actualizează lista de pachete disponibile din depozitele configurate, asigurându-mă că am cele mai recente informații înainte de instalarea oricărui pachet:
```bash
apt update
```
Am instalat pachetul apache2 (serverul web Apache). Opțiunea -y a confirmat automat instalarea tuturor pachetelor necesare, fără a solicita intervenție manuală :

```bash
apt install apache2 -y
```

Am pornit serviciul Apache, astfel încât serverul web să fie activ și să răspundă la solicitările HTTP:

```bash
service apache2 start
```
 
Am deschis browserul și am navigat la adresa: http://localhost:8000.
*Ce vedeam pe ecran?*
Am vizualizat pagina implicită a serverului Apache, care, în mod obișnuit, afișează un mesaj precum „It works!” sau o pagină de prezentare standard a Apache. Această pagină confirmă faptul că serverul este pornit și funcționează corect.


Această comandă a listat fișierele și permisiunile din directorul /var/www/html/, directorul implicit unde Apache caută fișierele web:

```bash
ls -l /var/www/html/
```
Am creat fișierul index.html cu conținutul HTML ce afișează mesajul „Hello, World!” ca titlu (folosind tag-ul <h1>). Acest fișier devine pagina principală a serverului web: 
```bash
    echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```
*Ce vedeam acum pe ecran?*
După reîmprospătare, pagina web afișa mesajul „Hello, World!” stilizat ca titlu (H1), confirmând că modificarea fișierului index.html a avut succes.

 Am navigat în directorul unde Apache stochează fișierele de configurare pentru site-urile active:
```bash
    cd /etc/apache2/sites-enabled/
```

 Această comandă afișează conținutul fișierului 000-default.conf, care conține setările implicite pentru site-ul Apache, cum ar fi configurația VirtualHost, portul ascultat, DocumentRoot (directorul rădăcină al site-ului) și alte directive de configurare:
```bash
cat 000-default.conf
```
*Ce vedeam pe ecran?*
Pe ecran am văzut conținutul fișierului 000-default.conf, care include directivele de configurare ale serverului Apache pentru site-ul implicit:
```bash
root@e2721d9906e8:/etc/apache2/sites-enabled# cat 000-default.conf
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```
Am închis sesiunea interactivă din container, revenind la mediul de lucru al sistemului gazdă:
```bash
exit
```
Această comandă a listat toate containerele (active și oprite), oferindu-mi o imagine de ansamblu asupra resurselor Docker utilizate:
```bash
docker ps -a
```
```bash
C:\Users\user\Desktop\cv-lab04\containers04> docker ps -a
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS                     PORTS     
NAMES
e2721d9906e8   ubuntu            "bash"                   20 minutes ago   Exited (0) 9 seconds ago
containers04
6fd7878f0798   containers03      "bash"                   7 days ago       Exited (0) 7 days ago
containers03
1bd75cc03d88   postgres:latest   "docker-entrypoint.s…"   5 months ago     Exited (0) 2 months ago
my-containerdocker rm containers04
```
_______________________________________________________________________________________________




PS C:\Users\user\Desktop\cv-lab04\containers04> docker run -ti -p 8000:80 --name containers04 ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
5a7813e071bf: Download complete
Digest: sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782
Status: Downloaded newer image for ubuntu:latest
root@e2721d9906e8:/# 


