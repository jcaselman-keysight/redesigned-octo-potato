FROM ubuntu:16.04

ARG eggplant_flavour="ubuntu"
ARG eggplant_subflavour="debian"
ARG eggplant_version=23.0.0
ARG eggplant_archive=Eggplant_${eggplant_flavour}_${eggplant_version}
ARG eggplant_url="https://downloads.eggplantsoftware.com/downloads/Linux/${eggplant_archive}.tgz"

LABEL "org.opencontainers.image.authors"="Frederik Carlier <frederik.carlier@keysight.com>, Sebastien Morgant <sebastien.morgant@keysight.com>"
LABEL "org.opencontainers.image.url"="https://eggplantsoftware.com/"
LABEL "org.opencontainers.image.documentation"="https://docs.eggplantsoftware.com/"
LABEL "org.opencontainers.image.vendor"="Keysight Technologies"
LABEL "org.opencontainers.image.title"="Eggplant functional with eggdrive"

WORKDIR /tmp

RUN apt-get update \
&& apt-get install -y curl \
&& rm -rf /var/lib/apt/lists/* \
&& curl $eggplant_url --output ${eggplant_archive}.tgz \
&& tar xvzf ${eggplant_archive}.tgz \
&& rm ${eggplant_archive}.tgz \
&& dpkg -i Eggplant_${eggplant_subflavour}/Eggplant.deb \
&& rm -rf Eggplant_${eggplant_subflavour}

RUN apt-get update \
&& apt-get install -y xvfb libxft2 libxcb-render0 libxcursor1 libxcb-shm0 libjbig0 libxml2 libavahi-client3 libgomp1 libltdl7 fonts-freefont-ttf \
# epgw dependencies
&& apt-get install -y libvncserver1 libturbojpeg \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /root

# Set the backend to libgnustep-back-headless to remove the dependency on X;
# disable Bonjour Discovery to disable a segfault:
RUN /usr/local/bin/defaults write Eggplant GSBackend libgnustep-back-headless \
&& /usr/local/bin/defaults write Eggplant BonjourDiscoveryEnabled false \
&& /usr/local/bin/defaults write Eggplant ScriptFont FreeSans \
&& /usr/local/bin/defaults write Eggplant ScriptLogFont FreeSans \
&& /usr/local/bin/defaults write Eggplant AcceptEULA YES \
&& /usr/local/bin/defaults write Eggplant AcceptPrivacyAgreement YES