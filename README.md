### Installation de Docker + permissions

```bash
sudo apt install docker.io docker-compose-v2 -y
sudo usermod -aG docker $USER
newgrp docker
```

### Lance les conteneurs

```bash
docker compose up -d
```

### création du projet front (nodeJS)

```bash
sudo chown -R $USER:$USER ./front
chmod -R 775 ./front
docker compose exec php composer create-project symfony/skeleton:6.4 .
mv temp-vue/* temp-vue/.* . 2>/dev/null
rmdir temp-vue
```

### création du projet back (Synfony)

```bash
docker exec -it php composer create-project symfony/skeleton temp_project
sudo chown -R $USER:$USER .
mv temp_project/* temp_project/.* . 2>/dev/null
rm -rf temp_project
```

### création du projet back (Dépendances + api-platform)

```bash
docker exec -it php composer require twig asset
docker exec -it php composer require symfony/orm-pack #répondre "n"
docker exec -it php composer require symfony/maker-bundle --dev #maker
docker exec -it php composer require api-platform/core #api-platform
```

### Configuration

Modifier le fichier .env : 
```bash
DATABASE_URL='mysql://user_name:strong_password@db:3306/database_name?serverVersion=mariadb-12.3.2'
```
