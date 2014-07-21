JAXB Codec
===================

This module adds support for encoding and decoding XML via JAXB.

Add `JAXBEncoder` and/or `JAXBDecoder` to your `Feign.Builder` like so:

```java
JAXBContextFactory jaxbFactory = new JAXBContextFactory.Builder()
    .withMarshallerJAXBEncoding("UTF-8")
    .withMarshallerSchemaLocation("http://apihost http://apihost/schema.xsd")
    .build();

Response response = Feign.builder()
                         .encoder(new JAXBEncoder(jaxbFactory))
                         .decoder(new JAXBDecoder(jaxbFactory))
                         .target(Response.class, "https://apihost");
```

Alternatively, you can add the encoder and decoder to your Dagger object graph using the provided JAXBModule like so:

```java
JAXBContextFactory jaxbFactory = new JAXBContextFactory.Builder().build();

Response response = Feign.create(Response.class, "https://apihost", new JAXBModule(jaxbFactory));
```