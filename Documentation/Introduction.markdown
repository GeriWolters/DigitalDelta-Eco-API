    This document is a proposal for an extension to the Digital Delta API, specifically for parameter-based queries, as opposed to the time-series focussed approach that the original DD API used.
    The document describes the required parts ('Minimal' level) and optional (discovery) parts ('Extended' level).

    Minimal only contains the definitions needed to retrieve measurements. The user will need to know the exact codes or names of the items to query.

    Extended provides definitions to discover information, such as finding the codes for parameters, find the measurement objects beloning to a monitoring network, etc. It is build on top of the Minimal specification.
    Every end-point in the Extended definition is optional.

    Providers (providers of data via this API) can use the definition to implement their own connector for this specification.
    Consumers (requesters of data via this API) can use the definition to connect external systems to their own systems.
    The samples given are based on the AquaDesk implementation of this specification.
