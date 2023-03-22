When a user makes an API call to the backend and encounters a network issue causing the call to fail, one common solution is to retry the call assuming that the APIs are idempotent.

However, when multiple clients simultaneously retry their calls, it can cause a "Thundering Herd" problem, overwhelming the server and making it difficult to recover. In this article, we will discuss how to address this issue by implementing Exponential Backoff and Jitter.

## Retrying is brutal

The simplest way to retry failed API calls is to repeat the call immediately in a loop for a specified number of attempts. However, this approach can make the problem worse at scale.

Imagine the server is already overwhelmed with requests, and each client retries every single connected API call that has failed. This creates more pressure on the server and leaves no room for recovery.

## Exponential Backoff

Exponential Backoff is a retry strategy that introduces a delay between retries, increasing the delay exponentially with each retry attempt.

This approach gives servers a breathing space and allows them time to recover. Instead of repeating the API call back-to-back, we introduce a delay that increases with each retry attempt.

Adding exponential backoff reduces immediate retries but there is still a chance that the retries repeating at the same time will continue to bombard the server concurrently.

## Jitter to the rescue

To further improve this approach, we can add a jitter to the retry intervals. Jitter refers to adding some random delay to the retry interval to avoid retries coinciding.

This approach helps to distribute the retries and prevent them from adding to the problem. By introducing randomness, we can ensure that the retries are distributed across a wider time interval, reducing the chances of coincidences during retries.

### Caveats

When implementing Exponential Backoff and Jitter, there are two key things to keep in mind. First, it is essential to add random jitter to the retry interval to avoid coincidences during retries. Second, ensure that the retries are exponentially spaced, so that the time interval between retries increases with each attempt.
