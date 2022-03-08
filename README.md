<div align="center">
    <img height="70" src="./logo.png" />
    <br />
    <br />
    <strong>Dockerized Authelia with Traefik</strong>
    <br />
    <br />
</div>

## ✔️ Setup Traefik
Setup the [Dockerized Traefik](https://github.com/sawden/traefik-base) before before you continue.

## Clone this Project
```bash
git clone https://github.com/sawden/traefik-authelia.git /opt/containers/authelia
```

---
**IMPORTANT**

This guide assumes that docker uses the user and group 'traefik' through userns-remap.

---

## Config and start authelia
```bash
# Adjust the configuration for all options with the placeholder 'your-domain.com'
nano /opt/containers/authelia/data/configuration.yml
# Create the log file 
echo "" > "/opt/containers/authelia/data/authelia.log"
# Create a 'secrets' folder.
mkdir /opt/containers/authelia/secrets/
# Create all required secrets. You can generate JWT secrets using this website: https://www.grc.com/passwords.htm
echo "YOUR_YWT_SECRET" > "/opt/containers/authelia/secrets/authelia_jwt_secret"
echo "YOUR_ENCRYPTION_KEY" > "/opt/containers/authelia/secrets/authelia_storage_encryption_key"
echo "YOUR_SMTP_PASSWORD" > "/opt/containers/authelia/secrets/authelia_notifier_smtp_password"
# Change the 'secrets' owner and permissions
sudo chmod -R 600 /opt/containers/authelia/secrets/
sudo chown -R traefik:traefik /opt/containers/authelia/secrets/
# Copy the sample env
cp /opt/containers/authelia/.env.dist /opt/containers/authelia/.env
# Edit the env
nano /opt/containers/authelia/.env
# Add users to 'users_database.yml' and remove the demo 'johndoe' user
nano /opt/containers/authelia/data/users_database.yml
# Chnage the permissions of the 'data' folder
sudo chown -R traefik:traefik /opt/containers/authelia/data
# Start 🚀 the container
docker-compose up -d
```

## Documentation and Inspiration
<strong>See the documentation [here](https://www.authelia.com/docs/) and a 
helpful source for this setup [here](https://www.smarthomebeginner.com/docker-authelia-tutorial/).</strong>