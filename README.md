# Better Gatling Cheatsheet

After using Gatling first hand for a while, it because clear that the documentation is a bit lacking. This hopes to give more and better examples of how to use it, along with important key concepts to know and gotchas.

# Sessions

One of the trickier things to get your head around. 

#### Inspecting the session

Can at any point in a chain drop an `exec` in to print out the current session:

```scala
exec(
    session => {
        println(session)
        session
    }
)
```

#### Creating functions that explicitly require values from the session
It can be unpleasant to just use the EL syntax, and rely on something being in the session already. Much better if you can make it clear when a request requires certain values from the session.
After spending a day trying to pass in attributes from the session into functions I was using to make API calls, it finally clicked that you can't do that. Instead you have to pass in a function to get the value you need out of the session at the point it's needed by the request. E.g:

```scala
def apiRequest(pathValue: Expression[String]): HttpRequestBuilder =
    http("/path/:pathValue")
    .get(session => pathValue(session).map(x => s"/path/$x"))

val chain: ChainBuilder =
    exec(apiRequest(session => session("pathValue").as[String]))
```

If you don't know for sure the attribute will exist in the session, you need to handle it to avoid getting lots of errors with seem to crash Gatling.
You can either use a `doIf` to check it exists before doing requests that use it:
```scala
doIf(_.contains("attribute")) {
    exec(apiRequest(session("pathValue").as[String]))
}
```
or get the session attribute via `validate`:
```scala
exec(apiRequest(session => session("pathValue").validate[String] match {
    case Success(value) => value
    case Failure(_) => "NOTFOUND"
}))
```

# Scenarios

## Scenario definition
### Describe your users behaviour

Most common imports needed:
```scala
import io.gatling.core.structure.ChainBuilder
import io.gatling.http.Predef._
import io.gatling.core.Predef._
import scala.concurrent.duration._
```

#### Scenario
##### scenario

#### Base structures
##### exec
```scala
val test: ChainBuilder =
    exec(http("Test").get("/"))
```
##### group
```scala
val test: ChainBuilder =
    group("group name") {
        exec(http("Test").get("/"))
        .exec(http("Test2").get("/test"))
    }
```
##### pause
```scala
val test: ChainBuilder =
    pause(500 milliseconds, 1 second)
    .exec(http("Test").get("/"))
```
##### pace
##### rendezVous

#### Loops
##### repeat
```scala
val test: ChainBuilder =
    exec(http("home").get("/"))
    .repeat(4)(exec(http("test").get("/test")))
```
##### during
##### asLongAs
##### foreach
##### doWhile
##### asLongAsDuring
##### doWhileDuring
##### forever

#### Conditions
##### doIf
##### doIfEquals
##### doIfOrElse
##### doIfEqualsOrElse
##### doSwitch
##### doSwitchOrElse
##### randomSwitch
```scala
val test: ChainBuilder =
    exec(http("home").get("/"))
    .randomSwitch(
        (50.0, exec(http("test").get("/test")))
    )
```
##### randomSwitchOrElse
##### uniformRandomSwitch
##### roundRobinSwitch

#### Errors handling
##### tryMax
##### exitBlockOnFail
##### exitHereIfFailed

##### Simulation configuration
##### Tune your simulation

#### Time
##### pauses
##### maxDuration

#### Throttling
##### throttle

## Feeder definition
### Inject data in your scenario

#### Feeder types
##### csv
##### tsv
##### ssv
##### jsonFile
##### jsonUrl
##### jdbcFeeder
##### redisFeeder

#### Feeder options
##### batch
##### unzip
##### shard
##### readRecords

#### Feeder strategies
##### queue
##### random
##### circular
##### shuffle

## Injection profile
### Control how users are injected in your scenario

#### Open injection steps
###### I.e. you control virtual users arrival rate
##### atOnceUsers
##### rampUsers
##### constantUsersPerSec
##### rampUsersPerSec
##### heavisideUsers
##### nothingFor
##### incrementUsersPerSec

#### Closed injection steps
###### I.e. you control number of concurrent virtual users)
##### constantConcurrentUsers
##### rampConcurrentUsers
##### incrementConcurrentUsers

## Assertions
### Check that your results match your expectations
#### Assertions
##### assertions
##### Scopes
##### global
##### forAll
##### details

#### Statistics
##### responseTime
##### allRequests
##### failedRequests
##### successfulRequests
##### requestsPerSec

#### Response time selectors
##### min
##### max
##### mean
##### stdDev
##### percentile1
##### percentile2
##### percentile3
##### percentile4
##### percentile

#### Count selectors
##### percent
##### count

#### Assertions conditions
##### lt
##### lte
##### gt
##### gte
##### between
##### is
##### in

## HTTP Action
### Define the HTTP requests sent in your scenario

#### HTTP
##### http
```scala
exec(http("home").get("/"))
```

#### HTTP verb
##### get
```scala
exec(http("home").get("/"))
```
##### post
```scala
exec(http("home").post("/"))
```
##### put
```scala
exec(http("home").put("/"))
```
##### delete
```scala
exec(http("home").delete("/"))
```
##### head
```scala
exec(http("home").head("/"))
```
##### patch
```scala
exec(http("home").patch("/"))
```
##### options
```scala
exec(http("home").options("/"))
```
##### httpRequest
```scala
exec(http("home").httpRequest("GET", "/"))
```

