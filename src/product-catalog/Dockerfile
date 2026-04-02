# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

FROM golang:1.25-alpine AS builder

WORKDIR /usr/src/app

COPY ./go.mod .

RUN go mod download

COPY . .

RUN go build -o product-catalog .

FROM alpine AS release

WORKDIR /usr/src/app

COPY ./products/ /usr/src/app/products/

COPY --from=builder /usr/src/app/product-catalog ./

ENV PRODUCT_CATALOG_PORT=8088

ENTRYPOINT ["./product-catalog"]
