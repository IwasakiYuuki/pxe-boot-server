FROM alpine:latest

RUN apk --no-cache add dnsmasq

RUN mkdir -p /var/tftp

COPY dnsmasq.conf /etc/dnsmasq.conf
COPY dnsmasq.hosts /etc/dnsmasq.hosts

EXPOSE 53/tcp
EXPOSE 53/udp
EXPOSE 67/udp
EXPOSE 69/udp

CMD ["dnsmasq", "-k"]
