# 1. Image de base : un Linux minimal avec Python 3.11 déjà installé
FROM python:3.11-slim

# 2. Dossier de travail dans l'image
WORKDIR /app

# 3. Copier d'abord SEULEMENT la liste des bibliothèques, puis les installer
# (couche mise en cache tant que requirements.txt ne change pas)
COPY requirements.txt .
RUN --mount=type=cache,target=/root/.cache/pip pip install --default-timeout=120 --retries 10 -r requirements.txt

# 4. Copier ensuite le code et le modèle (ils changent plus souvent)
COPY app.py .
COPY model/ model/

# 5. Valeur par défaut : charger le modèle depuis le dossier model
ENV MODEL_URI=model

# 6. Documenter le port utilisé par l'API (ne publie rien)
EXPOSE 8000

# 7. Commande lancée au démarrage du conteneur
# --host 0.0.0.0 : API joignable depuis l'extérieur du conteneur
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
