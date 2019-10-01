# PyCon 2017

Notes I took from PyCon 2017 in Portland.

## The Unexpected Effective of Python in Science

Jake VanderPlas

[Slide Deck](https://speakerdeck.com/jakevdp/the-unexpected-effectiveness-of-python-in-science), [Video](https://www.youtube.com/watch?v=ZyjCqQEUa8o)

* PyCon's Mosaic:
	* Data
	* Web
	* Different community uses different tools
* Employed by UW eScience Institute (tagline: advancing data-intensive discovery in all fields)
* Perspective of an astronomer
	* Kepler
	* JWST (James Webb Space telescope)
	* Large Synoptic Survey Telescope (LSST)
* Why is python such an effective tool in science?
	* Inter-operability with other languages ("Python as Glue")
	* Batteries included + third party modules ("Python as Applications")
	* Simplicity & Dynamic Nature: For day-to-day exploration of scientists, speed of exploration is more important than speed of execution
	* Open ethos well-fit to science
		* LIGO (gravitational wave) is using Python

![img](img/2017-05-19%2009.52.00.jpg)
![img](img/2017-05-19%2009.58.32.jpg)
![img](img/2017-05-19%2009.59.00.jpg)
![img](img/2017-05-19%2010.00.23.jpg)
![img](img/2017-05-19%2010.01.41.jpg)
![img](img/2017-05-19%2010.07.44.jpg)
![img](img/2017-05-19%2010.08.44.jpg)


## Big picture software testing: unit testing, Lean Startup, and everything in-between

Itamar Turner-Trauring

[Slide deck](https://codewithoutrules.com/pycon2017/)

* How should you test your software?
	* Early years: ad-hoc manual testing
	* Later: 100% automated test coverage. Problem: there are things that automated test won't catch.
	* These are inflexible answers!

* Four stages:
	* Understanding users
	* Correct functionality
	* Prevent Change
	* Understanding Runtime Behavior

* Automated test prevent change
	* If you are changing the UI / code base / functionality constantly, don't change


## Next Level Testing

James Saryerwinnie

Testing that goes beyond unit test and integration test

[Video](https://www.youtube.com/watch?v=jmsk1QZQEvQ)

#### Property based testing

* e.g. absolute.py:
* Write assertion about the properties of a function
* Generate random input data that violates these assertions
* Minimize the example to be as simple as possible
* `hypothesis`:
	* powerful test data generation
	* generate minimal test cases on failure
	* integrates with `pytest`, etc
* Example: `JMESPATH`, a query language for json
* CI/Travis integration

#### Fuzz testing

* `AFL`: American Fuzzy Lop (primarily run on C, has a Python port)
* Coverage guided fuzzer
* Fast
* Simple to use
* Smarter to test all the possibilities of your code, faster than brute force

#### Stress testing

* Same input, difference execution order due to threading
* Assert properties and invariants about the code
* Catch synchronization issues

#### Mutation testing

* What test the test?
* Modify the program in a small way
* RUn your test suite
* If a test fails, success
* If no tests pass, mutation survives
* Library: `cosmic-ray`
	* Takes a long time to run

## Dr. Microservices, Or How I Learned to Stop Worrying and Love the API

Ryan Anguiano

[Video](https://www.youtube.com/watch?v=OuhCYGLByJg)

* Don't start a new project with microservices just because you wan tto
* Hard to pivot from business standpoint
* Core of project should be rigidly defined
* Switch to microservices because you need to, not because you want to.

* The monolith:
	* Very large Django app
	* Old Python
	* Dependency Hell (80+ lines `requirements.txt`)
	* Deployment interrupts entire app

* Breaking up the monolith
	* Analyze your data flow
	* concentrate the getting the most obvious pieces like your accounts, locations, things that can be broken off

* Building a migration road map
	* Evaluate diff tools
	* Use solutions that best meet your needs
	* Tools: MANTL, docker, ansible, elasticsearch, kafka..,

Services and API design

* Standardize two methods of communication
	* Syn - HTTP REST
	* Asyn - Kafka messages
* The twelve-factor app is a good guide
	* Declarative configuration
	* Env portability
* Do not make breaking changes to API endpoints
	* Increment endpoint version or add new point
	* Always test every older endpoint version
* Separating data stores
	* Every database should only be accessed by a single service
	* If a database needs to be accessed by several logics, wrap it in REST API

* Microservices toolset creation
	* Auth
	* Messaging
	* Log settings
	* Correlation IDs
	* Middleware

DevOps and Infrastructure design

* Use docker to develop in the same env as production
* Use Terraform and ansible for configuration-based infrastructure
* Use CI to automate deployments

Logging and analytics

* Send all logs into data pipeline
* Send all docker logs into Kafka using logspout
* Send all syslog into Kafka using Kafka Connect
* Correlations IDs on all initial actions. Use CIDs in logs and all communications between devices.

## 5 ways to deploy your Python web app in 2017

Andrew T. Baker, Python web developer at Twilio

[Video](https://www.youtube.com/watch?v=vGphzPLemZE)

#### `ngrok`:

* a tool for secure tunnels to localhost (in a pinch)
* Pros:
	* fast and easy
	* handy for demos and hacking on webhooks
* Cons:
	* Stops when you close your laptop
	* random domains (unless you pay)
	* **definitely** doesn't scale

#### Heroku

* Pairs with gunicorn web server for python

* Pros:
	* One app 24/7 for free
	* Zero server management (don't need to)
	* Add-ons ecosystem
* Cons:
	* Scaling is easy but gets pricey
	* Server customization is hard
	* Some of the add-ons are better than others

#### Serverless

* Your app will be running only when someone use it.
* Example: AWS lambda (but other cloud providers has it)
* Pairs with Zappa (wrapper around aws lambda)

Pros:

* Economical for small to medium loads
* Good for "spikey" traffic
* Zero server config

Cons:

* Relatively new technique
* Less fun without Zappa
* Can be trickly to troubleshoot

#### Virtual Machines

* The workhorse of the internet (e.g. EC2 instance, GC compute engine)
* Pros:
	* Full control
	* Scale as much as your wallet
	* Economical if you are careful
* Cons:
	* More work for you
	* There's a lot more to learn
	* Harder to predict ultimate costs

#### Docker

* Attempt to balance between Heroku (less legwork, less control) and virtual machines (more legwork, more control)

* Pros:
	* Helps with dev / prod parity
	* Nice for microservices
	* Impress your friends
* Cons:
	* Newest technique, best practice is still being settled
	* Works best when you go "all in"
	* Docker comes with its own learning curve

## A gentle introduction to deep learning with TensorFlow

Michelle Fullwood

[Slide deck](https://michelleful.github.io/PyCon2017/#/), [Video](https://www.youtube.com/watch?v=5e0TbyCkbCY)

* Target: feed-forward neural network - how to train them, optimize them

## Instagram's Migration From Python 2 to Python 3

Lisa Guo, Hui Ding

[Video](https://www.youtube.com/watch?v=66XoCk79kjM)

* Python 2 -> Python 3 gotchas:
	* Unicode encode / decode
	* Iterators
* Type hinting was a key factor in Instagram's move to python 3
* Python 3 saved @instagram 12% of CPU and up to 30% of memory for certain services.
* Conclusion: It's possible, it's worth it, make it happen!

## Do it For Science

Kathryn (Katy) Huff - Professor at UIUC

[Slide Deck](https://katyhuff.github.io/2017-05-20-pycon/#/), [Video](https://www.youtube.com/watch?v=kaGS4YXwciQ)

Challenges of the world:

#### Water

* US EPA WNTR water network resilience: written in Python, code in GitHub
* Open Global Glacier Model: 43 open issues

#### Climate

* github.com/cambecc/earth
* aospy: automated climate data analysis and management (for atmospheric science)
* The Python-ARM Radar Toolkit

#### Energy

* CLUS : nuclear fuel cycle simulation framework
* PyNe (Python Nuclear Engineering)

#### Health

* pulse2percept


## It's time for `datetime`

Mario Corchero

[Video](https://www.youtube.com/watch?v=2BRdKf6WYIQ), [More reference](https://opensource.com/article/17/5/understanding-datetime-python-primer)

Tips:

* Always use time zones
* use dateutil pytz to handle time zone
* always use UTC when working with timestamps
* Remember that a day is not always made of 24 hours
* Keep your time zonedb up date date
* Always test your code against scenarios such as time zone changes

* Find a time standard: we use second by convention
	* UT1
	* TAI (Cesium atomic time)
	* UTC

* Further complications:
	* Time zones
	* Daylight saving time

* Timestamps vs. Wall Time
	* `datetime.datetime.now()` doesn't set timezones. Use `datetime.datetime..utc` (?)
	* `now = dt.datetime.now(gettz("Europe/Madrid"))`
	* Tip: if yo need to return in a different timezone, convert to UTC at the border
	* Tip: if working with future wall times, don't "resolve them" until you need them

* Date and time serialization
	* datetime is not JSON serialization
	* Solution 1: Convert to string: `isoformat()`
	* Solution 2: Use integers for an epoch based time standard
	* Solution 3: Use object and hooks to serialize in JSON (`{'day': 31, 'month': 9 ...}`)

* Time arithmetic
	* Time
	* Stop and think about the real meaning of the operation
	* Always use UTC

* Libraries worth mentioning: pytz, dateutil, arrow/pendulum, astropy (great), freezegun (good for tests w.r.t. time)

## Temporal Date Structures with SQLAlchemy and Postgres

Joseph Leingang

[Video](https://www.youtube.com/watch?v=2Za9kca3Tu0)

* Use case: user move around, so the time zone is not stable
	* 1st iteration: logging
	* 2nd: Versioned tables: friends table, vs the friends history table (that documents the timezone history per use)
	* 3rd: Per property tracking. Friends table, friends clock table, location history

* In postgres:
	* Ranges: you can consider datetime ranges to be continuous. Many operations available:
		* Containment
		* Overlaps
		* Extract the upper bound
		* Compute the intersection
		* Is range empty
		* ... check out postgres docs
	* Exclusion

* Skip the SQL, Go Straight to Alchemy
	* Python wrapper for SQL
	* Under the hood: TemporalModel Declared Attributes
	* Clock tick: made into a Python ContextManager

* Take Aways:
	* If you need to keep history, trade offs apply
	* For a lot of the models, and a lot of properties, you get A LOT of tables
	* Doing things in bulk is very challenging
	* Postgres and SQLAlchemy are very powerful!

* Open source package: github.com/CloverHealth/temporal-sqlalchemy

## Static Types for Python

Jukka Lehtosalo, David Fisher

* Add static types to Python using `mypy`
* Mypy is an experimental optional static type checker for Python that aims to combine the benefits of dynamic (or "duck") typing and static typing. Mypy combines the expressive power and convenience of Python with a powerful type system and compile-time type checking. Mypy type checks standard Python programs; run them using any Python VM with basically no runtime overhead.

## An Introduction to Reinforcement Learning

Jessica Forde

[Github repo](https://github.com/jzf2101/intro_rl), [Video](https://www.youtube.com/watch?v=k1UuTyW2uFc)


## Human Machine collaboration for Improved Analytical Processes

Tony Ojeda

[](https://www.youtube.com/watch?v=s0u_UkVecx0)

* Follett Education Group
* Co-founder of District Data Labs
* Co-author of applied text analysis with Python

* Recent update in AI: can AI automate our jobs? Tony doesn't think this is an appropriate question
* How can we combine human and machine abilities to produce better outcomes than either could on their own? (Not Human vs. Machine, but Human + Machine)
* Analytical Process:
	* Ingesting
	* Wrangling
	* Analysis
	* Modeling
	* Visualization
* Need to deconstruct the process and decide which step(s) should be completed by humans and/or machines. That lead to the question: which tasks are better for humans or machines?

* Human:
	* Sensory tasks
	* Social / language / communication tasks
	* General or domain knowledge tasks
	* Task requiring flexibility, adaptability, or creativity
	* Exploratory or investigative tasks

* Machine:
	* Precision
	* Processing vast amount of info
	* Memory and recollection
	* Repetitive tasks where consistency is important

* Designing collaborative process (interfaces for tasks "hand-off")
	* Example: Create: category aggregations
		* Tasks: id categorical variables and unique values
		* Natural language understanding
		* General and/or domain knowledge
		* Similarity in meaning
		* Sometimes creativity

Key takeaways (somewhat intuitive):

* Human machine collaboration is important and very useful
* We can design these processes via deconstruction into tasks and steps
* Pay special attention to the interfaces
* Plenty of room for development and advancement in this area, and Python already contains a lot of the tools we need to make these process

## Library UX: Using abstraction towards friendlier APIs

Mali Akmanalp

Library UX

[Slide deck](bit.ly/abstraction-talk)

Why care about UX? (UX for humans)

* Good UX reduces mistakes.
* Good UX minimizes distractions.
* Good UX makes complex tasks routine
* Good UX drives adoption. (Example nice UX libraries: django, flask, requests, etc)

Abstractions:

* As programmers, we are primarily in the business of dealing wth abstractions.
* Abstraction is about hiding details in a controlled way.
* Hiding details provides a stable interface

Abstraction in Python:

* Functions
* Classes

Pitfalls:

* Leaky abstractions: you try to hide the details but the details somehow still leaks" to the user.

Under-abstraction:

* Guts everywhere
* State everywhere
* Control flow everywhere

Over-abstraction

* Coupling: to change one thing, you must change all the things
* Cohesion: A thing that does too many things at the same time.

How to decide level of abstraction?

* There is a PM staying of "Press release first" - decide on a high level what you want to API to do, and work backwards from that
* "Imaginary code" second: think about the library API before dealing with the technical details
* Rewrite usage examples with existing libraries (sort of like test-driven development?)

Incremental architecture

* Good architecture and abstraction decisions follow from domain knowledge
* Adding things incrementally: err on the side of building less structure up front

Trick:

* More layers can make things cleaner. (Examples: bokeh charts, bokeh glphs, bokeh JS; SQLAlchemy ORM, SQLAlchemy Core, etc)

## Python Data Visualization Landscape

Jake VanderPlas

[Slide Deck](https://speakerdeck.com/jakevdp/pythons-visualization-landscape-pycon-2017), [Video](https://www.youtube.com/watch?v=FytuB8nFHPQ&t=115s)

![img](img/2017-05-20%2016.33.02.jpg)
![img](img/2017-05-20%2016.51.00.jpg)

Cluster Centers:

#### Matplotlib

Strengths:

* Designed like Matlab, switching was easy
* Many rendering backends (different file formats)
* Can reproduce just about any plot (with a bit of effort
* Well-tested, standard tool for over a decade

Weaknesses:

* API is imperative and often overly verbose (Lots of boilerplate code to do simple plots; not very expressive)
* Sometimes poor stylistic defaults
* Poor support for web/interactive graphs
* Often slow and complicated for large data.

#### Descendent of Matplotlib:

* `pandas`: lots of default plotting options that simplify boilerplate code
* `seaborn`: focus on statistical data visualization; wraps around of

#### Javascript:

* Lingua Franca of the web
* `bokeh`: built with interactivity in mind
	* Advancage: web view , interactivity. Handles large and/or streaming datasets; imperative and declarative layer
	* Disadv: no vector output; smaller output
* `plotly`:
	* Adv: similar to bokeh
	* Disadv: Some features require a paid plan

#### Viualization for larger data

* datashader (fast server-side engine for dynamic data aggregation)
	* Compute layer that works with bokeh
	* Rather than sending data to the client, it aggregates data and send pixels
	* Can handle interactive visualization of billions of rows
* Others: vaex, OpenGL

#### Holoviews

* Datasets themselves stored in objects that automatically produce intelligent visualizations
* Also handle geographical data & time series

#### Altair

* What if instead of passing around pixels, we pass around visualization specifications plus data?
* Underlying library: Vega, Vega-lite
* "Declarative Visualizations"

#### Declarative Viz vs Imperative Viz

* Declarative: SQL-like
* Imperative: Pandas like
* Vega: itself is a declarative specifications for visualizations, built on D3. (write JSON)
* Vega-lite: a simpler declarative specification aimed at statistical visualization
* Altair: a Python API that creates Vega-lite JSON specifications
* Coming in Altair 2.0: includes a grammar of interaction

## Fuzzy Search Algorithms: How and When to Use Them

Jiaqi Liu

[Slide deck](https://github.com/jiaqi216/fuzzy-search-talk)

#### Soundex (phonoeics )
* PostgresSQL has fuzzy string match as an extension
* Pros: Deterministic / easy to implement; fast
* Cons: Limited to language / dialect; consider only letters

#### Levenshtein Distance

* aka edit distance
* Damerau-Levenshtein: also consider transpositions
* Pitfall: comparing addresses
* Cons: pairwise comparison; might need customization (e.g. addresses)

#### N-Gram/Trigram

* Compare the set intersection of n-gram of two strings
* Postgres has trigram build in
* You can also build cosine similarity algorithms on top of trigrams
* To speed up in postgres: gist and gin indexes for trigrams
* Pros: more context!
* Cons: slower - need to calculate n-gram for each string

#### More context:

* nltk wordnet
* Word2Vec

## Probabilistic Programming with PyMC3

Christopher Fonnesbeck

#### Stochastic language "primitives"
* Distribution over values
* Distribution over functions
* Conditioning (make variables based on other distributions)

PyMC3: used for Bayesian inference

Why Bayes? - The bayesian approach is attractive becaus it is useful. its usefulness derives in large measure from its simplicity.

Three steps of probability

#### Encode a Probability Model

1. Prior distribution: quantifies the uncertainty in latent variables
	* Likelihood function: condition our model on the observed data
1. Infer values for latent variables
	* Probabilistic programmiing abstracts the inference procedure
1. Check your models

Probabilistic Programming is not new. Before Python:

* WinBUGS: closed source, objective pascal
* PyMC3: started in 2003
	* PP framework for fitting arbitrary probability models
	* Based on theano
	* Implements next generation Bayesian inference methods

MCMC: simulates a markov chain for which some function of interest is unique, invarant, limiting distribution.

* Metropolis sampling

* Hamiltonian Monte Carlo: uses a physical analogy a frictionless particle moving on a hyper surface. Require auxiliary variables (position and momentum) to be set.
* Variational inference: good for big datasets. Take some known distribution to approximate for unknown distribution.

References:

* Probabilistic Programming & Bayesian Methods for Hackers


## One Data Pipeline to Rule Them All

Sam Kitajima-Kimbrel (Data Platform of Twilio) - sam@twilio.com

#### Problems with Patch work of solutions for DB:

* Multiple data sources
* Multi data sinks
* N^2 connection paths
* No source of truth for schemas (schema change is all manual and takes a lot of time)
* No correctness guarantees

#### New & shiny:

* One (and only one) way to publish data
* Common storage tooling (libraries, etc)
* Common schemas
* Verifiable delivery and correctness

Event sourcing architecture

* Consumer systems doesn't have to be the same system.
* Kafka is the backbone of Twilio's pipeline
* Trillions of events per day in LinkedIn

Managed Kafak-like services:

* Heroku
* AWS Kinesis

Kafka pipeline architectuer

* Each applicaton source is a separate "topic" in kafak stream
* Each consumer

Tips & Tricks:

* Schemas are really really important. (MongoDB is tempting for its schema-less things, but you will pay massive tech debts later)
	* Schema validations: avro, thrift, protocol buffers
	* They ended up using Avro. Multiple language support, dynamic and static bindings, automatic corss-grading, compact binary serialization
* Enforce schemas at produce time (at data creation)
	* Topic metadata:
		* given a topic name, what schema are in this topic?
		* how do we resolve duplicates? What fields uniquely ID a record?
		* What field and logic let us choose among or merge multiple versions?
		* What tells us that the data is correct?

Components / Tooling that they build in house:

* Metadata Registry API
* Producer / Consumer library: accepts avro object, conform the schema, and serialize / deserialize the object according the the schema

#### producer systems:

PHP, Ruby, Node Snowflake... -> REST + JSON to producer API -> Kafka

#### Consumer systems:

* Archival storage (S3): Twiliofs data lake. Kafka (7-day retention) -> Copycat (Kafka Connect) -> Amazon S3 <-> Copydog (spark job to sort and de-dupe unique record sets)
* Warehousing and structured analytics: Data Marts (on Redshift), supports loading data from S3
* Batch processing & Ad-hoc analysis: Spark (has S3 data driver)
* Stream processing: Spark streaming coneected to Kafak, can store to a new Kafka connect topic, etc
* Online query systems

#### How do I know the data is correct?

* Monitoring: The monitoring offset is byitself a Kafka streaming

Recap:

* Event oriented data pieline
* Commong producer and consumer libraries
* Costrong schema validation and planned migrations
* Verifiable delivery and correctness

## Building Stream Processing Applications

Amit Ramesh, Qui Nguyen

#### Why streaming processing?

Over batch:

* Lower latency on results
* Most data is unbounded, so streaming model is more flexible

Yelp also went through the migration from batch to stream: more real time monitoring using spark streaming

#### Putting an application together

* Example: ad compaign metrics
* Goal: from various logs, construct each metrics overtime
* Streaming proessing pipelien: source of streaming data (Kafka) -> stream processing engine (Spark streaming) -> data Sink (kafka / Cassandra)

Operations:

1. Ingestion: kafka reader into spark streaming (`from pyspark.streaming.kafka import ... `)
2. Stateless transforms (single events): e.g. filtering, projection
3. Stateful transforms (window of events): e.g. sliding window aggregation
4. Keyed stateful transforms (e.g. MapReduce-like aggregation, and/or joining across multiple streams)
5. Publishing: write to some slink. (e.g. S3)

I may be able to use spark streaming to do streaming computations for metrics ledger?

#### Design principle and tradeoffs

* Horizontal scalability: break out your data into resonable-sized chunks so that it is easier to scale horizontally
	* Random partioning for stateless transforms
	* Keyed partioning for keyed transforms
	* Watchout: hot spots / data skew
* Handling failures
	* Idempotency: operation that can be applied for more than once and have the same effect.
	* Both in poutput to data sink and in local state (joining, aggregation)
	* Consistency (Every read sees a current view of the data) vs availability (capacity to handle requests)
		* Some system pick one, be aware
		* Other let you choose (e.g. Cassandra)
		* Streaming application runs continuously, so most cases user optimize for availability

## Kubernetes for Pythonistas

Kelsey Hightower

* What containers are, and why they are important, especially for Python users
* DevOps: "Group Therapy for Sys Admins"
* How to we make it better?
* Containers: "static linking on steroids"
	* Packaging format: package all the dependency into a single tarball, download it, and build from scratch
* Kubernetes: next gen automation -> work orchestration
