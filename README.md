# Fonction pour effectuer l'addition
function Addition {
    param (
        [double]$nombre1,
        [double]$nombre2
    )
    return $nombre1 + $nombre2
}

# Fonction pour effectuer la soustraction
function Soustraction {
    param (
        [double]$nombre1,
        [double]$nombre2
    )
    return $nombre1 - $nombre2
}

# Fonction pour effectuer la multiplication
function Multiplication {
    param (
        [double]$nombre1,
        [double]$nombre2
    )
    return $nombre1 * $nombre2
}

# Fonction pour effectuer la division
function Division {
    param (
        [double]$nombre1,
        [double]$nombre2
    )
    if ($nombre2 -ne 0) {
        return $nombre1 / $nombre2
    } else {
        return "Erreur : Division par zéro"
    }
}

# Fonction pour calculer la puissance
function Puissance {
    param (
        [double]$base,
        [double]$exposant
    )
    return [math]::Pow($base, $exposant)
}

# Fonction pour calculer le cosinus
function Cosinus {
    param (
        [double]$angleEnDegres
    )
    return [math]::Cos([math]::PI * $angleEnDegres / 180)
}

# Fonction pour calculer le sinus
function Sinus {
    param (
        [double]$angleEnDegres
    )
    return [math]::Sin([math]::PI * $angleEnDegres / 180)
}

# Fonction pour calculer la tangente
function Tangente {
    param (
        [double]$angleEnDegres
    )
    return [math]::Tan([math]::PI * $angleEnDegres / 180)
}

# Boucle principale pour exécuter la calculette
do {
    # Affiche le menu des opérations
    Write-Host "Choisissez une opération :"
    Write-Host "1. Addition"
    Write-Host "2. Soustraction"
    Write-Host "3. Multiplication"
    Write-Host "4. Division"
    Write-Host "5. Puissance"
    Write-Host "6. Cosinus"
    Write-Host "7. Sinus"
    Write-Host "8. Tangente"
    Write-Host "9. Comparer (inférieur/supérieur)"
    Write-Host "q. Quitter"

    # Demande à l'utilisateur de choisir une opération
    $choix = Read-Host "Entrez le numéro de l'opération"

    if ($choix -eq 'q') {
        break
    }

    # Vérifie si le choix est valide
    if ($choix -in 1..9) {
        # Demande à l'utilisateur de saisir les nombres nécessaires selon l'opération choisie
        if ($choix -ge 1 -and $choix -le 4) { # Pour les opérations arithmétiques de base
            $nombre1 = Read-Host "Entrez le premier nombre"
            $nombre2 = Read-Host "Entrez le deuxième nombre"

            # Convertit les entrées en nombres
            $nombre1 = [double]$nombre1
            $nombre2 = [double]$nombre2

            # Appelle la fonction appropriée selon le choix de l'utilisateur et affiche le résultat
            switch ($choix) {
                1 { $resultat = Addition -nombre1 $nombre1 -nombre2 $nombre2 }
                2 { $resultat = Soustraction -nombre1 $nombre1 -nombre2 $nombre2 }
                3 { $resultat = Multiplication -nombre1 $nombre1 -nombre2 $nombre2 }
                4 { $resultat = Division -nombre1 $nombre1 -nombre2 $nombre2 }
            }
        } elseif ($choix -eq 5) { # Pour la puissance
            $base = Read-Host "Entrez la base"
            $exposant = Read-Host "Entrez l'exposant"
            $resultat = Puissance -base ([double]$base) -exposant ([double]$exposant)
        } elseif ($choix -ge 6 -and $choix -le 8) { # Pour les fonctions trigonométriques
            $angle = Read-Host "Entrez l'angle en degrés"
            switch ($choix) {
                6 { $resultat = Cosinus -angleEnDegres ([double]$angle) }
                7 { $resultat = Sinus -angleEnDegres ([double]$angle) }
                8 { $resultat = Tangente -angleEnDegres ([double]$angle) }
            }
        } elseif ($choix -eq 9) { # Pour comparer infériorité/supériorité
            $valeur1 = Read-Host "Entrez la première valeur"
            $valeur2 = Read-Host "Entrez la deuxième valeur"
            if ([double]$valeur1 -gt [double]$valeur2) {
                $resultat = "$valeur1 est supérieur à $valeur2"
            } elseif ([double]$valeur1 -lt [double]$valeur2) {
                $resultat = "$valeur1 est inférieur à $valeur2"
            } else {
                $resultat = "$valeur1 est égal à $valeur2"
            }
        }

        Write-Output "Le résultat est : $resultat"
        
    } else {
        Write-Output "Choix invalide, veuillez réessayer."
    }

} while ($true)

Write-Host "Merci d'avoir utilisé la calculette !"
