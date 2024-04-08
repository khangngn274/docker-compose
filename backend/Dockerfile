FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

ENV MONGODB_USERNAME=khangngn274
ENV MONGODB_PASSWORD=14764119

CMD ["npm", "start"]