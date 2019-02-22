# Stretch amd64

## Optional : Build

```
sudo docker build -t g4bzh/alexa-base-stretch -f Dockerfile .
```

## Run

Need 3 parameters:
* Sound device
* Snips assisant
* jarvis commands

```
sudo docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assisant  -v mycommands:/opt/jarvis/jarvis-commands g4bzh/alexa-base-stretch
```

# Stretch rpi


## Install Docker on rpi

```
curl -sSL https://get.docker.com | sh
usermod -aG docker pi
```

## Optional : Build

```
sudo docker build -t g4bzh/alexa-base-stretch:pi -f Dockerfile .
```

## Run

Need 3 parameters:
* Sound device
* Snips assisant
* jarvis commands

```
docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assisant  -v mycommands:/opt/jarvis/jarvis-commands g4bzh/alexa-base-stretch:rpi
```
