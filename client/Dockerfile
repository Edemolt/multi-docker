# Stage 1: Build the application
FROM node:16-alpine as builder

USER node

RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY --chown=node:node ./package.json ./
RUN npm install

COPY --chown=node:node ./ ./
RUN npm run build

# Stage 2: Serve the application with Nginx
FROM nginx
EXPOSE 3000

# Copy Nginx configuration
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy the build output from the builder stage
COPY --from=builder /home/node/app/build /usr/share/nginx/html


