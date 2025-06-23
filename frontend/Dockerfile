# 1. Brug officiel Node image
FROM node:20-alpine

# 2. Opsæt arbejdsdirectory
WORKDIR /app

# 3. Kopier package.json og installer
COPY package*.json ./
RUN npm install

# 4. Kopier alt og byg Nuxt
COPY . .
RUN npm run build

# 5. Eksponér port og kør app
EXPOSE 3000
CMD ["npm", "run", "preview"]