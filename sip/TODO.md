## DONE

* draft new client lib with `legacy` support; figure out the architecture of detection and etc.
* Write IPFS-based proto
* see if IPFS pubsub/room has signatures - it has peerId, so it should be secure - there are NO SIGNATURES
* implement built-in promisification
* very simple pubsub impl
* solve the js-ipfs lock issue so we can test N instances at the same time - see ipfs tests and etc
* learn IPFS architecture and re-evaluate the design
* consider localtunnel (lt) instead of pubsub, will be easier and more anonymous: BETTER MAKE IT TUTORIALS
* how does routing work currently in js-ipfs?? why does IPNS depend on "dht being implemented"; DHT is implemented since 0.24.0
* can we broadcast content requests via the DHT? can we improve pubsub? ; NOT A SMART IDEA
* IPFS impl to use pubusb to get missing; also re-eval the pubsub model, perhaps sending a message to someone in the swarm is sufficient
* figure out IPNS slowness and how to work around; also IPNS is not implemented in js-ipfs
* Move out client to a new repo
* Decide on the new set of modules - `stremio-addon-sdk`, `stremio-addon-client`, `stremio-aggregators`
* consider the response formats - everything will be wrapped
* Move out SDK/docs to a new repo
* think about catalog pagination and Search; consider filters for Discover - maybe an internal thing for Cinemeta: search will be a new resource, pagination part of the ID
* stremio-aggregators
* stremio-addon-{sdk,client} and stremio-aggregators: think of code style, consider linter/flux/etc.
* Docs: explain idProperty better or change the standard to make more sense
* Figure out reloading/refresh - will just re-initialize an aggregator every time
* stremio-aggregators: consider reloading behaviour (addoncollection), i.e. what happens when an addon is installed or removed; DECIDED: we just re-construct everything
* FIGURE OUT: addon discovery
* Extra args
* think about publishing/discovery and claiming an ID; ipns solves that, but url-based addons do not
* FIGURE OUT: user-installed add-ons: will be a separate AddonCollection
* SDK: enforce to at least lint the manifest (e.g. .catalogs)
* consider stremio-addon-models that also enforces types/validation; OR implement a linter; also lint/validate the manifest
* basic tests for stremio-addon-sdk
* basic tests for stremio-aggregators
* Publish to the API: `addonPublish { transportUrl, transportName } -> { success: 1 }`
* think about whether we should bring back auto landing pages and how; also this can play along with SEO if there is a page for everything; also think of landing pages + authentication such as put.io; nah, this works via in-stremio page (app.strem.io/addon?url=...)
* consider cache - should be a concern of the transport, mostly the p2p one
* consider how to handle JSON parse errors and 404
* Write Docs

## TODO

* Write Spec
* SDK: Default function for publish (crawls all known resources), also validates and should be ran in testing too
* `stremio-addon-client`: ability to set header for every request (for example `X-User-ID`)
* Tutorials like 'Create a hosted add-on with nodejs', 'Create a hosted add-on with Python', 'Create a hosted add-on with Go', 'Create a hosted add-on with PHP', 'Create a hosted add-on with C#'
* Example: publish an add-on via now.sh; also publishToCentral
* Example: publish an add-on via localtunnel; consider other possibilities that are easy
* Tutorial: how to make a metadata add-on with search

## TODO p2p

* stremio p2p add-ons: consider a tendermint-like architecture where the replication service runs; replicationService<->add-on; this can connect directly via the stremio add-on protocol itself (over HTTP), and be a separate module "stremio-addon-p2p-replicator" or smth; that way even legacy add-ons can be replicated
* stremio addons Proto SDK, with http and ws (supernode) exposed connections
	ipfs config with bootstrap nodes, webrtc/websocket local multiaddrs
	test them in an automated test
	in `--publish` mode, log a gateway-based ipfs url to the manifest (it references peer ID, therefore the addon can update itself with IPNS)
* IPFS `requestUpdate` message: broadcast a message to the creator peer and "aggregator" peers to fetch / update an entry; use WebRTC 
* IPFS delegated nodes helping with routing and broadcasting/keeping track of `requestUpdate`
* IPNS over js-ipfs using the delegated routing nodes
* example addon based on the SDK
* tutorial: 'Create and publish a peer-to-peer addon with NodeJS'
* UI: figure out how to show add-ons that have not been online for a while - because they will just get increasingly outdated, but not offline