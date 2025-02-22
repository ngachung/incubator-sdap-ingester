# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.8.13

RUN apt-get update && apt-get install -y apt-transport-https gnupg2
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
RUN apt-get update && apt-get install -y kubectl

COPY VERSION.txt /VERSION.txt
COPY common /common
COPY collection_manager/collection_manager /collection_manager/collection_manager
COPY collection_manager/setup.py /collection_manager/setup.py
COPY collection_manager/requirements.txt /collection_manager/requirements.txt
COPY collection_manager/README.md /collection_manager/README.md
COPY collection_manager/docker/entrypoint.sh /entrypoint.sh

RUN cd /common && python setup.py install 
RUN cd /collection_manager && python setup.py install

RUN pip install boto3==1.16.10

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
