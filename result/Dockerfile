FROM node:18-slim

# Add curl for healthcheck
RUN apt-get update -y 
#RUN apt-get install curl -y --no-install-recommends\
RUN rm -rf /var/lib/apt/lists*

# Add Tini for proper init of signals
#ENV TINI_VERSION v0.19.0
#ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
#RUN chmod +x /tini

WORKDIR /app

# Have nodemon available for local dev use (file watching)
RUN npm install -g nodemon

COPY package*.json ./

RUN npm ci \
 && npm cache clean --force \
 && mv /app/node_modules /node_modules

COPY . .

#ENV PORT 80

EXPOSE 80

CMD ["node", "server.js"]
