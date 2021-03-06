FROM balenalib/rpi-raspbian:stretch

RUN set -x \
        && apt-get update \
        && sed  -i 's/main/main non-free/g' /etc/apt/sources.list \
        && apt-get update \
        && apt-get install --no-install-recommends --no-install-suggests -y git  ca-cacert net-tools python-pyaudio sox libatlas-base-dev swig alsa-utils make g++ python-dev libttspico-utils  curl jq nano perl sox wget whiptail libsox-fmt-mp3 \
        && apt-get install --no-install-recommends --no-install-suggests -y gnupg apt-transport-https wget git dirmngr python-pip python-sklearn python-dev bzip2 supervisor init-system-helpers \
        && echo "deb https://raspbian.snips.ai/stretch stable main" > /etc/apt/sources.list.d/snips.list \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D4F50CDCA10A2849 \
        && apt-get update \
        && apt-get install -y snips-asr \
        && cd /opt \
        && git -c http.sslVerify=false clone https://github.com/G4bzh/jarvis.git \
        && git -c http.sslVerify=false clone https://github.com/G4bzh/snowboy \
        && cd snowboy/swig/Python \
        && make \
        && cp _snowboydetect.so /opt/jarvis/stt_engines/snowboy/ \
        && cp snowboydetect.py /opt/jarvis/stt_engines/snowboy/ \
        && cd ../.. \
        && cp -r resources/ /opt/jarvis/stt_engines/snowboy/ \
        && cp  /opt/jarvis/stt_engines/snowboy/resources/alexa/alexa*.umdl  /opt/jarvis/stt_engines/snowboy/resources/alexa.umdl \
        && sed -i -e '/EUID/,+4 s/^/#/' /opt/jarvis/jarvis.sh \
        && sed -i "s/#cmd = 'arecord/cmd = 'arecord/g" /opt/jarvis/stt_engines/snowboy/maindecoder_sox.py \
        && sed -i "s/cmd = 'rec/#cmd = 'rec/g" /opt/jarvis/stt_engines/snowboy/maindecoder_sox.py \
        && usermod -a -G audio root \
        && echo "" > /opt/jarvis/config/bing_speech_api_key \
        && echo "0" > /opt/jarvis/config/check_updates \
        && echo "snips" > /opt/jarvis/config/command_stt \
        && echo "true" > /opt/jarvis/config/conversation_mode \
        && echo "stt_engines/pocketsphinx/jarvis-dictionary.dic" > /opt/jarvis/config/dictionary \
        && echo "0" > /opt/jarvis/config/gain \
        && echo "" > /opt/jarvis/config/google_speech_api_key \
        && echo "master" > /opt/jarvis/config/jv_branch \
        && echo "" > /opt/jarvis/config/jv_bt_device_mac \
        && echo "" > /opt/jarvis/config/jv_bt_device_name \
        && echo "10" > /opt/jarvis/config/jv_timeout \
        && echo "false" > /opt/jarvis/config/jv_use_bluetooth \
        && echo "fr_FR" > /opt/jarvis/config/language \
        && echo "stt_engines/pocketsphinx/jarvis-languagemodel.lm" > /opt/jarvis/config/language_model \
        && echo "" > /opt/jarvis/config/last_update_check \
        && echo "0.1" > /opt/jarvis/config/min_noise_duration_to_start \
        && echo "6.1%" > /opt/jarvis/config/min_noise_perc_to_start \
        && echo "0.5" > /opt/jarvis/config/min_silence_duration_to_stop \
        && echo "6.1%" > /opt/jarvis/config/min_silence_level_to_stop \
        && echo "" > /opt/jarvis/config/osx_say_voice \
        && echo "La commande a échouée" > /opt/jarvis/config/phrase_failed \
        && echo "La commande n'est pas implémentée" > /opt/jarvis/config/phrase_misunderstood \
        && echo "" > /opt/jarvis/config/phrase_triggered \
        && echo "Bonjour chef" > /opt/jarvis/config/phrase_welcome \
        && echo "false" > /opt/jarvis/config/play_hw \
        && echo "/dev/null" > /opt/jarvis/config/pocketsphinxlog \
        && echo "false" > /opt/jarvis/config/rec_hw \
        && echo "sox" > /opt/jarvis/config/recorder \
        && echo "false" > /opt/jarvis/config/send_usage_stats \
        && echo "puis" > /opt/jarvis/config/separator \
        && echo "true" > /opt/jarvis/config/show_commands \
        && echo "false" > /opt/jarvis/config/snowboy_checkticks \
        && echo "0.4" > /opt/jarvis/config/snowboy_sensitivity \
        && echo "" > /opt/jarvis/config/snowboy_token \
        && echo "1.0" > /opt/jarvis/config/tempo \
        && echo "alexa" > /opt/jarvis/config/trigger \
        && echo "magic_word" > /opt/jarvis/config/trigger_mode \
        && echo "snowboy" > /opt/jarvis/config/trigger_stt \
        && echo "svox_pico" > /opt/jarvis/config/tts_engine \
        && echo "chef" > /opt/jarvis/config/username \
        && echo "e1c7c773-4743-4863-86c3-334d51e86689" > /opt/jarvis/config/uuid \
        && echo "" > /opt/jarvis/config/wit_server_access_token \
        && apt-get remove --purge --auto-remove -y g++ make swig \
        && rm -rf /var/lib/apt/lists/* /opt/snowboy

CMD ["/opt/jarvis/jarvis.sh", "-n"]
