---
date: 2019-07-29
tags:
- java
- contract-first
- api-first
- tdd
- bdd
- open-api
title: doing contract-first with no sweat, is it possible?
description: ''
published: false
cover_image: ''
slug: ''
canonical_url: false
series: false

---
## Is it possible?

Whenever I heard someone saying that they wanted to start building services using contract-first approach I used to frown on them. Why? It seemed kind of pointless to create all that contract ahead, and see it changes during development.

The documentation, tests, end everything would be required to be updated whenever a change is needed. I don't know about your team, but here we deal with a lot of changes. So I always looked at this approach as it was "great in theory, but in practice....".

Recently I found there is a pragmatical way to apply this technique, and there are a lot of tools that help keeping everything updated from a "single source of truth", while enabling to execute good practices, like "TDD" and "BDD" for integration tests, with no sweat.

Today we will learn how we can leverage the openapi-first approach into the development cycle.

### OpenAPI Specification

You probably have heard of Swagger at least once, right? They were the ones that kind of standardized a way to write api first, and generate code later. Eventually they open-sourced this standard, and is a way to describe RESTful webservices.

How it works? It's easier to show:

    openapi: 3.0.2
    info:
      title: Sample API
      contact:
        name: Gabriel Couto
      version: 1.0.0
    
    paths:
    /uppercase:
        post:
          summary: Make any string uppercase
          operationId: postToUppercase
          requestBody:
            description: "A message"
            required: true
            content:
              text/plain;charset=utf-8:
                schema:
                  type: string
                  minLength: 1
                  example: "some message to convert"
          responses:
            '200':
              description: "OK"
              content:
                text/plain;charset=utf-8:
                  schema:
                    type: string
                    example: "SOME MESSAGE TO CONVERT"
            '400':
              description: "Bad Request"

As you may figure out, this is a simple service that turn some input string on `/uppercase` endpoint and returns it in uppercase. 