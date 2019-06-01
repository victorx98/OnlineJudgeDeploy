FROM python:3.7-alpine3.9

ENV OJ_ENV production

RUN mkdir -p /app
WORKDIR /app

RUN apk add --update --no-cache build-base nginx openssl curl unzip supervisor jpeg-dev zlib-dev postgresql-dev freetype-dev git nodejs nodejs-npm

RUN git clone https://github.com/victorx98/OnlineJudge.git /app

HEALTHCHECK --interval=5s --retries=3 CMD python2 /app/deploy/health_check.py


RUN pip install --no-cache-dir -r /app/deploy/requirements.txt && \
    apk del build-base --purge

RUN git clone -b mentorx https://github.com/victorx98/OnlineJudgeFE.git && cd OnlineJudgeFE && npm install && npm run build:dll && npm run build && cp -a dist ../
#RUN curl -L  $(curl -s  https://api.github.com/repos/QingdaoU/OnlineJudgeFE/releases/latest | grep /dist.zip | cut -d '"' -f 4) -o dist.zip && \
#    unzip dist.zip && \
#    rm dist.zip

ENTRYPOINT /app/deploy/entrypoint.sh