#### HTTP options
##### queryParam
##### multivaluedQueryParam
##### queryParamsSeq
##### queryParamsMap
##### header
##### headers
##### sign
##### signWithOAuth1
##### basicAuth
##### digestAuth
##### ntlmAuth
##### authRealm
##### resources
##### disableUrlEncoding
##### silent
##### notSilent

#### HTTP body
##### body
##### bodyPart
##### formParam
##### multivaluedFormParam
##### formParamSeq
##### formParamMap
##### form
##### processRequestBody
##### transformResponse
##### formUpload

## Checks
### Verifying server responses

#### Check
##### check
##### ignoreDefaultChecks
##### name

#### CheckIf
##### checkIf

#### Check extractors
##### find
##### findAll
##### findRandom
##### count

#### HTTP checks
##### status
##### currentLocation
##### header
##### headerRegex
##### responseTimeInMillis
##### bodyString
##### bodyBytes
##### bodyStream
##### substring
##### regex
##### xpath
##### jsonPath
##### jsonpJsonPath
##### jmesPath
##### jsonpJmesPath
##### css
##### form
##### md5
##### sha1

#### Check transformer
##### transform
##### transformOption

#### Check verifiers
##### is
##### not
##### exists
##### notExists
##### in
##### optional
##### isNull
##### notNull

#### Check saver
##### saveAs

## HTTP Protocol
### Mutualize your scenario's code and tune the behaviour of Gatling's HTTP client

#### Protocol
##### http
##### Urls
##### baseUrl
##### baseUrls
##### virtualHost
##### Proxy
##### proxy
##### noProxyFor
##### httpsPort
##### credentials
##### socks4
##### socks5

#### Headers
##### acceptHeader
##### acceptCharsetHeader
##### acceptEncodingHeader
##### acceptLanguageHeader
##### authorizationHeader
##### connectionHeader
##### contentTypeHeader
##### doNotTrackHeader
##### userAgentHeader

#### Options
##### disableFollowRedirect
##### maxRedirects
##### disableAutomaticReferer
##### disableWarmUp
##### warmUp
##### inferHtmlResources
##### nameInferredHtmlResourcesAfterUrlTail
##### nameInferredHtmlResourcesAfterPath
##### nameInferredHtmlResourcesAfterAbsoluteUrl
##### nameInferredHtmlResourcesAfterRelativeUrl
##### nameInferredHtmlResourcesAfterLastPathElement
##### nameInferredHtmlResources
##### maxConnectionsPerHost
##### shareConnections
##### enableHttp2
##### http2PriorKnowledge
##### asyncNameResolution
##### perUserNameResolution
##### localAddress
##### localAddresses
##### perUserKeyManagerFactory
##### disableCaching
##### disableUrlEncoding
##### silentUri
##### silentResources
##### basicAuth
##### digestAuth
##### ntlmAuth
##### authRealm

## WebSockets
### Define the WebSocket requests sent in your scenario

#### WebSocket
##### ws

#### Commons
##### wsName
##### connect
##### onConnected
##### close
##### sendText
##### sendBytes

#### Checks
##### await
##### checkTextMessage
##### checkBinaryMessage

#### Configuration
##### wsBaseUrl
##### wsBaseUrls
##### wsReconnect
##### wsMaxReconnects

## SSE (Server Sent Events)
### Define the SSE requests sent in your scenario

#### SSE
##### sse

#### Commons
##### sseName
##### connect
##### close

## JMS
### Define the JMS requests sent in your scenario

#### Start
##### jms

#### Commons
##### requestReply
##### send
##### queue
##### destination
##### replyQueue
##### replyDestination
##### trackerQueue
##### trackerDestination
##### noJmsReplyTo
##### selector
##### textMessage
##### bytesMessage
##### mapMessage
##### objectMessage
##### property
##### jmsType

#### Checks
##### simpleCheck
##### xpath

#### Protocol Configuration
##### jms

#### Connecting
##### connectionFactoryNameRequired
##### urlRequired
##### contextFactoryRequired
##### credentials
##### disableAnonymousConnect
##### listenerThreadCount
##### replyTimeout

#### Delivery modes
##### useNonPersistentDeliveryMode
##### usePersistentDeliveryMode

#### Message matching
##### matchByMessageId
##### matchByCorrelationId
##### messageMatcher

## MQTT FrontLine Only
### Define the MQTT requests sent in your scenario

#### Start
##### mqtt

#### Commons
##### subscribe
##### publish
##### expect
##### await
##### waitForMessages

#### Protocol Configuration
##### mqtt
##### mqttVersion_3_1
##### mqttVersion_3_1_1
##### broker
##### useTls
##### clientId
##### cleanSession
##### credentials
##### keepAlive
##### qosAtMostOnce
##### qosAtLeastOnce
##### qosExactlyOnce
##### retain
##### lastWill
##### reconnectAttemptsMax
##### reconnectDelay
##### reconnectBackoffMultiplier
##### resendDelay
##### resendBackoffMultiplier
##### timeoutCheckInterval
##### correlateBy
