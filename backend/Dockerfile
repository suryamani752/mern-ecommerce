FROM node:18-alpine AS deps
WORKDIR /app

COPY backend/package*.json ./
RUN npm ci --omit=dev

FROM node:18-alpine AS runner
WORKDIR /app

RUN addgroup --system appgroup && \
    adduser --system --ingroup appgroup appuser

COPY --from=deps /app/node_modules ./node_modules
COPY backend/ ./backend/

USER appuser
EXPOSE 8000
CMD ["node", "backend/index.js"]
