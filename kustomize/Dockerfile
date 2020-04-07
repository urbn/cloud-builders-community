FROM gcr.io/cloud-builders/gcloud

ENV VER 3.5.3

COPY kustomize.bash /builder/kustomize.bash

ENV KUBEVAL_VERSION 0.14.0

RUN apt-get update && \
    apt-get install -y wget && \
    wget https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv${VER}/kustomize_v${VER}_linux_amd64.tar.gz && \
    tar xf kustomize_v${VER}_linux_amd64.tar.gz && \
    mkdir /builder/kustomize && \
    mv kustomize /builder/kustomize/kustomize && \
    chmod +x /builder/kustomize/kustomize && \
    chmod +x /builder/kustomize.bash && \
    wget https://github.com/instrumenta/kubeval/releases/download/${KUBEVAL_VERSION}/kubeval-linux-amd64.tar.gz && \
    tar xf kubeval-linux-amd64.tar.gz && \
    cp kubeval /usr/local/bin && \
    apt-get remove --purge -y wget && \
    apt-get --purge -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* *.tar.gz

ENV PATH=/builder/kustomize:$PATH

ENTRYPOINT ["/builder/kustomize.bash"]
