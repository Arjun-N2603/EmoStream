# EmoStream: Concurrent Emoji Broadcast over Event-Driven Architecture

## Project Overview

EmoStream is a real-time emoji reaction processing system designed for live events, such as cricket matches, aiming for high concurrency and low latency.  Inspired by platforms like Hotstar, it leverages an event-driven architecture to capture, process, and distribute billions of emoji reactions, providing a dynamic and engaging user experience.

This project implements a scalable system that:

* **Captures Real-time Emoji Reactions:**  Handles a massive influx of emoji reactions from users during live events.
* **Processes Data with Kafka and Spark Streaming:** Utilizes robust technologies for message queuing and real-time stream processing.
* **Aggregates Audience Sentiment:**  Provides insights into collective audience sentiment through emoji data aggregation.
* **Delivers Real-time Updates Efficiently:**  Ensures low-latency delivery of processed emoji data to a large number of users.

## Key Features

* **API Endpoint for Emoji Ingestion:**  A REST API built with Flask/Express.js to receive emoji reactions from clients (User ID, Emoji Type, Timestamp).
* **Asynchronous Message Queuing with Kafka:**  Employs Kafka for reliable and scalable message queuing, ensuring no data loss under high load.
* **Real-time Stream Processing with Spark Streaming:**  Uses Spark Streaming to process emoji data in micro-batches for aggregation and analysis.
* **Efficient Data Aggregation:** Compresses similar emojis for efficient transmission, reducing bandwidth usage.
* **Publisher-Subscriber Architecture for Scalable Delivery:**  Implements a Pub-Sub pattern using Kafka/RabbitMQ for distributing processed emoji data to a large number of clients in real-time.
* **Comprehensive Testing:** Includes unit, load, and end-to-end tests to guarantee system stability, performance, and accuracy.

## Architecture

The EmoStream architecture follows these key stages:

1. **Emoji Capture:**
    * Clients send emoji reactions to the API endpoint.
    * The API service (Flask/Express.js) validates and forwards the data.
    * A Kafka Producer asynchronously writes emoji data to Kafka brokers.

2. **Real-time Processing:**
    * A Kafka Consumer reads emoji data from Kafka topics.
    * Spark Streaming processes the data in micro-batches (2-second intervals).
    * Aggregation logic in Spark Streaming compresses similar emojis.

3. **Real-time Delivery:**
    * A Main Publisher publishes aggregated emoji data back to a message queue (Kafka/RabbitMQ).
    * Cluster Publishers and Subscribers manage distribution to registered clients.
    * Clients subscribe to receive real-time emoji updates.
