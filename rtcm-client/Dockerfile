FROM node:14-alpine as builder
WORKDIR /rtcm-client
COPY package.json /rtcm-client
COPY . /rtcm-client
RUN npm install
RUN npm run build

# ------------------------------------------------------
# Production Build
# ------------------------------------------------------
FROM nginx:1.16.0-alpine
COPY --from=builder /rtcm-client/dist /usr/share/nginx/html/rtcm-client
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

