FROM node:14 as builder

# Install pnpm
RUN npm i -g pnpm@6.7.x

# install dependencies
WORKDIR /app
COPY pnpm-*.yaml ./
COPY services/svelte/package.json ./services/svelte/
RUN pnpm install --frozen-lockfile


WORKDIR /app/services/svelte

# Copy all local files into the image.

COPY ./services/svelte .
RUN npm run build

# ###
# # Only copy over the Node pieces we need
# # ~> Saves 35MB
# ###
# FROM node:14-alpine

# WORKDIR /app
# COPY --from=builder /app .
# COPY . .

EXPOSE 3000
CMD ["node", "./build"]
