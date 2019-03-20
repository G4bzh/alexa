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
docker run --device /dev/snd   -v snips_assistant:/opt/jarvis/stt_engines/snips/assistant  -v $PWD/mycommands:/opt/jarvis/jarvis-commands g4bzh/alexa-base-stretch:rpi
```

# Test Suite

## Test Output

```
pico2wave -l fr-FR -w /tmp/wav.wav "bonjour" && aplay /tmp/wav.wav
```


## RPI Microphone

```
pi@raspberrypi:~ $ lsusb
Bus 001 Device 006: ID 0556:0002 Asahi Kasei Microsystems Co., Ltd
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp. SMC9514 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

pi@raspberrypi:~ $ arecord -l
**** List of CAPTURE Hardware Devices ****
card 1: AK5371 [AK5371], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

```
pi@raspberrypi:~ $cat asoundrc
pcm.!default {
 type asym
  playback.pcm {
    type plug
    slave.pcm "hw:0,0"
  }
  capture.pcm {
    type plug
    slave.pcm "hw:1,0"
  }
}

docker run --device /dev/snd -v $PWD/assistant:/opt/jarvis/stt_engines/snips/assistant  -v $PWD/commands:/opt/jarvis/jarvis-commands -v $PWD/asoundrc:/root/.asoundrc  -it g4bzh/alexa-base-stretch:rpi
```
