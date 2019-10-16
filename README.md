## Scenario definition
### Describe your users behaviour
#### Scenario
##### scenario
#### Base structures
##### exec
##### group
##### pause
##### pace
##### rendezVous
#### Loops
##### repeat
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
##### I.e. you control virtual users arrival rate
##### atOnceUsers
##### rampUsers
##### constantUsersPerSec
##### rampUsersPerSec
##### heavisideUsers
##### nothingFor
##### incrementUsersPerSecNew!
#### Closed injection steps
##### I.e. you control number of concurrent virtual users)
##### constantConcurrentUsers
##### rampConcurrentUsers
##### incrementConcurrentUsersNew!
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
#### HTTP verb
##### get
##### post
##### put
##### delete
##### head
##### patch
##### options
##### httpRequest
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
