FROM node:12.16.3-stretch-slim AS build

WORKDIR /opt/front

RUN yarn config set registry https://registry.npmjs.org/

COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile --registry https://registry.npmjs.org/

COPY . .
RUN yarn build

FROM nginx:1.15.7-alpine

COPY --from=build /opt/front/dist /usr/share/nginx/html/
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80