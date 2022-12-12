FROM node as builder

WORKDIR /app

COPY . .

RUN npm install && npm run build

# FROM httpd

# COPY --from=builder /app/dist /usr/local/apache2/htdocs/