MultiStage build

    # from node docker images
    FROM node:alpine as node
    WORKDIR /app
    COPY . .
    RUN npm install 
    RUN REACT_APP_STAGE=prod npm run build --prod

    #  multi-stage
    FROM nginx:latest
    COPY --from=node    /app/build /usr/share/nginx/html
    EXPOSE 80