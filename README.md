# Cine-critiques

Blog de critiques de films, genere par Hugo, heberge sur seedhost.

## Structure

```
Sur ta machine (repo Git) :
  cinecritiques/
    hugo.toml
    deploy.bat            <- PAS dans Git (contient le mdp)
    content/films/
      pacifiction/
        index.md
      amen/
        index.md
    layouts/
    static/css/

Sur seedhost (via WinSCP) :
  html/CRITIQUES/cinema/
    index.html            <- genere par Hugo, uploade par deploy.bat
    films/...             <- genere par Hugo
    css/...               <- genere par Hugo
    media/                <- uploade A LA MAIN via WinSCP
      films/
        pacifiction/
          serra_bar.jpg
          extrait_boite.mp4
          ambiance_port.mp3
        amen/
          affiche_amen.jpg
```

## Installation (une seule fois)

1. Installer Hugo : https://gohugo.io/installation/windows/
   Telecharger hugo_extended, extraire, ajouter au PATH.

2. Verifier dans un terminal :
   ```
   hugo version
   ```

3. Editer `deploy.bat` :
   - Mettre ton vrai mot de passe seedhost a la ligne SEEDHOST_PASS
   - Verifier le chemin WinSCP (WINSCP_PATH)
   - Verifier le chemin distant (REMOTE_PATH) : ouvrir WinSCP,
     naviguer vers le dossier html, noter le chemin complet

4. Sur seedhost via WinSCP, creer le dossier :
   ```
   html/CRITIQUES/cinema/media/films/
   ```

## Ecrire une nouvelle critique

1. Creer le dossier et fichier :
   ```
   content/films/le-nom-du-film/index.md
   ```

2. En-tete YAML :
   ```yaml
   ---
   title: "Le Nom du Film"
   director: "Nom du Realisateur"
   directors: ["Nom du Realisateur"]
   year: 2024
   countries: ["France"]
   rating: 4
   viewings:
     - date: 2025-02-15
     - date: 2025-06-01
       note: "Revu en plein air"
   draft: false
   ---
   ```

3. Ecrire la critique. Pour inserer des medias :
   - Image : `{{</* img "fichier.jpg" "Legende" */>}}`
   - Video : `{{</* video "extrait.mp4" "Legende" */>}}`
   - Audio : `{{</* audio "son.mp3" "Legende" */>}}`

4. Uploader les medias sur seedhost via WinSCP dans :
   ```
   html/CRITIQUES/cinema/media/films/le-nom-du-film/
   ```
   (le nom du dossier doit correspondre a celui dans content/films/)

5. Deployer : double-cliquer sur `deploy.bat`

## Previsualiser en local

```
hugo server
```
Les medias ne s'afficheront pas en local (ils sont sur seedhost).
Le texte et la mise en page oui.

## Ajouter un visionnage

Ouvrir le index.md du film, ajouter sous `viewings:` :
```yaml
  - date: 2025-02-17
    note: "Troisieme visionnage"
```
Puis redeploy.

## Trouver le chemin distant (REMOTE_PATH)

Ouvrir WinSCP, se connecter a seedhost, naviguer jusqu'au dossier html.
Le chemin affiche en haut (ex: /home/jeanmichel/html/) est le chemin
a utiliser. Ajouter CRITIQUES/cinema/ a la fin.
