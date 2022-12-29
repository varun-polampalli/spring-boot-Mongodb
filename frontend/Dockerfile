FROM node:16-alpine
RUN mkdir /build
WORKDIR /build
COPY app /build
RUN npm install
RUN npm run build
RUN npm install --global serve -y
ENTRYPOINT ["serve","-s","build"]
EXPOSE 3000