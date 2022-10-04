Delivery of notifications is critical for a FinTech company like Razorpay because it is a way to notify customers about their transactions and connect with external systems through Webhooks.

So, how did they design their notification system? let's find out

## Key requirement

1. maintaining an SLA is very important
2. guaranteed delivery via SMS, Email, Push, and Webhooks

## Existing Setup

Upon every transaction, an event/message was sent to SQS (message broker) which was consumed by a worker that then fanned out the notification through different channels.

Because we want to guarantee delivery, a state was maintained in the database that tells if the notification was successfully sent or not (esp via Webhook).

Hence, there is a component called Scheduler that pulls the unsent notifications from this database and re-queues it in SQS; thus guaranteeing the delivery.

### Challenges at scale

1. huge load on this database
2. scaling workers were limited by the IPOS on the database
3. surges, during festive seasons, affected transactional notifications

## New architecture

1. Prioritising incoming load

In order to ensure that one type of notification does not affect others, every notification type is classified with some priority and depending on which they are pushed to the corresponding SQS queue.

This ensures that a huge marketing campaign does not affect transactional messages.

2. Rate Limiting

To ensure mass notification from one customer does not affect others, we add Rate Limiter that would limit the notifications per customer and per type ensuring that critical notifications always meet the SLA.

3. Reducing DB bottleneck

We could not scale workers because of high DB load, and hence instead of doing a sync write to the database, the notifications that are unsent and need to be retried are pushed in a sync way to the database.

Because of this async write, we ensure that we write to the database in a staggered way and not put unnecessary load on it.

### Observability

To ensure we are maintaining our SLA, we have to exhaustively monitor the entire infra for any anomaly; the metrics like - health of the infra, success rate of delivery, and SLA.