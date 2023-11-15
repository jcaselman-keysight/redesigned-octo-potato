FROM centos:7

ARG eggplant_flavour="redhat"
ARG eggplant_version=23.0.0
ARG eggplant_archive=Eggplant_${eggplant_flavour}_${eggplant_version}.tgz
ARG eggplant_url="https://downloads.eggplantsoftware.com/downloads/Linux/${eggplant_archive}"

LABEL "org.opencontainers.image.authors"="Frederik Carlier <frederik.carlier@keysight.com>"
LABEL "org.opencontainers.image.url"="https://eggplantsoftware.com/"
LABEL "org.opencontainers.image.documentation"="https://docs.eggplantsoftware.com/"
LABEL "org.opencontainers.image.vendor"="Keysight Technologies"
LABEL "org.opencontainers.image.title"="Eggplant functional"

WORKDIR /tmp

RUN curl $eggplant_url --output ${eggplant_archive}.tgz \
&& tar xvzf ${eggplant_archive}.tgz \
&& rm ${eggplant_archive}.tgz \
&& rpm -i Eggplant_${eggplant_flavour}/Eggplant${eggplant_version}.rpm \
&& rm -rf Eggplant_${eggplant_flavour}

RUN yum install -y xorg-x11-server-Xvfb libXrender gnu-free-sans-fonts \
# epgw dependencies
&& yum install -y libvncserver turbojpeg

WORKDIR /root

# Set the backend to libgnustep-back-headless to remove the dependency on X;
# disable Bonjour Discovery to disable a segfault:
RUN /usr/local/bin/defaults write Eggplant GSBackend libgnustep-back-headless \
&& /usr/local/bin/defaults write Eggplant BonjourDiscoveryEnabled false \
&& /usr/local/bin/defaults write Eggplant ScriptFont FreeSans \
&& /usr/local/bin/defaults write Eggplant ScriptLogFont FreeSans \
&& /usr/local/bin/defaults write Eggplant AcceptEULA YES \
&& /usr/local/bin/defaults write Eggplant AcceptPrivacyAgreement YES