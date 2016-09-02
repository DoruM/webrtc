FROM dreamnetwork/coturn:4.4.5.3
MAINTAINER David Witherspoon <david.witherspoon@kaazing.com>

ADD turnserver.conf /etc/turnserver.conf
RUN turnadmin -a -u user -r mycompany.org -p password




# We don't want the default run as we would like to run commands itself
# Also we would like docker logs to show the turn output
RUN chmod 755 /etc/service/turnserver/run

CMD /usr/bin/turnserver

# NOTE
