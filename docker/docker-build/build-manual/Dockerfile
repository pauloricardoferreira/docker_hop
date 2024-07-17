ARG IMAGE_VERSION=lateste

FROM apache/hop:${IMAGE_VERSION}

USER root

#adicionando pacotes extras
RUN apk add --update --no-cache git python3 py3-pip py3-requests

## deixo exemplos de customização para download de drivers
ENV URL_ORACLE="http://nexus.saas.hand-china.com/content/repositories/rdc/com/oracle/ojdbc7/12.1.0.2/ojdbc7-12.1.0.2.jar"
ENV URL_FIREBIRD="https://github.com/FirebirdSQL/jaybird/releases/download/v5.0.3/jaybird-5.0.3.java11.zip"

RUN wget -q $URL_ORACLE -O /opt/hop/plugins/databases/oracle/lib/ojdbc7-12.1.0.2.jar

RUN wget -q $URL_FIREBIRD -O /tmp/jaybird.zip \
&& unzip /tmp/jaybird.zip -d /tmp/jaybird \
&& cp /tmp/jaybird/jaybird-5.0.3.java11.jar /opt/hop/plugins/databases/firebird/lib/ \
&& rm -rf /tmp/jaybird.*

ARG ENVIRONMENT='nenhum parametro informado'

RUN /bin/echo $ENVIRONMENT

USER hop