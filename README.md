# tor-0.4.5.11
```
Changes in version 0.4.5.11 - 2021-10-26
  The major change in this version is that v2 onion services are now
  disabled at the client, service, and relay: any Tor nodes running this
  version and onward will stop supporting v2 onion services. This is the
  last step in the long deprecation process of v2 onion services.
  Everyone running an earlier version, whether as a client, a relay, or
  an onion service, should upgrade to Tor 0.3.5.17, 0.4.5.11,
  or 0.4.6.8.

  o Major feature (onion service v2):
    - See https://blog.torproject.org/v2-deprecation-timeline for
      details on how to transition from v2 to v3.
    - The control port commands HSFETCH and HSPOST no longer allow
      version 2, and it is no longer possible to create a v2 service
      with ADD_ONION.
    - Tor no longer allows creating v2 services, or connecting as a
      client to a v2 service. Relays will decline to be a v2 HSDir or
      introduction point. This effectively disables onion service
      version 2 Tor-wide. Closes ticket 40476.

  o Minor features (bridge, backport from 0.4.6.8):
    - We now announce the URL to Tor's new bridge status at
      https://bridges.torproject.org/ when Tor is configured to run as a
      bridge relay. Closes ticket 30477.

  o Minor features (fallbackdir):
    - Regenerate fallback directories for October 2021. Closes
      ticket 40493.

  o Minor features (logging, diagnostic, backport from 0.4.6.5):
    - Log decompression failures at a higher severity level, since they
      can help provide missing context for other warning messages. We
      rate-limit these messages, to avoid flooding the logs if they
      begin to occur frequently. Closes ticket 40175.

  o Minor features (testing, backport from 0.4.6.8):
    - On a testing network, relays can now use the
      TestingMinTimeToReportBandwidth option to change the smallest
      amount of time over which they're willing to report their observed
      maximum bandwidth. Previously, this was fixed at 1 day. For
      safety, values under 2 hours are only supported on testing
      networks. Part of a fix for ticket 40337.
    - Relays on testing networks no longer rate-limit how frequently
      they are willing to report new bandwidth measurements. Part of a
      fix for ticket 40337.
    - Relays on testing networks now report their observed bandwidths
      immediately from startup. Previously, they waited until they had
      been running for a full day. Closes ticket 40337.

  o Minor bugfix (CI, onion service):
    - Exclude onion service version 2 Stem tests in our CI. Fixes bug 40500;
      bugfix on 0.3.2.1-alpha.

  o Minor bugfix (onion service, backport from 0.4.6.8):
    - Do not flag an HSDir as non-running in case the descriptor upload
      or fetch fails. An onion service closes pending directory
      connections before uploading a new descriptor which can thus lead
      to wrongly flagging many relays and thus affecting circuit building
      path selection. Fixes bug 40434; bugfix on 0.2.0.13-alpha.

  o Minor bugfixes (compatibility, backport from 0.4.6.8):
    - Fix compatibility with the most recent Libevent versions, which no
      longer have an evdns_set_random_bytes() function. Because this
      function has been a no-op since Libevent 2.0.4-alpha, it is safe
      for us to just stop calling it. Fixes bug 40371; bugfix
      on 0.2.1.7-alpha.

  o Minor bugfixes (consensus handling, backport from 0.4.6.4-rc):
    - Avoid a set of bugs that could be caused by inconsistently
      preferring an out-of-date consensus stored in a stale directory
      cache over a more recent one stored on disk as the latest
      consensus. Fixes bug 40375; bugfix on 0.3.1.1-alpha.

  o Minor bugfixes (onion service, TROVE-2021-008, backport from 0.4.6.8):
    - Only log v2 access attempts once total, in order to not pollute
      the logs with warnings and to avoid recording the times on disk
      when v2 access was attempted. Note that the onion address was
      _never_ logged. This counts as a Low-severity security issue.
      Fixes bug 40474; bugfix on 0.4.5.8.
```
