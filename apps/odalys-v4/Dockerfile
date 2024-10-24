FROM node:18-alpine AS base
FROM base AS builder
# Check https://github.com/nodejs/docker-node/tree/b4117f9333da4138b03a546ec926ef50a31506c3#nodealpine to understand why libc6-compat might be needed.
# RUN apk add --no-cache libc6-compat 
# RUN apk update
# Set working directory
WORKDIR /app
# RUN npm config set registry https://registry.npmjs.org/
# RUN npm install -g turbo@1.12.5

COPY . .

RUN ls -al apps/odalys-v4

# RUN turbo prune odalys-v4 --docker
COPY apps/odalys-v4/.sentryclirc apps/odalys-v4/.sentryclirc

# Add lockfile and package.json's of isolated subworkspace
FROM base AS installer

WORKDIR /app

RUN cat apps/odalys-v4/.sentryclirc

# First install the dependencies (as they change less often)
# COPY .gitignore .gitignore
# COPY --from=builder /app/out/json/ .
# COPY --from=builder /app/out/package-lock.json ./package-lock.json
# RUN npm config set registry https://registry.npmjs.org/
# RUN npm install

# Build the project
# ARG DOTENV_FILE
# COPY --from=builder /app/out/full/ .
# COPY --from=builder /app/apps/odalys-v4/${DOTENV_FILE}  /app/apps/odalys-v4/.env
# RUN rm -f /app/apps/odalys-v4/.env.local
# COPY turbo.json turbo.json
# RUN npm run generate-translations --workspace odalys-v4
# RUN npm run build:odalys-v4

# FROM base AS runner
# WORKDIR /app

# # Don't run production as root
# RUN addgroup --system --gid 1001 nodejs
# RUN adduser --system --uid 1001 nextjs
# USER nextjs

# COPY --from=installer /app/apps/odalys-v4/next.config.js .
# COPY --from=installer /app/apps/odalys-v4/package.json .

# # Automatically leverage output traces to reduce image size
# # https://nextjs.org/docs/advanced-features/output-file-tracing
# COPY --from=installer --chown=nextjs:nodejs /app/apps/odalys-v4/public ./apps/odalys-v4/public
# COPY --from=installer --chown=nextjs:nodejs /app/apps/odalys-v4/.next/standalone ./
# COPY --from=installer --chown=nextjs:nodejs /app/apps/odalys-v4/.next/static ./apps/odalys-v4/.next/static

# CMD node apps/odalys-v4/server.js