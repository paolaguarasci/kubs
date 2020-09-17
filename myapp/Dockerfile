FROM node:14
  
WORKDIR /opt/myapp

# install deps
COPY package.json /opt/myapp
RUN npm install

# Setup workdir
COPY . /opt/myapp

# run
EXPOSE 3000
CMD ["npm", "start"]