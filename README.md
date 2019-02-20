
sudo docker build -t g4bzh/alexa-base-stretch -f Dockerfile .

sudo docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assisant  -v mycommands:/opt/jarvis-commands g4bzh/alexa-base-stretch
