FROM ubuntu:latest

RUN mkdir -p /nfsshare

RUN apt update && apt install -y nfs-kernel-server
RUN echo "/nfsshare *(rw,sync,no_subtree_check)" > /etc/exports

CMD ["sh", "-c", "rpcbind && exportfs -ra && service nfs-kernel-server start && tail -f /dev/null"]
