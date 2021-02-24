# Copyright (c) 2020 Project CHIP Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG BUILD_VERSION

# All tools required for compilation belong in chip-build, forms "truth" for CHIP build tooling
FROM pan2048/mbed-os-env-cmake:latest

# This Dockerfile contains things useful for an interactive development environment
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ENV LANG en_US.utf8

# these are installed for terminal/dev convenience.  If more tooling for build is required, please
#  add them to chip-build (in integrations/docker/images/chip-build)
RUN apt-get update
RUN apt-get install -y locales && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
RUN apt-get -fy install git sudo \
    apt-utils procps lsb-release \
    docker.io
RUN groupadd -g $USER_GID $USERNAME
RUN useradd -s /bin/bash -u $USER_UID -g $USER_GID -G docker -m $USERNAME
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME
RUN chmod 0440 /etc/sudoers.d/$USERNAME

RUN chown -R $USERNAME:$USERNAME /home/$USERNAME
RUN echo "PATH=/home/$USERNAME/bin:${PATH}" >> /home/$USERNAME/.bashrc
