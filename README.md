# Synthia Miner
Setup CommuneX Synthia miner on Ubuntu

### 1. Update and upgrade
- Let's start with updating and upgrading our installation.

```sh
sudo apt update && sudo apt -y upgrade
```
### 2. Install dependencies  
- Install python3
```sh
sudo apt install python3
```

- Install git
```sh
sudo apt install git -y
```

- Install pipx
```sh
sudo apt install pipx -y
```

- Fix paths for pipx
```sh
pipx ensurepath
```

- Install poetry
```sh
pipx install poetry
```

- Install npm
```sh
sudo apt install npm -y
```

- Install pm2
```sh
sudo npm install pm2 -g
```


- Install curl
```sh
sudo apt install curl
```

- Or you can do all in one go.
```sh
sudo apt install python3 git curl npm pipx -y && pipx ensurepath && pipx install poetry && sudo npm install pm2 -g
```

### 3. Clone Synthia git and change directory
- Clone git
```sh
git clone https://github.com/agicommies/synthia.git
```

- Change directory
```sh
cd synthia
```

### 4. Setup Poetry

- Install dependencies for Synthia
```sh
poetry install
```

- Enter shell
```sh
poetry shell
```

### 5. Create key
- Create CommuneAi key on CommuneX, replace <key-name> with the name you want for your key
- Remember that this key will need at least 2.5 $COMAI for the burn fee when you register your miner
```sh
comx key create <key-name>
```

### 6. Create environment file.
- Make sure you have signed up for Anthropic or Openrouter and created API key. Enter the API key you want to use and save the file as env/config.env
- If you are using openrouter you will need to "OPENROUTER_API_KEY=" to the config file and add your key
```sh
nano env/config.env.sample
```


### 7. Get public IP.
- Find your public IP, you will need this for registering a module.
```sh
curl -4 https://ipinfo.io/ip
```

### 8. Register module.
- Register module on Subnet 3
- Remember that you need at least 2.5 $COMIA for the burn fee
- Replace <key-name> with your key
- Replace <your-public-IP> with your IP
- You can also change the port if you want.
```sh
comx module register my-test-miner <key-name> --ip <your-public-IP> --port 8000 --netuid 3 
```

### 9. Test miner.
- Make sure you have signed up for Anthropic or Openrouter and created API key. Enter the API key you want to use and save the file as env/config.env
- Don't forget to replace <key-name> with the name of your key (step 5).
- Openrouter example.
```sh
comx module serve synthia.miner.anthropic.OpenrouterModule <key-name> --subnets-whitelist 3 --ip 0.0.0.0
```

- Anthropic example.
```sh
comx module serve synthia.miner.anthropic.AnthropicModule <key-name> --subnets-whitelist 3 --ip 0.0.0.0
```
- If all looks to be working you can abort with CTRL+C and go to the next step.

<br/><br/>

### 10. Start miner with pm2 and check logs
- Start miner, remember to replace <pm2-name> with the name you want.
- Also replace <key-name> with your key.
```sh
pm2 start "comx module serve synthia.miner.anthropic.OpenrouterModule <key-name> --subnets-whitelist 3 --ip 0.0.0.0" --name <pm2-name>
```

- Start logs.
```sh
pm2 <pm2-name> logs
```

