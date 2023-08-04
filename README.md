# Blox-xyz


APICaller Class
The APICaller class is designed to manage API calls with rate limiting using a token bucket algorithm. It ensures that the API calls are made at a controlled rate, preventing excessive traffic to the API server.

Token Bucket Algorithm
The token bucket algorithm is used to control the rate at which API calls are made. The tokenBucket variable represents the number of available API calls in the current minute and starts at 15. It is decremented with each API call. If the bucket is empty, the class waits until the next minute before refilling the bucket with 14 tokens (since one call will be made after the waiting period).

Rate Limiting
The rate limiting logic is implemented in the call_me method. When this method is called, it first calculates the time elapsed since the last API call (time_since_last_call). If the elapsed time is less than 60 seconds (i.e., within the same minute), it checks if there are available tokens in the token bucket. If there are tokens, it proceeds to make the API call and decrements the token bucket. If the bucket is empty, it waits for the remaining time in the minute (60 seconds) before refilling the bucket with 14 tokens.

If the elapsed time is greater than or equal to 60 seconds (i.e., a new minute has started), the token bucket is reset to 14, allowing for a fresh set of API calls in the new minute.


Usage
To use the APICaller class, create an instance of it, and then call the call_me method with the necessary input for the API call. The method will return the API response for the given input.

APICaller apiCaller = new APICaller();

// Simulate 20 calls per minute
for (int i = 1; i <= 20; i++) {
    String input = "Input data " + i;
    String response = apiCaller.call_me(input);
    System.out.println(response);
}
 this example, we create an APICaller instance and simulate 20 API calls with different input data. The rate limiting mechanism ensures that the API calls are made at a controlled rate, conforming to the specified token bucket size and refill rate
