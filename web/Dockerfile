FROM node:18 AS base
CMD [ "bash" ]

# build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
RUN npm ci && npm run test && npm run build

# hosting in nginx
FROM nginx:latest As production
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf