# pi-hole-blocklists

### Upgrading / Reconfiguring:

Pull latest image

    docker pull pihole/pihole
    
 Remove old container

    docker rm -f pihole


Start container with the newer base image

    docker run -d \
    --name pihole \
    -p 53:53/tcp \
    -p 53:53/udp \
    -p 67:67/udp \
    -p 88:80 \
    -p 8080:443 \
    -e PUID=1000 -e PGID=1000 \
    -e TZ=Europe/Berlin \
    -v /mnt/pihole/pihole/:/etc/pihole/ \
    -v /mnt/pihole/dnsmasq.d/:/etc/dnsmasq.d/ \
    -e 1.1.1.1 \
    -e 8.8.8.8 \
    --dns=127.0.0.1 --dns=1.1.1.1 \
    --cap-add=NET_ADMIN \
    --restart=unless-stopped \
    pihole/pihole:latest
