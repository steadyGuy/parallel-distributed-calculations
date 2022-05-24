FROM node:17-alpine AS builded_node
ENV NODE_ENV production
ENV REACT_APP_PROJECT_ID 975bf280-fd91-488c-994c-2f04416e5ee3
WORKDIR /app
COPY package.json .
COPY yarn.lock .
RUN yarn install --production
COPY . .
RUN yarn build

FROM nginx:1.21.0-alpine as production
ENV NODE_ENV production
COPY --from=builded_node /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]