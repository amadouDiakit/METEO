# METEO
#WEATHER FORECAST 
#LES ETAPES
pip install requests
python script_meteo.py
Entrez le nom de la ville : Bamako

#Prévisions météo pour Bamako, ML

import requests
from datetime import datetime

def obtenir_previsions_meteo(ville, api_key):
    """Récupère les prévisions météo pour 5 jours via l'API OpenWeatherMap."""
    url = f"http://api.openweathermap.org/data/2.5/forecast?q={ville}&appid={api_key}&units=metric&lang=fr"
    try:
        reponse = requests.get(url)
        reponse.raise_for_status()  # Vérifie si la requête a échoué
        donnees = reponse.json()
        return donnees
    except requests.exceptions.RequestException as e:
        print(f"Erreur lors de la récupération des données météo: {e}")
        return None

def afficher_previsions_meteo(donnees):
    """Affiche les prévisions météo sur 5 jours."""
    if not donnees or 'list' not in donnees:
        print("Aucune donnée météo à afficher.")
        return
    
    print(f"\nPrévisions météo pour {donnees['city']['name']}, {donnees['city']['country']}\n")
    
    previsions_par_jour = {}
    for prevision in donnees['list']:
        date_heure = datetime.fromtimestamp(prevision['dt'])
        date_str = date_heure.strftime('%Y-%m-%d')
        
        if date_str not in previsions_par_jour:
            previsions_par_jour[date_str] = []

        previsions_par_jour[date_str].append(prevision)
    
    for date, previsions in previsions_par_jour.items():
        print(f"📅 {date} :")
        for prevision in previsions:
            heure = datetime.fromtimestamp(prevision['dt']).strftime('%H:%M')
            temperature = prevision['main']['temp']
            meteo = prevision['weather'][0]['description']
            vent = prevision['wind']['speed']
            print(f"  ⏰ {heure} - 🌡️ {temperature}°C, 🌥️ {meteo}, 💨 Vent: {vent} m/s")
        print("\n")

def main():
    """Fonction principale de l'application."""
    ville = input("Entrez le nom de la ville : ")
    api_key = "VOTRE_CLE_API_ICI"  # Remplacez par votre clé API OpenWeatherMap
    
    donnees_meteo = obtenir_previsions_meteo(ville, api_key)
    afficher_previsions_meteo(donnees_meteo)

if __name__ == "__main__":
    main()

#LES ETAPES
pip install requests
python script_meteo.py
Entrez le nom de la ville : Bamako

Prévisions météo pour Bamako, ML

📅 2024-12-08 :
  ⏰ 06:00 - 🌡️ 25°C, 🌥️ ciel dégagé, 💨 Vent: 3.2 m/s
  ⏰ 09:00 - 🌡️ 28°C, 🌥️ nuageux, 💨 Vent: 3.5 m/s
  ⏰ 12:00 - 🌡️ 32°C, 🌥️ ciel dégagé, 💨 Vent: 2.8 m/s

📅 2024-12-09 :
  ⏰ 06:00 - 🌡️ 24°C, 🌥️ ciel dégagé, 💨 Vent: 2.9 m/s
  ⏰ 09:00 - 🌡️ 28°C, 🌥️ nuageux, 💨 Vent: 3.2 m/s
  ⏰ 12:00 - 🌡️ 31°C, 🌥️ ciel dégagé, 💨 Vent: 2.5 m/s
