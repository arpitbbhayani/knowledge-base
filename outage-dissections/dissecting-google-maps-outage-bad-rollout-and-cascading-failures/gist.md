Google Maps Outage Dissection

On the 18th of March, 2022, Google Maps faced a major outage affecting millions of people for a couple of hours. The outage happened due to a bad deployment.

Although a bad deployment does not sound too bad, the situation worsens when there are cascading failures if 3 services have a synchronous dependency, forming a chain-like A -> B -> C.

If A goes down, it will have some impact on B, and if the impact is big enough, we might see B going down as well; and extending it, we might see C going down.

This is exactly what happened in this Google Outage. Some services had a bad deployment, and they started crashing. Tile Rendering service depended on it, and the Tile rendering service went down because of retries.

The Direction SDK, Navigation SDK directly invoked the Tile rendering service for rendering the maps, which didn't work, causing a big outage.

✨ How to remediate a bad deployment?

Rollback as soon as possible.

✨ Preventing cascading outages

 - Reject requests when the server is exhausted
 - Tune the performance of the webserver and networking stack of the server
 - Monitor the server resource consumption and set alerts
 - Add circuit breakers wherever possible.