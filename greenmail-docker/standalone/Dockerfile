FROM openjdk:8u302-jre-slim-buster
MAINTAINER https://github.com/greenmail-mail-test/greenmail (marcel.may.de@gmail.com)

#######################
# Expose ports:
# - smtp  : 3025
# - smtps : 3465
# - pop3  : 3110
# - pop3s : 3995
# - imap  : 3143
# - imaps : 3993
# - api   : 8080
#######################
EXPOSE 3025 3465 3110 3995 3143 3993 8080

#######################
# Configuration options
#######################
ENV JAVA_OPTS      -Djava.net.preferIPv4Stack=true
ENV GREENMAIL_OPTS -Dgreenmail.setup.test.all \
    -Dgreenmail.hostname=0.0.0.0 \
    -Dgreenmail.auth.disabled

#######################
# Run as user greenmail
RUN groupadd -r greenmail && useradd --no-log-init -r -g greenmail greenmail
# Note: If using Dockerfile without Maven, you must manually copy the JAR
ADD target/greenmail-standalone.jar /home/greenmail/greenmail-standalone.jar
ADD run_greenmail.sh /home/greenmail/run_greenmail.sh
RUN chown greenmail:greenmail /home/greenmail/greenmail-standalone.jar /home/greenmail/run_greenmail.sh && \
    chmod +x /home/greenmail/run_greenmail.sh
USER greenmail
WORKDIR /home/greenmail
# Run GreenMail Standalone with test setup and disabled authentication
ENTRYPOINT ["/bin/sh", "-c", "/home/greenmail/run_greenmail.sh"]
