---
layout: post
title: AWS Lambda vs Azure Function Latency
---

I recently saw [this](https://www.reddit.com/r/programming/comments/56t76l/aws_latency_comparison_api_gateway_vs_lambda_vs/) reddit post
 about these [graphs](https://www.prerender.cloud/lambda-latency).
As of the time of writing this it seems the API Gateway -> Lambda has a ~270 ms mean response time. Most of the time is because of the API Gateway but it still leaves around ~60 ms for basic Lambda.

I have thought about using Lambda with functional languages like Clojure. The ideas of Serverless Architecture and functional languages seems like a good fit.
In my current job I use .Net and I have been learning and playing with  F#.
Luckily Azure Functions offer F# support but unfortunately I couldn't find any information about latency.
The following are some of my own tests and conclusions.

I setup the following test code in two Azure Functions.

TestFSharp1
```fsharp
open System
open System.Net;
open System.Net.Http;
open System.Net.Http.Headers;

let Run (req: HttpRequestMessage, log: TraceWriter) =  
    let resp = new HttpResponseMessage(HttpStatusCode.OK)
    resp.Content <- new StringContent("Hi")
    resp
```

AzureFunctionSpeedTest
```fsharp
open System
open System.IO
open System.Net
open System.Net.Http
open System.Net.Http.Headers

let Run (req: HttpRequestMessage, log: TraceWriter) =  
    let stopWatch = System.Diagnostics.Stopwatch.StartNew()
    let req = WebRequest.Create(Uri("https://????.azurewebsites.net/api/TestFSharp1"))
    use resp = req.GetResponse()
    stopWatch.Stop()
    let resp = new HttpResponseMessage(HttpStatusCode.OK)
    resp.Content <- new StringContent(stopWatch.Elapsed.TotalMilliseconds.ToString())
    resp
```

Nothing too complex.
A simple API that returns "Hi" and another one that calls that API and returns the response time.


There are two basic states that both AWS Lambda and Azure Functions can be in: Cold or Warm.
Cold means that the code is not loaded into a container and needs to be started: The language byte code needs to be loaded, libraries need to be load, etc.
Warm means that everything is mostly ready to be executed.

In the graphs from Lambda I am assuming that the code is in a "warm" state.
In my informal tests I saw times of around ***10 ms internal response time*** if I pinged every minute. ***Almost 6 times faster than Lambda(assuming not using API Gateway).***
I am not sure my test is exactly apples to apples but it seems Azure Functions is much faster than Lambda at least in a warm state.

For the cold state the story was different. It was common to see start times of 10+ seconds.The highest I saw was 34 seconds.
People have tried to keep the function in a warm state by calling it every 4 minutes but that has [issues](https://github.com/Azure/azure-webjobs-sdk-script/issues/298) depending on use cases.

I love the idea of Serverless Architecture and it is in its infancy.
There is a lot of room for growth and not a lot of platforms yet.
Even though AWS started the tend, in one way (warm response time) Azure is already doing well. Looking forward to see what happens in the coming years.
