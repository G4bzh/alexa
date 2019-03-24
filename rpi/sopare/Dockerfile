FROM balenalib/rpi-raspbian:stretch

RUN set -x \
  && apt-get update \
  && apt-get install build-essential python-pyaudio python-numpy python-scipy python-matplotlib git -y \
  && cd /opt \
  && git clone https://github.com/bishoph/sopare.git \
  && cd sopare \
  && mkdir tokens \
  && mkdir samples \
  && sed -i 's/THRESHOLD.*$/THRESHOLD = 400/g' config/default.ini
