FROM mhart/alpine-node:16

# install dependencies
WORKDIR /clientApp
COPY package.json package-lock.json ./
RUN npm ci

# Copy all local files into the image.
COPY . .

RUN npm run build

###
# Only copy over the Node pieces we need
# ~> Saves 35MB
###
FROM mhart/alpine-node:slim-16

WORKDIR /clientApp
COPY --from=0 /clientApp .
COPY . .

EXPOSE 3000
CMD ["node", "./build"]
