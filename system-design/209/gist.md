The emergency button on the Uber app is life-saving; and the service powering it needs to be available 24 x 7, no matter what!

So, how did Uber design such a service? How did they make it highly available; here's a quick gist about its system design 👇‍

## Information Gathering

When the emergency button is pressed, we first need to gather all the critical information and send it to the server. The critical information could be

- Current Location
- Vehicle and Trip Details
- Rider and Driver Details

## Capturing Location

When the emergency button is pressed, we do not just need to fetch the location at that moment, instead we continuously capture the location and keep sending it to the backend.

This would help us notify the nearby police and help them keep an eye on the movement.

### Lat-long are not enough

To make tracing effective, we cannot just share the lat and long because they are incomprehensible; hence we try to deduce the address from the lat-long.

This process of deducing address from lat-long is called Reverse Geocoding.

## Notifying the police

Uber uses a 3rd party service named RapidSOS to notify nearby local authorities.

RapidSOS provides APIs to register an emergency and send live updates about the emergency. It takes care of notifying the local authorities and providing them with the necessary information.

## Notifying others

Uber not only notifies the police through RapidSOS, but it also notifies

- emergency contacts
- internal support staff for close follow-ups

The notification to all channels happens in parallel to increase the probability of someone getting notified.

## Reliability and Availability

Given that the emergency service deals with events that are urgent, important, and critical; it is extremely crucial that the service is reliable and highly available; which means

- no events loss
- persistence and retries
- fallback to every single component 

## Key Decisions

1. Location getting ingested in Kafka
2. Kafka guarantees persistence and reprocessing if required
3. RapidSOS can be down and hence apply retries on consumers
4. Emergency service notifies emergency and internal staff async