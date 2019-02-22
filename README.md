
sudo docker build -t g4bzh/alexa-base-stretch -f Dockerfile .

sudo docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assisant  -v mycommands:/opt/jarvis/jarvis-commands g4bzh/alexa-base-stretch


rpi

curl -sSL https://get.docker.com | sh
usermod -aG docker pi

docker build -t g4bzh/alexa-base-stretch:rpi -f Dockerfile .
sudo docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assisant  -v mycommands:/opt/jarvis/jarvis-commands g4bzh/alexa-base-stretch:rpi
