FROM s390x/node:12-buster 

ENV BUILD_DEPS='libica-utils'

RUN set -x \
&&  apt-get update \
&&  apt-get install -y $BUILD_DEPS --no-install-recommends \
&&  rm -rf /var/lib/apt/lists/* \
&&  apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false

RUN mkdir -p /home/node/app && chown -R node:node /home/node/app

RUN mkdir -p /home/node/app/builtAssets && chmod 777 /home/node/app/builtAssets
# Create app directory
WORKDIR /home/node/app

USER node

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
# COPY --chown=node:node ../package*.json ./
COPY --chown=node:node package*.json ./
RUN npm install

# Bundle app source
# COPY --chown=node:node ../ .
COPY --chown=node:node . .

EXPOSE 8080
CMD [ "npm", "start" ]
